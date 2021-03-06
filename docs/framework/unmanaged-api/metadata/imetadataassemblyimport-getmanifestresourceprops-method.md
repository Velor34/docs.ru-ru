---
title: Метод IMetaDataAssemblyImport::GetManifestResourceProps
ms.date: 03/30/2017
api_name:
- IMetaDataAssemblyImport.GetManifestResourceProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataAssemblyImport::GetManifestResourceProps
helpviewer_keywords:
- GetManifestResourceProps method [.NET Framework metadata]
- IMetaDataAssemblyImport::GetManifestResourceProps method [.NET Framework metadata]
ms.assetid: 00be4789-ac63-4397-b2ec-1629a5c5a585
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 07237794ca45b16b1ae1ca95b1d62889f095350f
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
---
# <a name="imetadataassemblyimportgetmanifestresourceprops-method"></a>Метод IMetaDataAssemblyImport::GetManifestResourceProps
Получает набор свойств ресурса манифеста с заданной подписью метаданных.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
HRESULT GetManifestResourceProps (  
    [in]  mdManifestResource   mdmr,   
    [out] LPWSTR               szName,   
    [in]  ULONG                cchName,   
    [out] ULONG                *pchName,   
    [out] mdToken              *ptkImplementation,   
    [out] DWORD                *pdwOffset,   
    [out] DWORD                *pdwResourceFlags  
);  
```  
  
#### <a name="parameters"></a>Параметры  
 `mdmr`  
 [in] `mdManifestResource` Токен, представляющий ресурса, для которого нужно получить свойства.  
  
 `szName`  
 [out] Имя ресурса.  
  
 `cchName`  
 [in] Размер в расширенных символов из `szName`.  
  
 `pchName`  
 [out] Указатель на число расширенных символов, фактически извлеченных в `szName`.  
  
 `ptkImplementation`  
 [out] Указатель на `mdFile` маркера или `mdAssemblyRef` маркер, который представляет файл или сборку, соответственно, содержащий ресурс.  
  
 `pdwOffset`  
 [out] Указатель на значение, задающее смещение для начала ресурсов в файле.  
  
 `pdwResourceFlags`  
 [out] Указатель флаги, описывающие метаданные, применяемые к ресурсу. Значение флагов представляет собой сочетание одного или нескольких [CorManifestResourceFlags](../../../../docs/framework/unmanaged-api/metadata/cormanifestresourceflags-enumeration.md) значения.  
  
## <a name="requirements"></a>Требования  
 **Платформы:** разделе [требования к системе для](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок:** Cor.h  
  
 **Библиотека:** используется как ресурс в MsCorEE.dll  
  
 **Версии платформы .NET framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>См. также  
 [Интерфейс IMetaDataAssemblyImport](../../../../docs/framework/unmanaged-api/metadata/imetadataassemblyimport-interface.md)
