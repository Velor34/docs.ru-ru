---
title: Обращение к службам с использованием клиента
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c8329832-bf66-4064-9034-bf39f153fc2d
ms.openlocfilehash: 1ac7acda0b9065fde4ab04c80e9d26a1ec23fa6e
ms.sourcegitcommit: ccd8c36b0d74d99291d41aceb14cf98d74dc9d2b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2018
ms.locfileid: "53130992"
---
# <a name="accessing-services-using-a-client"></a>Обращение к службам с использованием клиента
Клиентские приложения необходимо создать, настроить и использовать объекты клиента или каналов WCF для взаимодействия со службами. [WCF Client Overview](../../../../docs/framework/wcf/wcf-client-overview.md) разделе представлен обзор объектов и шаги по созданию базовых объектов клиента и канала и их использованию.  
  
 В разделе приводится подробная информация о некоторых проблемах с приложениями клиента и объектами клиента и канала, которые могут пригодиться в зависимости от вашего сценария.  
  
## <a name="overview"></a>Обзор  
 В разделе описаны поведение и проблемы, связанные со следующими пунктами.  
  
-   Каналы и время существования сеанса.  
  
-   Обработка исключений.  
  
-   Понимание блокирующих проблем.  
  
-   Интерактивная инициализация каналов.  
  
### <a name="channel-and-session-lifetimes"></a>Каналы и время существования сеанса  
 Приложения Windows Communication Foundation (WCF) включает в себя две категории каналов: датаграмма и сеанс.  
  
 Объект *датаграмм* канал является каналом, в котором все сообщения являются некоррелированными. При использовании канала датаграммы на последующую операцию обычно не влияет то, что операция ввода или вывода не удалась, и тот же канал может быть использован повторно. По этой причине в каналах датаграмм обычно не возникает сбоев.  
  
 *На основе сеанса* каналы, однако, являются каналами с подключением к другой конечной точки. Сообщения в сессии всегда коррелируют с таким же сеансом с другой стороны. Кроме того, между участниками сеанса должно быть соглашение, описывающее требования к их диалогу, которые, для того чтобы сеанс считался успешным, должны быть удовлетворены. Если такого соглашения между участниками нет, в канале сеанса может возникнуть ошибка.  
  
 Откройте клиенты явно или неявно, вызвав первую операцию.  
  
> [!NOTE]
>  Попытка явно обнаружить каналы сеанса со сбоем обычно оказывается полезной, поскольку то, когда вы будете оповещены, зависит от реализации сеанса. Например, поскольку <xref:System.ServiceModel.NetTcpBinding?displayProperty=nameWithType> (с отключенным надежным сеансом) покрывает сеанс связи TCP, если при ожидании передачи данных события <xref:System.ServiceModel.ICommunicationObject.Faulted?displayProperty=nameWithType> службы или клиента, желательно получить уведомление о сбое сети незамедлительно. Но надежные сеансы (установленные привязками, в которых включен <xref:System.ServiceModel.Channels.ReliableSessionBindingElement?displayProperty=nameWithType>) предназначены для изолирования служб от незначительных сбоев сети. Если сеанс может быть повторно установлен в течение допустимого периода времени, та же привязка, настроенная для надежных сеансов, может не дать сбой, пока прерывание не будет происходить в течение более продолжительного промежутка времени.  
  
 Большинство предоставляемых системой привязок (экспонирующих каналы на уровень приложения) использует сеансы по умолчанию, однако <xref:System.ServiceModel.BasicHttpBinding?displayProperty=nameWithType> этого не делает. Дополнительные сведения см. в разделе [с использованием сеансов](../../../../docs/framework/wcf/using-sessions.md).  
  
### <a name="the-proper-use-of-sessions"></a>Правильное использование сеансов  
 Сеансы являются способом, с помощью которого можно узнать, полностью ли был завершен обмен сообщением и обе ли стороны считают его успешным. Рекомендуется, чтобы вызывающее приложение открыло канал, использовало его и закрыло канал внутри одного блока try. Если канал сеанса открыт и однократно вызван метод <xref:System.ServiceModel.ICommunicationObject.Close%2A?displayProperty=nameWithType>, и данный вызов успешно возвращается, значит сеанс был успешен. "Успешный" в данном случае означает, что все гарантии доставки, заданные привязкой, были обеспечены и другая сторона не вызвала <xref:System.ServiceModel.ICommunicationObject.Abort%2A?displayProperty=nameWithType> в канале перед вызовом <xref:System.ServiceModel.ICommunicationObject.Close%2A>.  
  
 В следующем разделе показан пример данного подхода к клиенту.  
  
### <a name="handling-exceptions"></a>Обработка исключений  
 Обработка исключений в приложениях клиента является прямой. Если канал открыт, использован и закрыт внутри одного блока try, диалог был успешен, кроме случая, если было выдано исключение. Обычно при выдаче исключения диалог прерывается.  
  
> [!NOTE]
>  Использование `using` инструкции (`Using` в Visual Basic) не рекомендуется. Это связано с тем, что конец оператора `using` может привести к исключениям, которые могут маскировать другие исключения, о которых вам, возможно, нужно знать. Дополнительные сведения см. в разделе [используйте Close и Abort для освобождения ресурсов клиента WCF](../../../../docs/framework/wcf/samples/use-close-abort-release-wcf-client-resources.md).  
  
 В приведенном ниже примере кода демонстрируется рекомендуемый шаблон клиента с помощью блока try/catch, а не с помощью оператора `using`.  
  
 [!code-csharp[FaultContractAttribute#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/faultcontractattribute/cs/client.cs#3)]
 [!code-vb[FaultContractAttribute#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/faultcontractattribute/vb/client.vb#3)]  
  
> [!NOTE]
>  Проверка значения свойства <xref:System.ServiceModel.ICommunicationObject.State%2A?displayProperty=nameWithType> является состоянием гонки и не рекомендуется для определения ситуации, когда канал можно использовать повторно или когда его нужно закрыть.  
  
 Каналы датаграммы не дают сбой, даже если исключения происходят при их закрытии. Кроме того, недуплексные клиенты, которые не смогли пройти проверку с помощью защищенного диалога, как правило, создают исключение <xref:System.ServiceModel.Security.MessageSecurityException?displayProperty=nameWithType>. Однако если дуплексному клиенту, использующему защищенный диалог, не удается пройти проверку, клиент получает вместо этого исключение <xref:System.TimeoutException?displayProperty=nameWithType>.  
  
 Более полные сведения о работе с информацией об ошибке на уровне приложения, см. в разделе [задание и обработка сбоев в контрактах и службах](../../../../docs/framework/wcf/specifying-and-handling-faults-in-contracts-and-services.md). [Ожидается исключения](../../../../docs/framework/wcf/samples/expected-exceptions.md) описываются ожидаемые исключения и показано, как их обрабатывать. Дополнительные сведения о том, как обрабатывать ошибки при разработке каналов см. в разделе [обработки исключений и ошибок](../../../../docs/framework/wcf/extending/handling-exceptions-and-faults.md).  
  
### <a name="client-blocking-and-performance"></a>Блокировка и производительность клиента  
 Когда приложение синхронно вызывает операцию типа запрос-ответ, клиент блокируется до тех пор, пока не будет получено возвращаемое значение или создано исключение (такое как <xref:System.TimeoutException?displayProperty=nameWithType>). Такое поведение аналогично локальному поведению. Когда приложение синхронно вызывает операцию объекта клиента WCF или канала, клиент не возвращает, пока уровень канала сможет записать данные в сеть, или пока не возникает исключение. И до тех пор, пока шаблон одностороннего обмена сообщениями (заданный маркировкой операции с помощью <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A?displayProperty=nameWithType>, которому присвоено значение `true`) повышает реакцию некоторых клиентов, односторонние операции также блокируются, в зависимости от привязки и того, какие сообщения уже были отправлены. Односторонние операции относятся только к обмену сообщениями, не больше и не меньше. Дополнительные сведения см. в разделе [служб односторонняя](../../../../docs/framework/wcf/feature-details/one-way-services.md).  
  
 Большие порции данных могут замедлить обработку клиента, независимо от шаблона обмена сообщениями. Чтобы понять, как обрабатывать эти проблемы, см. в разделе [большие наборы данных и потоковая передача](../../../../docs/framework/wcf/feature-details/large-data-and-streaming.md).  
  
 Если ваше приложение должно выполнять больше работы, при завершении операции, необходимо создать пару асинхронных методов интерфейса контракта службы, реализующий клиента WCF. Для этого проще всего использовать `/async` переключиться [ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md). Например, см. в разделе [как: Асинхронный вызов операций службы](../../../../docs/framework/wcf/feature-details/how-to-call-wcf-service-operations-asynchronously.md).  
  
 Дополнительные сведения о увеличение производительности клиента, см. в разделе [клиентские приложения среднего уровня](../../../../docs/framework/wcf/feature-details/middle-tier-client-applications.md).  
  
### <a name="enabling-the-user-to-select-credentials-dynamically"></a>Включение динамического выбора учетных данных пользователем  
 Интерфейс <xref:System.ServiceModel.Dispatcher.IInteractiveChannelInitializer> позволяет приложениям отображать интерфейс пользователя, что позволяет пользователю выбирать учетные данные пользователя с которыми канал создается до того, как запустятся таймеры периода времени.  
  
 Разработчики приложений могут использовать вставленный <xref:System.ServiceModel.Dispatcher.IInteractiveChannelInitializer> двумя способами. Клиентское приложение может вызвать либо метод <xref:System.ServiceModel.ClientBase%601.DisplayInitializationUI%2A?displayProperty=nameWithType> или <xref:System.ServiceModel.IClientChannel.DisplayInitializationUI%2A?displayProperty=nameWithType> (или асинхронную версию) до открытия канала ( *явные* подход) или вызвать первую операцию ( *неявное*подход).  
  
 Если использовать неявный подход, то приложение должно вызвать первую операцию в расширении <xref:System.ServiceModel.ClientBase%601> или <xref:System.ServiceModel.IClientChannel>. Если приложение вызовет что-либо другое вместо первой операции, будет создано исключение.  
  
 Если использовать явный подход, то приложение должно выполнить следующие шаги по порядку:  
  
1.  Вызывать либо <xref:System.ServiceModel.ClientBase%601.DisplayInitializationUI%2A?displayProperty=nameWithType>, либо <xref:System.ServiceModel.IClientChannel.DisplayInitializationUI%2A?displayProperty=nameWithType> (или асинхронную версию).  
  
2.  После возвращения инициализаторов вызвать либо метод <xref:System.ServiceModel.ICommunicationObject.Open%2A> в объекте <xref:System.ServiceModel.IClientChannel>, либо в объекте <xref:System.ServiceModel.IClientChannel>, возвращенном из свойства <xref:System.ServiceModel.ClientBase%601.InnerChannel%2A?displayProperty=nameWithType>.  
  
3.  Вызовите операции.  
  
 Рекомендуется, чтобы приложения для промышленного применения управляли процессом пользовательского интерфейса в соответствии с явным подходом.  
  
 Приложения, использующие неявный подход, вызывают инициализаторы интерфейса пользователя, но если пользователь приложения не сможет ответить в отведенный период времени привязки для отправки, то при возвращении пользовательского интерфейса создается исключение.  
  
## <a name="see-also"></a>См. также  
 [Дуплексные службы](../../../../docs/framework/wcf/feature-details/duplex-services.md)  
 [Инструкции: Доступ к службам с односторонним контрактом и контрактом типа запрос ответ](../../../../docs/framework/wcf/feature-details/how-to-access-wcf-services-with-one-way-and-request-reply-contracts.md)  
 [Инструкции: Службы доступа с дуплексным контрактом](../../../../docs/framework/wcf/feature-details/how-to-access-services-with-a-duplex-contract.md)  
 [Инструкции: Доступ к WSE 3.0 служба](../../../../docs/framework/wcf/feature-details/how-to-access-a-wse-3-0-service-with-a-wcf-client.md)  
 [Инструкции: Использование ChannelFactory](../../../../docs/framework/wcf/feature-details/how-to-use-the-channelfactory.md)  
 [Инструкции: Асинхронный вызов операций службы](../../../../docs/framework/wcf/feature-details/how-to-call-wcf-service-operations-asynchronously.md)  
 [Клиентские приложения среднего уровня](../../../../docs/framework/wcf/feature-details/middle-tier-client-applications.md)
