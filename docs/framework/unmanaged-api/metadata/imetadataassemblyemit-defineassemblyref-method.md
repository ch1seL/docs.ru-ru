---
title: "Метод IMetaDataAssemblyEmit::DefineAssemblyRef"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IMetaDataAssemblyEmit.DefineAssemblyRef
api_location: mscoree.dll
api_type: COM
f1_keywords: IMetaDataAssemblyEmit::DefineAssemblyRef
helpviewer_keywords:
- DefineAssemblyRef method [.NET Framework metadata]
- IMetaDataAssemblyEmit::DefineAssemblyRef method [.NET Framework metadata]
ms.assetid: 0b284b18-0084-4b3a-912a-5ebe9f29c88b
topic_type: apiref
caps.latest.revision: "17"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 074e589b84e21de4ec3bcc3c54a865297587d383
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/18/2017
---
# <a name="imetadataassemblyemitdefineassemblyref-method"></a><span data-ttu-id="8c982-102">Метод IMetaDataAssemblyEmit::DefineAssemblyRef</span><span class="sxs-lookup"><span data-stu-id="8c982-102">IMetaDataAssemblyEmit::DefineAssemblyRef Method</span></span>
<span data-ttu-id="8c982-103">Создает структуру `AssemblyRef`, содержащую метаданные для сборки, на которую ссылается данная сборка, и возвращает связанный токен метаданных.</span><span class="sxs-lookup"><span data-stu-id="8c982-103">Creates an `AssemblyRef` structure containing metadata for the assembly that this assembly references, and returns the associated metadata token.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="8c982-104">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="8c982-104">Syntax</span></span>  
  
```  
HRESULT DefineAssemblyRef (  
    [in]  void                *pbPublicKeyOrToken,  
    [in]  ULONG               cbPublicKeyOrToken,  
    [in]  LPCWSTR             szName,  
    [in]  ASSEMBLYMETADATA    pMetaData,  
    [in]  void                *pbHashValue,  
    [in]  ULONG               cbHashValue,  
    [in]  DWORD               dwAssemblyRefFlags,  
    [out] mdAssemblyRef       *pmdar  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="8c982-105">Параметры</span><span class="sxs-lookup"><span data-stu-id="8c982-105">Parameters</span></span>  
 `pbPublicKeyOrToken`  
 <span data-ttu-id="8c982-106">[in] Открытый ключ издателя по ссылке сборки.</span><span class="sxs-lookup"><span data-stu-id="8c982-106">[in] The public key of the publisher of the referenced assembly.</span></span> <span data-ttu-id="8c982-107">Вспомогательная функция [StrongNameTokenFromAssembly](../../../../docs/framework/unmanaged-api/strong-naming/strongnametokenfromassembly-function.md) может использоваться для получения хэша открытого ключа, передаваемый в качестве этого параметра.</span><span class="sxs-lookup"><span data-stu-id="8c982-107">The helper function [StrongNameTokenFromAssembly](../../../../docs/framework/unmanaged-api/strong-naming/strongnametokenfromassembly-function.md) can be used to get the hash of the public key to pass as this parameter.</span></span>  
  
 `cbPublicKeyOrToken`  
 <span data-ttu-id="8c982-108">[in] Размер в байтах `pbPublicKeyOrToken`.</span><span class="sxs-lookup"><span data-stu-id="8c982-108">[in] The size in bytes of `pbPublicKeyOrToken`.</span></span>  
  
 `szName`  
 <span data-ttu-id="8c982-109">[in] Понятное текстовое имя сборки.</span><span class="sxs-lookup"><span data-stu-id="8c982-109">[in] The human-readable text name of the assembly.</span></span> <span data-ttu-id="8c982-110">Это значение не должно превышать 1024 символа.</span><span class="sxs-lookup"><span data-stu-id="8c982-110">This value must not exceed 1024 characters.</span></span>  
  
 `pMetaData`  
 <span data-ttu-id="8c982-111">[in] ASSEMBLYMETADATA экземпляр, который содержит сведения о версии, платформы и языка сборки.</span><span class="sxs-lookup"><span data-stu-id="8c982-111">[in] An ASSEMBLYMETADATA instance that contains the version, platform and locale information of the referenced assembly.</span></span>  
  
 `pbHashValue`  
 <span data-ttu-id="8c982-112">[in] Хэш данных, связанные со сборкой, на которую указывает ссылка.</span><span class="sxs-lookup"><span data-stu-id="8c982-112">[in] The hash data associated with the referenced assembly.</span></span> <span data-ttu-id="8c982-113">Необязательно.</span><span class="sxs-lookup"><span data-stu-id="8c982-113">Optional.</span></span>  
  
 `cbHashValue`  
 <span data-ttu-id="8c982-114">[in] Размер в байтах `pbHashValue`.</span><span class="sxs-lookup"><span data-stu-id="8c982-114">[in] The size in bytes of `pbHashValue`.</span></span>  
  
 `dwAssemblyRefFlags`  
 <span data-ttu-id="8c982-115">[in] Побитовое сочетание [CorAssemblyFlags](../../../../docs/framework/unmanaged-api/metadata/corassemblyflags-enumeration.md) значения, которые влияют на поведение механизма выполнения сборки.</span><span class="sxs-lookup"><span data-stu-id="8c982-115">[in] A bitwise combination of [CorAssemblyFlags](../../../../docs/framework/unmanaged-api/metadata/corassemblyflags-enumeration.md) values that influence the behavior of the execution engine.</span></span>  
  
 `pmdar`  
 <span data-ttu-id="8c982-116">[out] Указатель на возвращаемый `AssemblyRef` токен метаданных.</span><span class="sxs-lookup"><span data-stu-id="8c982-116">[out] A pointer to the returned `AssemblyRef` metadata token.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="8c982-117">Примечания</span><span class="sxs-lookup"><span data-stu-id="8c982-117">Remarks</span></span>  
 <span data-ttu-id="8c982-118">Один `AssemblyRef` структуру метаданных должны быть определены для каждой сборки, на которую ссылается данная сборка.</span><span class="sxs-lookup"><span data-stu-id="8c982-118">One `AssemblyRef` metadata structure must be defined for each assembly that this assembly references.</span></span>  
  
 <span data-ttu-id="8c982-119">Во время выполнения передаются сведения о связанной сборке распознаватель сборок с указанием, что они представляют информацию «в процессе построения».</span><span class="sxs-lookup"><span data-stu-id="8c982-119">At run time, the details of a referenced assembly are passed to the assembly resolver with an indication that they represent the "as built" information.</span></span> <span data-ttu-id="8c982-120">Затем распознаватель сборок применяет политику.</span><span class="sxs-lookup"><span data-stu-id="8c982-120">The assembly resolver then applies policy.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="8c982-121">Требования</span><span class="sxs-lookup"><span data-stu-id="8c982-121">Requirements</span></span>  
 <span data-ttu-id="8c982-122">**Платформы:** разделе [требования к системе для](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="8c982-122">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="8c982-123">**Заголовок:** Cor.h</span><span class="sxs-lookup"><span data-stu-id="8c982-123">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="8c982-124">**Библиотека:** используется как ресурс в MsCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="8c982-124">**Library:** Used as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="8c982-125">**Версии платформы .NET framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="8c982-125">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="8c982-126">См. также</span><span class="sxs-lookup"><span data-stu-id="8c982-126">See Also</span></span>  
 [<span data-ttu-id="8c982-127">Интерфейс IMetaDataAssemblyEmit</span><span class="sxs-lookup"><span data-stu-id="8c982-127">IMetaDataAssemblyEmit Interface</span></span>](../../../../docs/framework/unmanaged-api/metadata/imetadataassemblyemit-interface.md)