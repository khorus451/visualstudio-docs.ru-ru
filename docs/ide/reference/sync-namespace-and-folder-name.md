---
title: Синхронизация пространства имен и имени папки
ms.date: 06/12/2019
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: d7073edaf6ecc261c58bf1e5607323b9214c5ed0
ms.sourcegitcommit: d4920babfc3d24a3fe1d4bf446ed3fe73b344467
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/17/2019
ms.locfileid: "67160760"
---
# <a name="sync-namespace-and-folder-name"></a>Синхронизация пространства имен и имени папки

Область применения этого рефакторинга:

- C#

**Что?** Синхронизация пространства имен и имени папки.

**Когда?** Вы хотите перепроектировать части решения, перетащив файл в новую папку. 

**Зачем?** Вы хотите убедиться, что ваше пространство имен соответствует вашей новой структуре папок.

## <a name="how-to"></a>Практические советы

1. Поместите курсор в имени пространства имен.
2. Нажмите клавиши **CTRL**+ **.** чтобы открыть меню **Быстрые действия и рефакторинг**.
3. Выберите **Изменить пространство имен на \<имя_папки>** .

   ![Синхронизация пространства имен и имени папки](media/sync-namespace-and-folder-name.png)

## <a name="see-also"></a>См. также

- [Рефакторинг](../refactoring-in-visual-studio.md)
