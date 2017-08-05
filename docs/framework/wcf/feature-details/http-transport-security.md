---
title: "Безопасность транспорта HTTP | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d3439262-c58e-4d30-9f2b-a160170582bb
caps.latest.revision: 14
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 14
---
# Безопасность транспорта HTTP
Если в качестве транспорта используется протокол HTTP, безопасность обеспечивается реализацией протокола SSL \(Secure Sockets Layer\).  Протокол SSL широко используется в Интернете для проверки подлинности службы при подключении клиента, а затем и для обеспечения конфиденциальности \(шифрования\) канала.  В этом разделе описаны функционирование SSL и его реализация в [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].  
  
## Базовый SSL  
 Лучше всего функционирование SSL можно продемонстрировать с помощью стандартного сценария, в данном случае \- веб\-сайта банка.  Сайт позволяет клиенту входить в систему с помощью имени пользователя и пароля.  После прохождения проверки подлинности пользователь может совершать различные транзакции, например просматривать балансы счетов, оплачивать счета и переводить деньги с одного счета на другой.  
  
 Когда пользователь посещает сайт впервые, механизм SSL начинает с клиентом пользователя \(в данном случае Internet Explorer\) серию согласований, которая называется *подтверждение*.  Во\-первых, SSL проводит проверку подлинности сайта банка для клиента.  Это очень важный шаг, так как в первую очередь клиенты должны знать, что они взаимодействуют с настоящим сайтом, а не подделкой, с помощью которой злоумышленники пытаются обманным путем получить их имя пользователя и пароль.  SSL проводит такую проверку подлинности с помощью сертификата SSL, предоставляемого надежным центром сертификации, таким как VeriSign.  Эта процедура основана на следующей логике: VeriSign подтверждает удостоверение сайта банка.  Поскольку Internet Explorer доверяет VeriSign, этот сайт считается надежным.  Если вы хотите осуществлять проверку с VeriSign, щелкните по логотипу VeriSign.  Сертификат VeriSign представляет утверждение подлинности с датой истечения срока действия и указанием, кому был выписан сертификат \(сайту банка\).  
  
 Чтобы инициировать безопасный сеанс, клиент отправляет серверу эквивалент приветствия, а также список алгоритмов шифрования, которые могут быть использованы клиентом для подписания, шифрования и расшифровки данных и создания хэшей.  В ответ сайт отправляет подтверждение и указывает, какой набор алгоритмов был выбран.  В ходе такого первоначального подтверждения оба участника посылают и отправляют специальные слова.  *Специальное слово* \- это случайным образом созданный блок данных, который в сочетании с открытым ключом сайта используется для создания хэша.  *Хэш* \- это новое число, наследуемое от двух чисел с использованием стандартного алгоритма, такого как SHA1.  \(Клиент и сайт также обмениваются сообщениями, чтобы согласовать, какой хэш\-алгоритм следует использовать.\) Хэш уникален и используется только для шифрования и расшифровки сообщений в ходе сеанса между клиентом и сайтом.  Как клиент, так и служба имеют исходное специальное слово и открытый ключ сертификата, поэтому обе стороны могут создать один и тот же хэш.  Следовательно, клиент проверяет хэш, отправленный службой, \(а\) используя согласованный алгоритм для вычисления хэша из данных и \(б\) сравнивая его с хэшем, отправленным службой; если хэши соответствуют друг другу, клиент может быть уверен, что хэш не был подделан.  После этого клиент может использовать этот хэш в качестве ключа для шифрования сообщения, которое содержит другой, новый хэш.  Служба может расшифровать сообщение с помощью хэша и восстановить предпоследний хэш.  Теперь накопленная информация \(специальные слова, открытый ключ и другие данные\) известна обеим сторонам, и они могут создать окончательный хэш \(или главный ключ\).  Окончательный ключ отправляется зашифрованным с использованием предпоследнего хэша.  Затем главный ключ используется для шифрования и расшифровки сообщений для сброса сеанса.  Так как клиент и служба используют один и тот же ключ, он также называется *сеансовым ключом*.  
  
 Сеансовый ключ также характеризуется как симметричный ключ или "общий секрет". Наличие симметричного ключа очень важно, так как благодаря этому обоим участникам транзакции требуется выполнять меньше вычислений.  Если бы для каждого сообщения приходилось заново обмениваться специальными словами и хэшами, это значительно бы снизило производительность.  Следовательно, конечной целью сертификатов SSL является использование симметричного ключа, благодаря чему оба участника взаимодействия могут свободно, более безопасно и эффективно обмениваться сообщениями.  
  
 Предыдущее описание представляет собой упрощенную версию происходящего, так как протокол по\-разному функционирует на разных сайтах.  Возможно также, что и клиент, и сайт создают специальные слова, которые алгоритмически сочетаются во время подтверждения, усложняя тем самым процесс обмена данными, одновременно обеспечивая его дополнительную защиту.  
  
### Сертификаты и инфраструктура открытого ключа  
 Во время подтверждения служба также отправляет свой SSL\-сертификат клиенту.  В сертификате содержится различная информация, такая как дата истечения срока действия, центр выдачи и универсальный код ресурса \(URI\) сайта.  Клиент сравнивает этот URI с универсальным кодом ресурса, с которым он взаимодействовал изначально, чтобы убедиться, что они соответствуют друг другу, затем клиент проверяет дату и центр выдачи сертификата.  
  
 Каждый сертификат имеет два ключа \(закрытый ключ и открытый ключ\), известные как *пара ключей обмена*.  Вкратце, закрытый ключ известен только владельцу сертификата, а открытый ключ можно прочитать из сертификата.  Любой из них можно использовать для шифрования и расшифровки дайджеста, хэша или другого ключа, но только как противоположные операции.  Например, если клиент осуществляет шифрование с использованием открытого ключа, только сайт может расшифровать сообщение с помощью закрытого ключа.  Аналогично, если сайт осуществляет шифрование с помощью закрытого ключа, клиент может расшифровать данные с помощью открытого ключа.  Благодаря этому клиент уверен, что обменивается сообщениями только с обладателем закрытого ключа, так как только сообщения, зашифрованные с помощью закрытого ключа, можно расшифровать с использованием открытого ключа.  При этом сайт уверен, что обменивается сообщениями с клиентом, осуществившим шифрование с использованием открытого ключа.  Такой обмен надежен только на этапе первоначального подтверждения, поэтому создание фактического симметричного ключа представляет собой гораздо более сложную процедуру.  Тем не менее, все виды взаимодействия зависят от наличия у службы действительного SSL\-сертификата.  
  
## Реализация SSL с WCF  
 Безопасность транспорта HTTP \(или SSL\) предоставляется [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] извне.  SSL можно реализовать одним из двух способов; при этом выбор способа определяется размещением приложения.  
  
-   Если в качестве узла [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] используются службы IIS, для настройки службы SSL следует использовать инфраструктуру IIS.  
  
-   Если создается резидентное приложение [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], можно привязать SSL\-сертификат к адресу с помощью средства HttpCfg.exe.  
  
### Использование служб IIS для безопасности транспорта  
  
#### IIS 7.0  
 Настройка [!INCLUDE[iisver](../../../../includes/iisver-md.md)] в качестве надежного узла \(с использованием SSL\) описана в разделе [IIS 7.0, бета\-версия: настройка SSL в IIS 7.0](http://go.microsoft.com/fwlink/?LinkId=88600).  
  
 Настройка сертификатов для использования с [!INCLUDE[iisver](../../../../includes/iisver-md.md)] описана в разделе [IIS 7.0, бета\-версия: настройка сертификатов сервера в IIS 7.0](http://go.microsoft.com/fwlink/?LinkID=88595).  
  
#### IIS 6,0  
 Настройка [!INCLUDE[iis601](../../../../includes/iis601-md.md)] в качестве надежного узла \(с использованием SSL\) описана в разделе [Настройка протокола SSL](http://go.microsoft.com/fwlink/?LinkId=88601).  
  
 Настройка сертификатов для использования с [!INCLUDE[iis601](../../../../includes/iis601-md.md)] описана в разделе [Сертификаты\_IIS\_SP1\_Ops](http://go.microsoft.com/fwlink/?LinkId=88602).  
  
### Использование средства HttpCfg для SSL  
 Для создания резидентного приложения [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] загрузите средство HttpCfg.exe, доступное на [сайте средств поддержки Windows XP с пакетом обновления 2 \(SP2\)](http://go.microsoft.com/fwlink/?LinkId=29002).  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] использовании средства HttpCfg.exe для настройки порта с сертификатом X.509 см. раздел [Практическое руководство. Настройка порта с использованием SSL\-сертификата](../../../../docs/framework/wcf/feature-details/how-to-configure-a-port-with-an-ssl-certificate.md).  
  
## См. также  
 [Безопасность транспорта](../../../../docs/framework/wcf/feature-details/transport-security.md)   
 [Безопасность обмена сообщениями](../../../../docs/framework/wcf/feature-details/message-security-in-wcf.md)