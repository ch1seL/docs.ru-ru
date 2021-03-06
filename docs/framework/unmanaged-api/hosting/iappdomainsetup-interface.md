---
title: Интерфейс IAppDomainSetup
ms.date: 03/30/2017
api_name:
- IAppDomainSetup
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IAppDomainSetup
helpviewer_keywords:
- IAppDomainSetup interface [.NET Framework hosting]
ms.assetid: 1844da85-c031-40bf-bea4-1a3d12a36c8c
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: cbcbc446eabcfcbc28c830f8860bde726c8eb6e3
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
ms.locfileid: "33434772"
---
# <a name="iappdomainsetup-interface"></a>Интерфейс IAppDomainSetup
Предоставляет свойства, позволяющие настроить узел <xref:System.AppDomain?displayProperty=nameWithType> тип перед вызовом [ICorRuntimeHost::CreateDomainEx](../../../../docs/framework/unmanaged-api/hosting/icorruntimehost-createdomainex-method.md) метод для его создания.  
  
## <a name="properties"></a>Свойства  
  
|Свойство|Описание|  
|--------------|-----------------|  
|<xref:System.AppDomainSetup.ApplicationBase%2A>|Возвращает или задает имя каталога, содержащего приложение.|  
|<xref:System.AppDomainSetup.ApplicationName%2A>|Возвращает или задает имя приложения.|  
|<xref:System.AppDomainSetup.CachePath%2A>|Возвращает или задает имя области конкретных приложению где создаются теневые копии файлов.|  
|<xref:System.AppDomainSetup.ConfigurationFile%2A>|Возвращает или задает имя файла конфигурации для приложения.|  
|<xref:System.AppDomainSetup.DynamicBase%2A>|Возвращает или задает имя каталога, где сохраняются и становятся доступными динамически созданные файлы.|  
|<xref:System.AppDomainSetup.LicenseFile%2A>|Возвращает или задает путь к файлу лицензии, связанного с этим доменом.|  
|<xref:System.AppDomainSetup.PrivateBinPath%2A>|Возвращает или задает список каталогов, в сочетании с <xref:System.AppDomainSetup.ApplicationBase%2A> directory, чтобы производить поиск закрытых сборок.|  
|<xref:System.AppDomainSetup.PrivateBinPathProbe%2A>|Возвращает или задает строковое значение, которое включает или исключает <xref:System.AppDomainSetup.ApplicationBase%2A> из пути поиска для приложения.|  
|<xref:System.AppDomainSetup.ShadowCopyDirectories%2A>|Возвращает или задает имена каталогов, содержащих сборки, подлежащие теневому копированию.|  
|<xref:System.AppDomainSetup.ShadowCopyFiles%2A>|Возвращает или задает строку, позволяющую определить, включено ли теневое копирование. Допустимыми значениями являются «true» или «false».|  
  
## <a name="remarks"></a>Примечания  
 `IAppDomainSetup` Соответствующий интерфейс в управляемом <xref:System.IAppDomainSetup> интерфейс, который <xref:System.AppDomainSetup> тип реализует. В разделе <xref:System.IAppDomainSetup?displayProperty=nameWithType> подробные описания его свойств.  
  
 `IAppDomainSetup` Представляет сведения о привязке сборок, которые могут добавляться в <xref:System.AppDomain> экземпляра до его создания. Например, хост может устанавливать <xref:System.AppDomainSetup.ApplicationBase%2A> свойства, чтобы установить корневой каталог, общеязыковой среды выполнения (CLR) проверяет наличие управляемых сборок.  
  
## <a name="requirements"></a>Требования  
 **Платформы:** разделе [требования к системе для](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок:** MSCorEE.h  
  
 **Библиотека:** включена как ресурс в MSCorEE.dll  
  
 **Версии платформы .NET framework:** [!INCLUDE[net_current_v11plus](../../../../includes/net-current-v11plus-md.md)]  
  
## <a name="see-also"></a>См. также  
 <xref:System.AppDomain>  
 <xref:System.AppDomainSetup>  
 <xref:System.IAppDomainSetup>  
 [Интерфейсы размещения](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
