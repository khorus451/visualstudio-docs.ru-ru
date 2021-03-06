---
title: Добавление расширений в определения DSL | Документация Майкрософт
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 07e133be-92ab-4936-a02b-45d2012bd0a6
caps.latest.revision: 8
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 5fab56a7738ed7b52760cf20a5bfcc8542ee5a23
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/13/2020
ms.locfileid: "75919062"
---
# <a name="adding-extensions-to-dsl-definitions"></a>Добавление расширений в определения доменных языков
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Расширение определения DSL позволяет создать пакет расширений для доменного языка (DSL). Расширение DSL, которое содержится в расширении интеграции Visual Studio (VSIX), может быть установлено на компьютере пользователя точно так же, как и DSL. Дополнительные функции могут динамически включаться и отключаться во время выполнения. Доменный язык не обязательно должен быть специально спроектирован для расширения, а расширения могут быть созданы позже или сторонними производителями без изменения расширенного DSL.

 К дополнительным функциям могут относиться следующие:

- Свойства элементов Model и Presentation

- Декораторы для фигур и соединителей

- Классы, связи, фигуры и соединители

- Ограничения проверки

- Элементы и вкладки панели элементов

  Пользователь расширенного DSL может создать и сохранить модель, содержащую экземпляры дополнительных компонентов, и они могут быть прочитаны другими пользователями, которые установили соответствующее расширение. Пользователи, которые не установили расширение, не могут использовать дополнительные функции, но могут обновлять и сохранять модель без потери дополнительных функций.

  Пример кода и дополнительные сведения об этой функции см. на веб-сайте [SDK визуализации и моделирования Visual Studio](https://www.microsoft.com/en-us/download/details.aspx?id=48148) .

## <a name="see-also"></a>См. также раздел
 [Пакет SDK визуализации и моделирования Visual Studio](https://www.microsoft.com/en-us/download/details.aspx?id=48148)
