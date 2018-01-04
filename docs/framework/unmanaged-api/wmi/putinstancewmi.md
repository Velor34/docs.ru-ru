---
title: "Функция PutInstanceWmi (Справочник по неуправляемым API)"
description: "Функция PutInstanceWmi создает или обновляет экземпляр существующего класса."
ms.date: 11/06/2017
ms.prod: .net-framework
ms.technology: dotnet-clr
ms.topic: reference
api_name: PutInstanceWmi
api_location: WMINet_Utils.dll
api_type: DLLExport
f1_keywords: PutInstanceWmi
helpviewer_keywords: PutInstanceWmi function [.NET WMI and performance counters]
topic_type: Reference
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: b1996103eea87562226537f9aa90dc337c56313c
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="putinstancewmi-function"></a>Функция PutInstanceWmi
Создает или обновляет экземпляр существующего класса. Экземпляр записывается в репозиторий WMI. 

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>Синтаксис  
  
```  
HRESULT PutInstanceWmi (
   [in] IWbemClassObject*    pInst,
   [in] long                 lFlags,
   [in] IWbemContext*        pCtx,
   [out] IWbemCallResult**   ppCallResult
); 
```  

## <a name="parameters"></a>Параметры

`pInst`    
[in] Указатель на экземпляр должен иметь writen.

`lFlags`   
[in] Сочетание флагов, влияющих на поведение этой функции. Следующие значения определяются в *WbemCli.h* файла заголовка, или их можно определить как константы в коде: 

|Константа  |Значение  |Описание:  |
|---------|---------|---------|
| `WBEM_FLAG_USE_AMENDED_QUALIFIERS` | 0x20000 | Если задано, WMI не сохраняет любые квалификаторы с **Amended** flavor. </br> В противном случае набор, предполагается этот объект не локализован, что все квалификаторы — storedwith данного экземпляра. |
| `WBEM_FLAG_CREATE_OR_UPDATE` | 0 | Создайте экземпляр, если она не существует, или перезаписать его, если он уже существует. |
| `WBEM_FLAG_UPDATE_ONLY` | 1 | Обновите экземпляр. Экземпляр должен существовать для успешного вызова. |
| `WBEM_FLAG_CREATE_ONLY` | 2 | Создайте экземпляр. Вызов завершается неудачей, если экземпляр уже существует. |
| `WBEM_FLAG_RETURN_IMMEDIATELY` | 0x10 | Флаг вызывает полусинхронных вызовов. |

`pCtx`  
[in] Как правило, это значение равно `null`. В противном случае он является указателем на [IWbemContext](https://msdn.microsoft.com/library/aa391465(v=vs.85).aspx) экземпляр, который может использоваться поставщиком, предоставляющего запрошенного классы. 

`ppCallResult`  
[out] Если `null`, этот параметр не используется. Если `lFlags` содержит `WBEM_FLAG_RETURN_IMMEDIATELY`, функция немедленно возвращает `WBEM_S_NO_ERROR`. `ppCallResult` Параметр получает указатель на новый [IWbemCallResult](https://msdn.microsoft.com/library/aa391425(v=vs.85).aspx) объекта.

## <a name="return-value"></a>Возвращаемое значение

Следующие значения, возвращаемые этой функцией, определяются в *WbemCli.h* файла заголовка, или их можно определить как константы в коде:

|Константа  |Значение  |Описание:  |
|---------|---------|---------|
| `WBEM_E_ACCESS_DENIED` | 0x80041003 | Пользователь не имеет разрешения на обновление экземпляра указанного класса. |
| `WBEM_E_FAILED` | 0x80041001 | Произошла неизвестная ошибка. |
| `WBEM_E_INVALID_CLASS` | 0x80041010 | Указан недопустимый класс, поддерживающий этот экземпляр. |
| `WBEM_E_ILLEGAL_NULL` | 0x80041028 | `null` был указан для свойства, которое не может быть `null`, например, помеченного атрибутом **индексированное** или **Not_Null** квалификатор. |
| `WBEM_E_INVALID_OBJECT` | 0x8004100f | Указанный экземпляр не является допустимым. (Например, вызов метода `PutInstanceWmi` с классом возвращает это значение.) |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | Параметр не является допустимым. |
| `WBEM_E_ALREADY_EXISTS` | 0x80041019 | `WBEM_FLAG_CREATE_ONLY` Был указан флаг, но экземпляр уже существует. |
| `WBEM_E_NOT_FOUND` | 0x80041002 | `WBEM_FLAG_UPDATE_ONLY`был указан в `lFlags`, но экземпляр не существует. |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | Недостаточно памяти для завершения операции. |
| `WBEM_E_SHUTTING_DOWN` | 0x80041033 | WMI был, скорее всего, остановлен и перезапускать. Вызовите [ConnectServerWmi](connectserverwmi.md) еще раз. |
| `WBEM_E_TRANSPORT_FAILURE` | 0x80041015 | Не удалось выполнить вызов RPC удаленной процедуры связь между текущим процессом и WMI. |
| `WBEM_S_NO_ERROR` | 0 | Успешный вызов функции. |
  
## <a name="remarks"></a>Примечания

Эта функция создает оболочку для вызова [IWbemServices::PutInstance](https://msdn.microsoft.com/library/aa392115(v=vs.85).aspx) метод.

`PutInstanceWmi` Функция поддерживает создание экземпляров и обновление экземпляров только существующих классов.  В зависимости от того как `pCtx` имеет параметр, будут обновлены некоторые или все свойства экземпляра. 

Если экземпляр, на который указывает `pInst` принадлежит вызовы всех поставщиков, ответственного за классов, от которых происходит подкласса подкласс управления Windows. Все эти поставщики должны успешно завершиться для исходного `PutInstanceWmi` для успешного выполнения запроса. Сначала вызывается поставщик поддержки верхних класс в иерархии. Вызывающий порядок продолжается с подклассом класса переднего плана и переход сверху вниз, пока не достигнет Windows управления поставщика для классов, владельца экземпляра, на который указывает `pInst`.
Управление Windows не вызывает поставщики для любого дочернего класса экземпляра. 

Если приложение необходимо обновить экземпляр, который принадлежит к иерархии классов: `pInst` параметр должен указывать экземпляр, содержащий свойства, чтобы изменить. То есть, рассмотрите возможность целевой экземпляр, которому принадлежит **ClassB**. **ClassB** экземпляра является производным от **ClassA**, и **ClassA** определяет свойство **PropA**. Если приложению требуется внести изменение значение **PropA** в **ClassB** экземпляр, он должен задать `pInst` для этого экземпляра, а не экземпляр **ClassA** .

Вызов `PutInstanceWmi` на экземпляр абстрактного класса не допускается.

При сбое вызова функции, можно получить дополнительные сведения об ошибке, вызвав [GetErrorInfo](geterrorinfo.md) функции.

## <a name="requirements"></a>Требования  
 **Платформы:** разделе [требования к системе для](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок:** WMINet_Utils.idl  
  
 **Версии платформы .NET framework:**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>См. также  
[WMI и счетчиков производительности (Справочник по неуправляемым API)](index.md)