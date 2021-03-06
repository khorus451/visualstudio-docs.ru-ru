---
title: Практическое руководство. Перемещение вверх или вниз по содержимому памяти | Документация Майкрософт
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- VB
- CSharp
- C++
helpviewer_keywords:
- debugger, paging up or down in memory
- memory, paging up or down
- Disassembly window, viewing memory space
- Memory window, paging up or down in memory
ms.assetid: 50b30a68-66f6-43f8-a48b-59ce12c95471
caps.latest.revision: 23
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: cc05772e6376dbe151d5ca71b9ee221e61a7be88
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "68157859"
---
# <a name="how-to-page-up-or-down-in-memory"></a>Практическое руководство. перемещение вверх или вниз по содержимому памяти
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

При просмотре содержимого памяти в окне **Память** или **Дизассемблированный код** для перемещения вверх и вниз по области памяти можно использовать вертикальную полосу прокрутки.  
  
### <a name="to-page-up-or-down-in-memory"></a>Перемещение вверх или вниз в области памяти  
  
1. Для перемещения на страницу вниз (к старшему адресу памяти) щелкните вертикальную полосу прокрутки ниже того места, где находится бегунок.  
  
2. Для перемещения на страницу вверх (к младшему адресу памяти) щелкните вертикальную полосу прокрутки выше того места, где находится бегунок.  
  
   Обратите внимание, что вертикальная полоса прокрутки работает не в стандартном режиме. Современные персональные компьютеры имеют огромное адресное пространство, поэтому в нем достаточно легко заблудиться, перетаскивая бегунок полосы прокрутки в произвольное расположение. По этой причине бегунок "подпружинен" и всегда остается в центре полосы прокрутки. В приложениях машинного кода можно постранично перемещаться вверх и вниз, однако нельзя свободно использовать полосу прокрутки.  
  
   В управляемых приложениях дизассемблирование ограничивается одной функцией и прокруткой можно пользоваться в обычном режиме.  
  
   Обратите внимание, что старшие адреса отображаются в нижней части окна. Для просмотра старших адресов следует перемещаться вниз, а не вверх.  
  
#### <a name="to-move-up-or-down-one-instruction"></a>Перемещение вверх или вниз на одну инструкцию  
  
- Щелкните стрелку, расположенную над или под вертикальной полосой прокрутки.  
  
## <a name="see-also"></a>См. также  
 [Окно памяти](../debugger/memory-windows.md)   
 [Практическое руководство. Использование окна дизассемблирования](../debugger/how-to-use-the-disassembly-window.md)   
 [Просмотр данных в отладчике](../debugger/viewing-data-in-the-debugger.md)
