---
title: Метод ICorProfilerInfo::GetObjectSize
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.GetObjectSize
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::GetObjectSize
helpviewer_keywords:
- GetObjectSize method [.NET Framework profiling]
- ICorProfilerInfo::GetObjectSize method [.NET Framework profiling]
ms.assetid: 9f02e763-73f7-42cb-a41c-f78499d9482c
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 7ed27602dfa9090b46b842e4e65af8af373cc207
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
ms.locfileid: "33453913"
---
# <a name="icorprofilerinfogetobjectsize-method"></a>Метод ICorProfilerInfo::GetObjectSize
Возвращает размер указанного объекта.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
HRESULT GetObjectSize(  
    [in]  ObjectID objectId,  
    [out] ULONG  *pcSize);  
```  
  
#### <a name="parameters"></a>Параметры  
 `objectId`  
 [in] Идентификатор объекта.  
  
 `pcSize`  
 [out] Указатель на размер объекта в байтах.  
  
## <a name="remarks"></a>Примечания  
  
> [!IMPORTANT]
>  Этот метод устарел. Он возвращает COR_E_OVERFLOW для объектов более 4 ГБ на 64-разрядных платформах. Используйте [ICorProfilerInfo4::GetObjectSize2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-getobjectsize2-method.md) метод вместо него.  
  
 Разные объекты одного типа часто имеют одинаковый размер. Однако некоторые типы, например массивов или строк, могут иметь другого размера для каждого объекта.  
  
 Размер, возвращаемый `GetObjectSize` метода не включает заполнения выравнивание, может появиться после объекта в куче сбора мусора. Если вы используете `GetObjectSize` метод перемещаться от объекта к объекту в куче сбора мусора, добавлять заполнение вручную, при необходимости выравнивания.  
  
-   На 32-разрядной версии Windows, COR_PRF_GC_GEN_0, COR_PRF_GC_GEN_1 и COR_PRF_GC_GEN_2 используется 4-байтовое выравнивание, а COR_PRF_GC_LARGE_OBJECT_HEAP 8-байтового выравнивания.  
  
-   На 64-разрядной версии Windows выравнивание всегда равно 8 байт.  
  
## <a name="requirements"></a>Требования  
 **Платформы:** разделе [требования к системе для](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок:** CorProf.idl, CorProf.h  
  
 **Библиотека:** CorGuids.lib  
  
 **Версии платформы .NET framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>См. также  
 [Интерфейс ICorProfilerInfo](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)
