---
title: -DebugExe (devenv.exe) | Документы Майкрософт
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- Devenv, /DebugExe switch
- DebugExe switch
- /DebugExe [devenv.exe]
ms.assetid: cd700006-1648-418f-924b-4b1e5c1412ab
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f472add6b821693d1d48397e878db19e707e2868
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ru-RU
ms.lasthandoff: 10/19/2019
ms.locfileid: "72660808"
---
# <a name="debugexe-devenvexe"></a>/DebugExe (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Открывает указанный исполняемый файл для отладки.

## <a name="syntax"></a>Синтаксис

```
Devenv /debugexe ExecutableFile
```

## <a name="arguments"></a>Аргументы
 `ExecutableFile` Обязательный. Путь и имя EXE-файла.

 Если EXE-файл не найден или не существует, никакие предупреждения или ошибки не выводятся, а [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] запускается обычным образом.

## <a name="remarks"></a>Примечания
 Строки, следующие за параметром `ExecutableFile`, передаются в этот файл в качестве аргументов.

## <a name="example"></a>Пример
 Следующий пример открывает файл `MyApplication.exe` для отладки.

```
Devenv.exe /debugexe MyApplication.exe
```

## <a name="see-also"></a>См. также
 [Параметры командной строки для команды Devenv](../../ide/reference/devenv-command-line-switches.md)
