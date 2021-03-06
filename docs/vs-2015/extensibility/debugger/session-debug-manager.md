---
title: Сеанс отладки Manager | Документация Майкрософт
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- session debug manager, unifying session views
- session debug manager, broadcasting
- debugging [Debugging SDK], session debug manager
- session debug manager
- session debug manager, debug engine multiplexing
- session debug manager, delegating
ms.assetid: fbb1928d-dddc-43d1-98a4-e23b0ecbae09
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9fd7c7555c19f850a15161f6fba00b1184621a9e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "68157824"
---
# <a name="session-debug-manager"></a>Диспетчер отладки сеансов
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Диспетчер отладки сеансов (SDM) управляет любое количество отладчиков (DE) отладка любое количество программ в нескольких процессах на любое число компьютеров. Кроме того, что отладчик мультиплексор, SDM обеспечивает единое представление сеанс отладки в интегрированную среду разработки.  
  
## <a name="session-debug-manager-operation"></a>Операция диспетчера сеанса отладки  
 Диспетчер отладки сеансов (SDM) управляет DE. Возможно, более одного модуля отладки, работающим на этом компьютере, в то же время. Чтобы мультиплексировать DEs, SDM целый ряд интерфейсов из DEs заключает в оболочку и предоставляет их в интегрированную среду разработки, как единый интерфейс.  
  
 В целях повышения производительности некоторые интерфейсы не мультиплексируются. Вместо этого они используются непосредственно из DE и вызовы этих интерфейсов не проходят через SDM. Например интерфейсы, используемые с памятью, кода и контекстов документа не мультиплексируются, поскольку они ссылаются на конкретные инструкции, памяти или документа в указанной программы отладки программы с определенной DE. Нет других DE должны заняться на данном уровне взаимодействия.  
  
 Это справедливо не для всех контекстов. Вызовы к интерфейсу контекст оценки выражения, проходить через SDM. Во время вычисления выражения, обертывает SDM [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) интерфейсом, предоставляющим в интегрированную среду разработки, так как при вычислении этого выражения, оно может включать несколько DEs, при отладке программ, в том же процессе, который может быть выполняется на том же потоке.  
  
 Обычно SDM выступает в качестве механизм делегирования, но он может выступать в качестве широковещательных механизма. Например во время вычисления выражения, SDM выступает в качестве механизме оповещения для уведомления о всех DEs, что они могут выполнять код для указанного потока. Аналогичным образом когда SDM получает событие stopping, он осуществляет широковещательную передачу все программы, что их следует прекратить выполнение. При вызове шаг SDM осуществляет широковещательную передачу все программы, можно по-прежнему работает. Точки останова также передаются каждые DE.  
  
 SDM не отслеживает текущую программу, потока или кадра стека. Процесс, программу и поток информация отправляется SDM вместе с конкретными событиями отладки.  
  
## <a name="see-also"></a>См. также  
 [Отладка ядра](../../extensibility/debugger/debug-engine.md)   
 [Компоненты отладчика](../../extensibility/debugger/debugger-components.md)   
 [Контексты отладчика](../../extensibility/debugger/debugger-contexts.md)
