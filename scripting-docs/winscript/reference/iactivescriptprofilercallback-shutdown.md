---
title: 'IActiveScriptProfilerCallback:: Shutdown | Документация Майкрософт'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptProfilerCallback.Shutdown
apilocation:
- scrobj.dll
ms.assetid: 1281bf3c-d7d8-4ff5-9d8a-d1761fdb262e
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: deecfe4134a4b0e18591823f194ceaf6d1eb0a14
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571644"
---
# <a name="iactivescriptprofilercallbackshutdown"></a>IActiveScriptProfilerCallback::Shutdown
Вызывается для оповещения объекта профилировщика при остановке профилирования в обработчике скриптов. Таким образом, объект профилировщика может вызывать свои подпрограммы очистки, если это необходимо. Этот метод также вызывается обработчиком скриптов при завершении работы обработчика скриптов или при сбое вызова [IActiveScriptProfilerCallback:: Initialize](../../winscript/reference/iactivescriptprofilercallback-initialize.md) .  
  
## <a name="syntax"></a>Синтаксис  
  
```cpp
HRESULT Shutdown(  
    [in] HRESULT hrReason);  
```  
  
#### <a name="parameters"></a>Параметры  
 `hrReason`  
 окне Причина завершения работы. Если обработчик скриптов завершает работу, `S_OK` передается. Если вызов [IActiveScriptProfilerCallback:: Initialize](../../winscript/reference/iactivescriptprofilercallback-initialize.md) ВОЗВРАЩАЕТ ошибку HRESULT, передается значение HRESULT. В противном случае это значение извлекается из [IActiveScriptProfilerControl:: стоппрофилинг](../../winscript/reference/iactivescriptprofilercontrol-stopprofiling.md).  
  
## <a name="return-value"></a>Возвращаемое значение  
 Возвращаемое значение этого метода игнорируется обработчиком скриптов.  
  
## <a name="see-also"></a>См. также  
 [Интерфейс IActiveScriptProfilerCallback](../../winscript/reference/iactivescriptprofilercallback-interface.md)