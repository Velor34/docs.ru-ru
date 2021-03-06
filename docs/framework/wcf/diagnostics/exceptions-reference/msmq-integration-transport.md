---
title: Транспорт интеграции с MSMQ
ms.date: 03/30/2017
ms.assetid: 2bf9893a-fbd1-41fc-b6de-a41a44279936
ms.openlocfilehash: 52fd98354ded57bd7d7c075d4f08ca543760e598
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
ms.locfileid: "33473377"
---
# <a name="msmq-integration-transport"></a>Транспорт интеграции с MSMQ
В этом разделе перечислены все исключения, вызываемые транспортом интеграции MSMQ.  
  
## <a name="exception-list"></a>Список исключений  
  
|Код ресурса|Строка ресурса|  
|-------------------|---------------------|  
|MessageSizeMustBeInIntegerRange|Эта фабрика помещает сообщения в буфер, поэтому размер сообщений должен лежать в диапазоне целого числа.|  
|MsmqByteArrayBodyExpected|Обнаружено несоответствие между указанным форматом сериализации и телом MSMQ-сообщения. Невозможно отправить или получить сообщение. Формат сериализации ByteArray требует, чтобы тело MSMQ-сообщения имело тип byte[].|  
|MsmqCannotDeserializeActiveXMessage|Произошла ошибка сериализации ActiveX. Невозможно отправить или получить сообщение. Указанный тип variant тела не соответствует фактическому телу MSMQ-сообщения.|  
|MsmqCannotUseBodyTypeWithActiveXSerialization|Обнаружено несоответствие свойств сообщения. Невозможно отправить или получить сообщение. Задать свойство сообщения BodyType невозможно, если используется формат сериализации ActiveX.|  
|MsmqInvalidServiceOperationForMsmqIntegrationBinding|Сбой при проверке MsmqIntegrationBinding. Запуск конечной точки службы невозможен. Указанная привязка не поддерживает сигнатуру метода для указанной операции службы в указанном контракте. Исправьте операцию службы, чтобы она использовала MsmqIntegrationBinding.|  
|MsmqInvalidTypeDeserialization|При сериализации ActiveX произошел сбой, так как не распознан формат сериализации. Невозможно отправить или получить сообщение.|  
|MsmqInvalidTypeSerialization|Тип variant не распознан. При сериализации ActiveX произошел сбой. Невозможно отправить или получить сообщение. Указанный тип variant не поддерживается.|  
|MsmqStreamBodyExpected|Обнаружено несоответствие между форматом сериализации и содержимым тела. Невозможно отправить или получить сообщение. В режиме сериализации потока можно отправлять или получать только тела типа stream.|
