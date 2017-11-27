---
title: "Метод IHostSyncManager::CreateRWLockWriterEvent"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IHostSyncManager.CreateRWLockWriterEvent
api_location: mscoree.dll
api_type: COM
f1_keywords: IHostSyncManager::CreateRWLockWriterEvent
helpviewer_keywords:
- CreateRWLockWriterEvent method [.NET Framework hosting]
- IHostSyncManager::CreateRWLockWriterEvent method [.NET Framework hosting]
ms.assetid: 70e488c2-cf53-4dc0-ba52-74372d215c41
topic_type: apiref
caps.latest.revision: "13"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: c89dec681102f96f96f1d7f3e802ded0a2df7b4d
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="ihostsyncmanagercreaterwlockwriterevent-method"></a><span data-ttu-id="b46d5-102">Метод IHostSyncManager::CreateRWLockWriterEvent</span><span class="sxs-lookup"><span data-stu-id="b46d5-102">IHostSyncManager::CreateRWLockWriterEvent Method</span></span>
<span data-ttu-id="b46d5-103">Создает объект события автоматического сброса для реализации блокировки модуля записи.</span><span class="sxs-lookup"><span data-stu-id="b46d5-103">Creates an auto-reset event object for the implementation of a writer lock.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="b46d5-104">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="b46d5-104">Syntax</span></span>  
  
```  
HRESULT CreateRWLockWriterEvent (  
    [in]  SIZE_T cookie,  
    [out] IHostAutoEvent **ppEvent  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="b46d5-105">Параметры</span><span class="sxs-lookup"><span data-stu-id="b46d5-105">Parameters</span></span>  
 `cookie`  
 <span data-ttu-id="b46d5-106">[in] Файл cookie, связываемый с события автоматического сброса.</span><span class="sxs-lookup"><span data-stu-id="b46d5-106">[in] A cookie to associate with the auto-reset event.</span></span>  
  
 `ppEvent`  
 <span data-ttu-id="b46d5-107">[out] Указатель на адрес [IHostAutoEvent](../../../../docs/framework/unmanaged-api/hosting/ihostautoevent-interface.md) экземпляра, или значение null, если не удалось создать объект события.</span><span class="sxs-lookup"><span data-stu-id="b46d5-107">[out] A pointer to the address of an [IHostAutoEvent](../../../../docs/framework/unmanaged-api/hosting/ihostautoevent-interface.md) instance, or null if the event object could not be created.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="b46d5-108">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="b46d5-108">Return Value</span></span>  
  
|<span data-ttu-id="b46d5-109">HRESULT</span><span class="sxs-lookup"><span data-stu-id="b46d5-109">HRESULT</span></span>|<span data-ttu-id="b46d5-110">Описание</span><span class="sxs-lookup"><span data-stu-id="b46d5-110">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="b46d5-111">S_OK</span><span class="sxs-lookup"><span data-stu-id="b46d5-111">S_OK</span></span>|<span data-ttu-id="b46d5-112">`CreateRWLockWriterEvent`успешно возвращен.</span><span class="sxs-lookup"><span data-stu-id="b46d5-112">`CreateRWLockWriterEvent` returned successfully.</span></span>|  
|<span data-ttu-id="b46d5-113">ЗНАЧЕНИЕ HOST_E_CLRNOTAVAILABLE</span><span class="sxs-lookup"><span data-stu-id="b46d5-113">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="b46d5-114">Общеязыковая среда выполнения (CLR) не был загружен в процесс или находится в состоянии, в котором не может выполнять управляемый код или успешно обработать вызов.</span><span class="sxs-lookup"><span data-stu-id="b46d5-114">The common language runtime (CLR) has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
|<span data-ttu-id="b46d5-115">HOST_E_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="b46d5-115">HOST_E_TIMEOUT</span></span>|<span data-ttu-id="b46d5-116">Истекло время ожидания вызова.</span><span class="sxs-lookup"><span data-stu-id="b46d5-116">The call timed out.</span></span>|  
|<span data-ttu-id="b46d5-117">HOST_E_NOT_OWNER</span><span class="sxs-lookup"><span data-stu-id="b46d5-117">HOST_E_NOT_OWNER</span></span>|<span data-ttu-id="b46d5-118">Вызывающий объект не является владельцем блокировки.</span><span class="sxs-lookup"><span data-stu-id="b46d5-118">The caller does not own the lock.</span></span>|  
|<span data-ttu-id="b46d5-119">HOST_E_ABANDONED</span><span class="sxs-lookup"><span data-stu-id="b46d5-119">HOST_E_ABANDONED</span></span>|<span data-ttu-id="b46d5-120">Событие было отменено заблокированный поток или ожидал волокон.</span><span class="sxs-lookup"><span data-stu-id="b46d5-120">An event was canceled while a blocked thread or fiber was waiting on it.</span></span>|  
|<span data-ttu-id="b46d5-121">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="b46d5-121">E_FAIL</span></span>|<span data-ttu-id="b46d5-122">Неизвестная Неустранимая ошибка.</span><span class="sxs-lookup"><span data-stu-id="b46d5-122">An unknown catastrophic failure occurred.</span></span> <span data-ttu-id="b46d5-123">Если метод вернет значение E_FAIL, среда CLR больше не может использоваться в процессе.</span><span class="sxs-lookup"><span data-stu-id="b46d5-123">When a method returns E_FAIL, the CLR is no longer usable within the process.</span></span> <span data-ttu-id="b46d5-124">Последующие вызовы размещение методы возвращают значение HOST_E_CLRNOTAVAILABLE.</span><span class="sxs-lookup"><span data-stu-id="b46d5-124">Subsequent calls to hosting methods return HOST_E_CLRNOTAVAILABLE.</span></span>|  
|<span data-ttu-id="b46d5-125">E_OUTOFMEMORY</span><span class="sxs-lookup"><span data-stu-id="b46d5-125">E_OUTOFMEMORY</span></span>|<span data-ttu-id="b46d5-126">Не хватает памяти была доступна для создания запрошенного объекта события.</span><span class="sxs-lookup"><span data-stu-id="b46d5-126">Not enough memory was available to create the requested event object.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="b46d5-127">Примечания</span><span class="sxs-lookup"><span data-stu-id="b46d5-127">Remarks</span></span>  
 <span data-ttu-id="b46d5-128">Среда CLR вызывает `CreateRWLockWriterEvent` метод позволяет получить ссылку на `IHostAutoEvent` экземпляр для использования в своей реализации блокировку записи.</span><span class="sxs-lookup"><span data-stu-id="b46d5-128">The CLR calls the `CreateRWLockWriterEvent` method to get a reference to an `IHostAutoEvent` instance to use in its implementation of a writer lock.</span></span> <span data-ttu-id="b46d5-129">Узел может использовать указанного файла cookie для определения задач, ожидающих блокировки, вызывая итерационные методы [ICLRSyncManager](../../../../docs/framework/unmanaged-api/hosting/iclrsyncmanager-interface.md) интерфейса.</span><span class="sxs-lookup"><span data-stu-id="b46d5-129">The host can use the specified cookie to determine which tasks are waiting on the lock by calling the iteration methods of the [ICLRSyncManager](../../../../docs/framework/unmanaged-api/hosting/iclrsyncmanager-interface.md) interface.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="b46d5-130">Требования</span><span class="sxs-lookup"><span data-stu-id="b46d5-130">Requirements</span></span>  
 <span data-ttu-id="b46d5-131">**Платформы:** разделе [требования к системе для](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="b46d5-131">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="b46d5-132">**Заголовок:** MSCorEE.h</span><span class="sxs-lookup"><span data-stu-id="b46d5-132">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="b46d5-133">**Библиотека:** включена как ресурс в MSCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="b46d5-133">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="b46d5-134">**Версии платформы .NET framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="b46d5-134">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="b46d5-135">См. также</span><span class="sxs-lookup"><span data-stu-id="b46d5-135">See Also</span></span>  
 [<span data-ttu-id="b46d5-136">ICLRSyncManager-интерфейс</span><span class="sxs-lookup"><span data-stu-id="b46d5-136">ICLRSyncManager Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/iclrsyncmanager-interface.md)  
 [<span data-ttu-id="b46d5-137">IHostAutoEvent-интерфейс</span><span class="sxs-lookup"><span data-stu-id="b46d5-137">IHostAutoEvent Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihostautoevent-interface.md)  
 [<span data-ttu-id="b46d5-138">IHostManualEvent-интерфейс</span><span class="sxs-lookup"><span data-stu-id="b46d5-138">IHostManualEvent Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihostmanualevent-interface.md)  
 [<span data-ttu-id="b46d5-139">Ihostsyncmanager-интерфейс</span><span class="sxs-lookup"><span data-stu-id="b46d5-139">IHostSyncManager Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihostsyncmanager-interface.md)