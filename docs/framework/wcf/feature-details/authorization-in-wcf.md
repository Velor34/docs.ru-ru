---
title: Авторизация в WCF
ms.date: 03/30/2017
helpviewer_keywords:
- authorization [WCF]
- security [WCF], authorization
ms.assetid: 8ea0b552-af65-45b0-a157-c6c111b8ce5e
ms.openlocfilehash: 8e7632dda1a1bd2b60b71c385ad58c23e4207534
ms.sourcegitcommit: 3c1c3ba79895335ff3737934e39372555ca7d6d0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/05/2018
ms.locfileid: "43749584"
---
# <a name="authorization-in-wcf"></a>Авторизация в WCF
Авторизация - процесс управления доступом и правами на ресурсы, например службы и файлы. В подразделах этого раздела показано, как выполнять эту основную задачу в Windows Communication Foundation (WCF) в различными способами.  
  
## <a name="in-this-section"></a>В этом разделе  
 [Механизмы управления доступом](../../../../docs/framework/wcf/feature-details/access-control-mechanisms.md)  
 Содержит краткий обзор механизмов авторизации в WCF и предлагаемые используется.  
  
 [Практическое руководство. Ограничение доступа с использованием класса PrincipalPermissionAttribute](../../../../docs/framework/wcf/how-to-restrict-access-with-the-principalpermissionattribute-class.md)  
 Показывает процесс ограничения доступа к сервису с помощью класса <xref:System.Security.Permissions.PrincipalPermissionAttribute>.  
  
 [Практическое руководство. Использование поставщика ролей ASP.NET со службой](../../../../docs/framework/wcf/feature-details/how-to-use-the-aspnet-role-provider-with-a-service.md)  
 Пошаговое руководство по конфигурации службы, в котором рассказывается, как разрешить ей использовать функцию поставщика ролей инфраструктуры [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)].  
  
 [Практическое руководство. Использование поставщика ролей диспетчера авторизации ASP.NET со службой](../../../../docs/framework/wcf/feature-details/how-to-use-the-aspnet-authorization-manager-role-provider-with-a-service.md)  
 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] может использовать диспетчер авторизации для управления авторизацией на веб-сайте. WCF аналогичным образом можно использовать [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]комбинацию диспетчера /Authorization для авторизации клиентов.  
  
 [Управление утверждениями и авторизацией с помощью модели удостоверения](../../../../docs/framework/wcf/feature-details/managing-claims-and-authorization-with-the-identity-model.md)  
 Объясняет основы использования инфраструктуры модели удостоверения для механизма авторизации на основе утверждений.  
  
 [Делегирование и олицетворение](../../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md)  
 Объясняет разницу между делегированием и олицетворением.  
  
## <a name="reference"></a>Ссылка  
 <xref:System.ServiceModel.Security>  
  
 <xref:System.ServiceModel.Description.PrincipalPermissionMode>  
  
 <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior>  
  
 <xref:System.Security.Permissions.PrincipalPermissionAttribute>  
  
## <a name="related-sections"></a>Связанные разделы  
 [Проверка подлинности](../../../../docs/framework/wcf/feature-details/authentication-in-wcf.md)  
  
## <a name="see-also"></a>См. также  
 [Общие сведения о безопасности](../../../../docs/framework/wcf/feature-details/security-overview.md)  
 [Модель безопасности для Windows Server App Fabric](https://go.microsoft.com/fwlink/?LinkID=201279&clcid=0x409)
