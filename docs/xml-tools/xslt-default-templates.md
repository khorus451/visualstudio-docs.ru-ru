---
title: XSLT-шаблоны по умолчанию
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 773dd34e-67d3-4997-8df9-b71e7f880d88
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0f3a6e6391e3c76a43a94e5cf77c819a2f4b18c6
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592299"
---
# <a name="xslt-default-templates"></a>Шаблоны XSLT по умолчанию

Если в таблице стилей отсутствует совпадающее явное правило шаблона, то во время обработки XSLT используется шаблон по умолчанию. Шаблон по умолчанию, называемый также встроенным правилом шаблона, определен в разделе  5.8 спецификации W3C XSLT 1.0. Шаблон по умолчанию разрешает обработчику XSLT обрабатывать узел, даже если ему не соответствует ни одно явное правило шаблона. Однако, поскольку встроенное правило шаблона явно не определено в таблице стилей, это может привести к непредвиденным или сбивающим с толку результатам XSLT-преобразования.

Отладчик XSLT теперь отображает код XSLT-шаблонов по умолчанию. При пошаговом выполнении XSLT-преобразования отладчик отображает в окне шаблон по умолчанию, если используется шаблон по умолчанию. Это позволяет выполнять по шагам код и задавать точки останова на инструкциях кода.

## <a name="see-also"></a>См. также:

- [Отладка XSLT](../xml-tools/debugging-xslt.md)
