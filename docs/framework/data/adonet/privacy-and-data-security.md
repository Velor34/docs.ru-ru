---
title: "Конфиденциальность и безопасность данных | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 46fa5839-adf7-4c7c-bce3-71e941fa7de9
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Конфиденциальность и безопасность данных
Защита и управление конфиденциальными данными в приложении ADO.NET зависит от базовых продуктов и технологий, используемых для их создания.  ADO.NET не предоставляет напрямую службы безопасности или шифрования данных.  
  
## Шифрование и хэш\-коды  
 Классы в пространстве имен <xref:System.Security.Cryptography> платформы .NET Framework можно использовать из приложений ADO.NET для предотвращения несанкционированного считывания или изменения данных сторонними пользователями.  Некоторые классы являются оболочками для неуправляемого интерфейса Microsoft CryptoAPI, а другие представляют собой управляемые реализации.  В разделе [Cryptographic Services](http://msdn.microsoft.com/ru-ru/68a1e844-c63c-44af-9247-f6716eb23781) приведены общие сведения о криптографии в .NET Framework, описывается реализация криптографии, а также способы выполнения конкретных криптографических задач.  
  
 В отличие от шифрования, представляющего собой обратимый процесс, хэширование данных необратимо.  Хэширование данных может оказаться полезным в тех случаях, когда необходимо предотвратить искажение путем проверки неизменяемости данных. Если заданы идентичные входные строки, то алгоритмы хэширования всегда производят идентичные короткие выходные значения, которые легко сравнить.  Раздел [Ensuring Data Integrity with Hash Codes](../../../../docs/standard/security/ensuring-data-integrity-with-hash-codes.md) описывает способ создания и проверки хэш\-значений.  
  
## Шифрование файлов конфигурации  
 Защита доступа к источникам данным \- одна из важнейших целей защиты приложения.  Строка соединения представляет собой потенциальную уязвимость, если она не защищена.  Строки соединения, сохраненные в файлах конфигурации, хранятся в стандартных XML\-файлах, для которых в .NET Framework определен набор элементов.  Защищенная конфигурация дает возможность шифровать конфиденциальные данные в файле конфигурации.  Хотя защищенная конфигурация в первую очередь создана для приложений ASP.NET, она также может использоваться для шифрования разделов файла конфигурации в приложениях Windows.  Для получения дополнительной информации см. [Защита сведений о соединении](../../../../docs/framework/data/adonet/protecting-connection-information.md).  
  
## Обеспечение безопасности строковых значений в памяти  
 Если объект <xref:System.String> содержит конфиденциальные данные, например пароль, номер кредитной карты или персональные данные, то существует риск раскрытия этих сведений после их использования, поскольку приложение не может удалить данные из памяти компьютера.  
  
 Объект <xref:System.String> является неизменяемым; после создания его значение нельзя изменить.  Даже если создается впечатление, что произошло изменение строкового значения, в действительности в памяти создается новый экземпляр объекта <xref:System.String>, в котором данные сохраняются в виде обычного текста.  Кроме того, невозможно спрогнозировать время удаления строковых экземпляров из памяти.  Для возврата в систему памяти, освободившейся после удаления строк, применяются средства сборки мусора .NET, поэтому данный процесс является недетерминированным.  Если данные по\-настоящему конфиденциальны, то следует избегать использования классов <xref:System.String> и <xref:System.Text.StringBuilder>.  
  
 Класс <xref:System.Security.SecureString> предоставляет методы шифрования текста в памяти с помощью API\-интерфейса защиты данных \(DPAPI\).  Когда строка больше не нужна, она удаляется из памяти.  Метода `ToString` для быстрого считывания содержимого <xref:System.Security.SecureString> не существует.  Можно инициализировать новый экземпляр `SecureString`, не задавая значений, или передать ему указатель на массив объектов <xref:System.Char>.  Для работы со строкой можно использовать различные методы этого класса.  Для получения дополнительных сведений загрузите [образец приложения SecureString](http://go.microsoft.com/fwlink/?LinkId=120418), в котором демонстрируется использование класса `SecureString`.  
  
## См. также  
 [Защита приложений ADO.NET](../../../../docs/framework/data/adonet/securing-ado-net-applications.md)   
 [Безопасность SQL Server](../../../../docs/framework/data/adonet/sql/sql-server-security.md)   
 [Центр разработчиков, поставщики ADO.NET Managed Provider и набор данных](http://go.microsoft.com/fwlink/?LinkId=217917)