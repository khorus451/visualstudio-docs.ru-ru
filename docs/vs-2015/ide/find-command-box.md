---
title: Поле "Найти/Команда" | Документы Майкрософт
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.findcommandbox
helpviewer_keywords:
- Find/Command box
ms.assetid: c81736dd-7a26-4e11-95c8-c2a2e56d7a41
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b7c5f9c19573a04b1d9a8d7b8c6e9450aef9bc44
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ru-RU
ms.lasthandoff: 10/19/2019
ms.locfileid: "72645734"
---
# <a name="findcommand-box"></a>Поиск/Команда - окно
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

В поле **Найти/Команда** можно искать текст и выполнять команды Visual Studio. Поле **Найти/Команда** по-прежнему доступно как элемент управления панели инструментов, но больше не отображается по умолчанию. Поле **Найти/Команда** можно отобразить, выбрав на **стандартной** панели инструментов команду **Добавить или удалить кнопки** и щелкнув **Найти**.

 Чтобы выполнить команду [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], введите перед ней знак "больше, чем" (>).

 В поле **Найти/Команда** сохраняются последние 20 введенных элементов, которые выводятся в раскрывающемся списке. Перемещаться по списку можно с помощью клавиш со стрелками.

 ![Поле&#47;"команда поиска"](../ide/media/findcommandbox.png "|::ref1::|") Поле "Поиск/команда"

## <a name="searching-for-text"></a>Поиск текста
 После ввода текста в поле **Найти/Команда** и нажатии клавиши ВВОД среда Visual Studio по умолчанию выполняет поиск в текущем документе или окне инструментов с использованием параметров, указанных в диалоговом окне **Поиск в файлах**. Для получения дополнительной информации см. [Finding and Replacing Text](../ide/finding-and-replacing-text.md).

## <a name="entering-commands"></a>Ввод команд
 Чтобы с помощью поля **Найти/Команда** выполнить отдельную команду или псевдоним [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], а не поиск текста, введите команду [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], указав перед ней знак "больше, чем" (>). Например:

```
>File.NewFile c:\temp\MyFile /t:"General\Text File"
```

 Кроме того, для ввода и выполнения отдельных или нескольких команд можно использовать окно "Команда". Некоторые команды и псевдонимы можно вводить и выполнять сами по себе, в то время как синтаксис других включает обязательные аргументы. Список команд с аргументами см. в разделе [Команды Visual Studio](../ide/reference/visual-studio-commands.md).

## <a name="escape-characters"></a>Escape-символы
 Символ "крышки" (^) в командной строке означает, что следующий за ним символ интерпретируется буквально, а не как управляющий символ. Благодаря этому в значение параметра можно внедрить прямые кавычки ("), пробелы, начальные символы косой черты, крышки или другие знаки, за исключением имен параметров. Например, примененная к объекту директива

```
>Edit.Find ^^t /regex
```

 Крышка действует одинаково как внутри кавычек, так и за их пределами. Если крышка является последним символом в строке, она игнорируется.

## <a name="see-also"></a>См. также
 [Окно команд](../ide/reference/command-window.md) для [поиска и замены текста](../ide/finding-and-replacing-text.md)
