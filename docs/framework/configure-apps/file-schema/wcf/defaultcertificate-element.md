---
title: Элемент &lt;defaultCertificate&gt;
ms.date: 03/30/2017
ms.assetid: f1ddf364-9a00-45d3-b989-ff381c154ce6
ms.openlocfilehash: a4af1c6ec452b24634fa50162fa71f069e2451f5
ms.sourcegitcommit: 11f11ca6cefe555972b3a5c99729d1a7523d8f50
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
ms.locfileid: "32751016"
---
# <a name="ltdefaultcertificategt-element"></a>Элемент &lt;defaultCertificate&gt;
Задает сертификат X.509 для использования, когда служба или служба маркеров безопасности не предоставляет сертификат посредством протокола согласования.  
  
 \<система. ServiceModel >  
\<поведения >  
раздел endpointBehaviors  
\<поведение >  
\<clientCredentials >  
\<serviceCertificate >  
\<defaultCertificate >  
  
## <a name="syntax"></a>Синтаксис  
  
```xml  
<defaultCertificate findValue="String"   
storeLocation=" CurrentUser/LocalMachine"  
storeName="AddressBook/AuthRoot/CertificateAuthority/Disallowed/My/Root/TrustedPeople/TrustedPublisher"   
x509FindType="FindByThumbPrint/FindBySubjectName/FindBySubjectDistinguishedName/FindByIssuerName/FindByIssuerDistinguishedName/FindBySerialiNumber/FindByTimeValid/FindByTimeNotYetValid/FindByTimeExpired/FindByTemplateName/FindByApplicationPolicy/FindByCertificatePolicy/FindByExtension/FindByKeyUsage/FindBySubjectKeyIdentifier" />  
```  
  
## <a name="attributes-and-elements"></a>Атрибуты и элементы  
 В следующих разделах описываются атрибуты, дочерние и родительские элементы.  
  
### <a name="attributes"></a>Атрибуты  
  
|Атрибут|Описание|  
|---------------|-----------------|  
|findValue|Строка. Значение, которое нужно найти.|  
|x509FindType|Перечисление. Одно из полей сертификата, где следует проводить поиск.|  
|storeLocation|Перечисление. Одно из двух системных расположений хранилища, где следует проводить поиск.|  
|storeName|Перечисление. Одно из системных хранилищ, где следует проводить поиск.|  
  
## <a name="findvalue-attribute"></a>Атрибут findValue  
  
|Значение|Описание|  
|-----------|-----------------|  
|Строковое|Значение зависит от поля (заданного атрибутом x509FindType), поиск которого выполняется. Например, при поиске отпечатка значение должно быть строкой шестнадцатеричных чисел.|  
  
## <a name="x509findtype-attribute"></a>Атрибут x509FindType  
  
|Значение|Описание|  
|-----------|-----------------|  
|Перечисление|К числу значений относятся следующие: FindByThumbprint, FindBySubjectName, FindBySubjectDistinguishedName, FindByIssuerName, FindByIssuerDistinguishedName, FindBySerialNumber, FindByTimeValid, FindByTimeNotYetValid, FindBySerialNumber, FindByTimeExpired, FindByTemplateName, FindByApplicationPolicy, FindByCertificatePolicy, FindByExtension, FindByKeyUsage, FindBySubjectKeyIdentifier.|  
  
## <a name="storelocation-attribute"></a>Атрибут storeLocation  
  
|Значение|Описание|  
|-----------|-----------------|  
|Перечисление|CurrentUser или LocalMachine.|  
  
## <a name="storename-attribute"></a>Атрибут storeName  
  
|Значение|Описание|  
|-----------|-----------------|  
|Перечисление|К числу значений относятся следующие: AddressBook, AuthRoot, CertificateAuthority, Disallowed, My, Root, TrustedPeople и TrustedPublisher.|  
  
### <a name="child-elements"></a>Дочерние элементы  
 Отсутствует.  
  
### <a name="parent-elements"></a>Родительские элементы  
  
|Элемент|Описание|  
|-------------|-----------------|  
|[\<serviceCertificate >](../../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-clientcredentials-element.md)|Задает сертификат для использования при проверке подлинности службы для клиента.|  
  
## <a name="remarks"></a>Примечания  
 Для привязок, использующих безопасность сообщений на основе сертификатов, сертификат, заданный этим элементом конфигурации, используется для шифрования сообщений службе; предполагается также, что он будет использоваться службой для подписи ответов клиенту. Он сохраняет один сертификат для использования при отсутствии сертификата, заданного службой сертификата.  
  
## <a name="example"></a>Пример  
 В следующем примере задается сертификат для конечных точек, чей URI начинается с http://www.contoso.com и сертификат для использования для всех конечных точек, не выполняющих согласование сертификатов.  
  
```xml  
<serviceCertificate>  
  <defaultCertificate findValue="www.contoso.com"   
                      storeLocation="LocalMachine"  
                      storeName="TrustedPeople"   
                      x509FindType="FindByIssuerDistinguishedName" />  
  <scopedCertificates>  
     <add targetUri="http://www.contoso.com"   
          findValue="www.contoso.com" storeLocation="LocalMachine"  
                  storeName="Root" x509FindType="FindByIssuerName" />  
  </scopedCertificates>  
  <authentication revocationMode="Online"   
   trustedStoreLocation="LocalMachine" />  
</serviceCertificate>  
```  
  
## <a name="see-also"></a>См. также  
 <xref:System.ServiceModel.Configuration.X509DefaultServiceCertificateElement>  
 <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential>  
 <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential.DefaultCertificate%2A>  
 [Работа с сертификатами](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md)  
 [\<Проверка подлинности >](../../../../../docs/framework/configure-apps/file-schema/wcf/authentication-of-clientcertificate-element.md)  
 [Защита клиентов](../../../../../docs/framework/wcf/securing-clients.md)  
 [Защита служб и клиентов](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)
