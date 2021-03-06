---
title: Как двунаправленные расширения
ms.date: 06/25/2017
ms.topic: conceptual
ms.assetid: 2d6cf53c-011e-4c9e-9935-417edca8c486
author: willbrown
ms.author: madsk
manager: justinclareburt
ms.workload:
- willbrown
ms.openlocfilehash: d6de945e7221d2239e1b4f00185a5b16c04b717d
ms.sourcegitcommit: e3c3d2b185b689c5e32ab4e595abc1ac60b6b9a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/18/2020
ms.locfileid: "76269066"
---
# <a name="how-to-make-extensions-compatible-with-visual-studio-20192017-and-visual-studio-2015"></a>Как сделать расширения совместимыми с Visual Studio 2019/2017 и Visual Studio 2015

В этом документе объясняется, как сделать проекты расширяемости циклическим обменом между Visual Studio 2015 и Visual Studio 2019 или Visual Studio 2017. После завершения этого обновления проект будет доступен для открытия, сборки, установки и запуска в Visual Studio 2015 и Visual Studio 2019 или 2017. В качестве справочной ссылки некоторые расширения, которые могут циклически переноситься между Visual Studio 2015 и Visual Studio 2019 или 2017, можно найти в [примерах расширяемости пакета SDK VS](https://github.com/Microsoft/VSSDK-Extensibility-Samples).

Если вы планируете выполнять сборку только в Visual Studio 2019/2017, но хотите, чтобы выходной VSIX выполнялся как в Visual Studio 2015, так и в Visual Studio 2019/2017, см. [документ по миграции расширений](how-to-migrate-extensibility-projects-to-visual-studio-2017.md).

> [!NOTE]
> Из-за изменений в Visual Studio между версиями некоторые элементы, которые работали в одной версии, не работают в другой. Убедитесь, что компоненты, к которым вы пытаетесь получить доступ, доступны в обеих версиях, или расширение будет иметь непредвиденные результаты.

Ниже приведена последовательность действий, которые вы закончите в этом документе, чтобы выполнить цикл обработки VSIX-файла:

1. Импортируйте правильные пакеты NuGet.
2. Обновить манифест расширения:
    * Целевой объект установки
    * Prerequisites
3. Обновление CSProj:
    * Обновите `<MinimumVisualStudioVersion>`.
    * Добавление свойства `<VsixType>`
    * Добавьте свойство отладки `($DevEnvDir)` 3 раза.
    * Добавьте условия для импорта средств и целевых объектов сборки.

4. Сборка и тестирование

## <a name="environment-setup"></a>Настройка среды

В этом документе предполагается, что на компьютере установлены следующие компоненты:

* Visual Studio 2015 с установленным пакетом SDK для VS
* Visual Studio 2019 или 2017 с установленной рабочей нагрузкой

## <a name="recommended-approach"></a>Рекомендуемый подход

Настоятельно рекомендуется запускать это обновление с помощью Visual Studio 2015, а не Visual Studio 2019 или 2017. Основным преимуществом разработки в Visual Studio 2015 является обеспечение ссылок на сборки, недоступные в Visual Studio 2015. При разработке в Visual Studio 2019 или 2017 существует риск, что вы можете ввести зависимость от сборки, которая существует только в Visual Studio 2019 или 2017.

## <a name="ensure-there-is-no-reference-to-projectjson"></a>Убедитесь, что ссылка на Project. JSON отсутствует.

Далее в этом документе мы будем вставлять операторы условного импорта в файл * *. csproj* . Это не сработает, если ссылки NuGet хранятся в *Project. JSON*. Поэтому рекомендуется переместить все ссылки NuGet в файл *Packages. config* .
Если проект содержит файл *Project. JSON* :

* Запишите ссылки в *Project. JSON*.
* Из **Обозреватель решений**удалите файл *Project. JSON* из проекта. Это приведет к удалению файла *Project. JSON* и его удалению из проекта.
* Добавьте ссылки NuGet обратно в проект:
  * Щелкните **решение** правой кнопкой мыши и выберите пункт **Управление пакетами NuGet для решения**.
  * Visual Studio автоматически создает файл *Packages. config* .

> [!NOTE]
> Если проект содержал пакеты EnvDTE, их может потребоваться добавить, щелкнув правой кнопкой мыши **ссылки** , выбрав **Добавить ссылку** и добавив соответствующую ссылку. Использование пакетов NuGet может привести к ошибкам при попытке выполнить сборку проекта.

## <a name="add-appropriate-build-tools"></a>Добавление соответствующих средств сборки

Необходимо добавить средства сборки, которые позволят вам выполнять сборку и отладку соответствующим образом. Корпорация Майкрософт создала сборку для этой сборки с именем Microsoft. VisualStudio. SDK. Буилдтаскс.

Чтобы создать и развернуть VSIXv3 в Visual Studio 2015 и 2019/2017, вам потребуется следующие пакеты NuGet:

{2&gt;Version&lt;2} | Встроенные средства
--- | ---
Visual Studio 2015 | Microsoft. VisualStudio. SDK. Буилдтаскс.,
Visual Studio 2019 или 2017 | Microsoft. VSSDK. Буилдтул

Для этого сделайте следующее:

* Добавьте в проект пакет NuGet Microsoft. VisualStudio. SDK. Буилдтаскс. ".
* Если проект не содержит Microsoft. VSSDK. BuildTools, добавьте его.
* Убедитесь, что версия Microsoft. VSSDK. BuildTools имеет значение 15. x или больше.

## <a name="update-extension-manifest"></a>Обновить манифест расширения

### <a name="1-installation-targets"></a>1. целевые объекты установки

Нам нужно сообщить Visual Studio, какие версии следует использовать для создания VSIX. Как правило, эти ссылки относятся либо к версии 14,0 (Visual Studio 2015), версии 15,0 (Visual Studio 2017), либо к версии 16,0 (Visual Studio 2019). В нашем случае мы хотим создать VSIX, который установит расширение для обоих версий, поэтому нам нужно выбрать обе версии. Если вы хотите, чтобы VSIX выполнил сборку и установку в версиях, предшествующих 14,0, это можно сделать, задав номер более ранней версии. Однако версии 10,0 и более ранних версий больше не поддерживаются.

* Откройте файл *source. extension. vsixmanifest* в Visual Studio.
* Откройте вкладку **установки конечных объектов** .
* Измените **диапазон версий** на [14,0, 17,0). "[" Указывает Visual Studio включить 14,0 и все версии после него. ")" Указывает Visual Studio включить все версии, но не включая версию 17,0.
* Сохраните все изменения и закройте все экземпляры Visual Studio.

![Образ целевых объектов установки](media/visual-studio-installation-targets-example.png)

### <a name="2-adding-prerequisites-to-the-extensionvsixmanifest-file"></a>2. Добавление необходимых компонентов в файл *Extension. vsixmanifest*

Для этого нам нужен редактор основных компонентов Visual Studio. Откройте Visual Studio и используйте обновленный конструктор манифеста, чтобы вставить необходимые компоненты.

Чтобы сделать это вручную:

* Перейдите в каталог проекта в проводнике.
* Откройте файл *Extension. vsixmanifest* в текстовом редакторе.
* Добавьте следующий тег:

```xml
<Prerequisites>
    <Prerequisite Id="Microsoft.VisualStudio.Component.CoreEditor" Version="[15.0,16.0)" DisplayName="Visual Studio core editor" />
</Prerequisites>
```

* Сохраните и закройте файл.

> [!NOTE]
> Вам может потребоваться изменить предварительную версию вручную, чтобы убедиться, что она совместима со всеми версиями Visual Studio 2019 или 2017. Это связано с тем, что конструктор вставит минимальную версию в качестве текущей версии Visual Studio (например, 15.0.26208.0). Однако, так как другие пользователи могут иметь более раннюю версию, вам потребуется вручную изменить это значение на 15,0.

На этом этапе файл манифеста должен выглядеть примерно так:

![Пример предварительных требований](media/visual-studio-prerequisites-example.png)

## <a name="modify-the-project-file-myprojectcsproj"></a>Изменение файла проекта (MyProject. csproj)

При выполнении этого шага настоятельно рекомендуется открыть измененный CSPROJ-объект. Несколько примеров можно найти [здесь](https://github.com/Microsoft/VSSDK-Extensibility-Samples). Выберите любой пример расширяемости, найдите *CSPROJ* файл и выполните следующие действия.

* Перейдите в каталог проекта в **проводнике**.
* Откройте файл *MyProject. csproj* в текстовом редакторе.

### <a name="1-update-the-minimumvisualstudioversion"></a>1. обновление Минимумвисуалстудиоверсион

* Установите минимальную версию Visual Studio для `$(VisualStudioVersion)` и добавьте в нее условный оператор. Добавьте эти теги, если они не существуют. Убедитесь, что теги заданы следующим образом:

```xml
<VisualStudioVersion Condition="'$(VisualStudioVersion)' == ''">14.0</VisualStudioVersion>
<MinimumVisualStudioVersion>$(VisualStudioVersion)</MinimumVisualStudioVersion>
```

### <a name="2-add-the-vsixtype-property"></a>2. Добавьте свойство Всикстипе.

* Добавьте следующий тег `<VsixType>v3</VsixType>` в группу свойств.

> [!NOTE]
> Рекомендуется добавить следующий тег `<OutputType></OutputType>`.

### <a name="3-add-the-debugging-properties"></a>3. Добавление свойств отладки

* Добавьте следующую группу свойств:

```xml
<PropertyGroup>
    <StartAction>Program</StartAction>
    <StartProgram>$(DevEnvDir)devenv.exe</StartProgram>
    <StartArguments>/rootsuffix Exp</StartArguments>
</PropertyGroup>
```

* Удалите все экземпляры следующего примера кода из файла *CSPROJ* и всех файлов *csproj. User* :

```xml
<StartAction>Program</StartAction>
<StartProgram>$(ProgramFiles)\Microsoft Visual Studio 14.0\Common7\IDE\devenv.exe</StartProgram>
<StartArguments>/rootsuffix Exp</StartArguments>
```

### <a name="4-add-conditions-to-the-build-tools-imports"></a>4. Добавление условий в импорт средств сборки

* Добавьте дополнительные условные операторы в теги `<import>`, которые содержат ссылку на Microsoft. VSSDK. BuildTools. Вставьте `'$(VisualStudioVersion)' != '14.0' And` в начале оператора условия. Эти инструкции будут отображаться в верхнем и нижнем колонтитулах файла CSPROJ.

Например:

```xml
<Import Project="packages\Microsoft.VSSDK.BuildTools.15.0.26201…" Condition="'$(VisualStudioVersion)' != '14.0' And Exists(…" />
```

* Добавьте дополнительные условные операторы в теги `<import>`, которые имеют Microsoft. VisualStudio. SDK. Буилдтаскс., Вставьте `'$(VisualStudioVersion)' == '14.0' And` в начале оператора условия. Эти инструкции будут отображаться в верхнем и нижнем колонтитулах файла CSPROJ.

Например:

```xml
<Import Project="packages\Microsoft.VisualStudio.Sdk.BuildTasks.14.0.14.0…" Condition="'$(VisualStudioVersion)' == '14.0' And Exists(…" />
```

* Добавьте дополнительные условные операторы в теги `<Error>`, которые содержат ссылку на Microsoft. VSSDK. BuildTools. Для этого вставьте `'$(VisualStudioVersion)' != '14.0' And` в начале оператора условия. Эти инструкции будут отображаться в нижнем колонтитуле файла CSPROJ.

Например:

```xml
<Error Condition="'$(VisualStudioVersion)' != '14.0' And Exists('packages\Microsoft.VSSDK.BuildTools.15.0.26201…" />
```

* Добавьте дополнительные условные операторы в теги `<Error>`, которые имеют Microsoft. VisualStudio. SDK. Буилдтаскс., Вставьте `'$(VisualStudioVersion)' == '14.0' And` в начале оператора условия. Эти инструкции будут отображаться в нижнем колонтитуле файла CSPROJ.

Например:

```xml
<Error Condition="'$(VisualStudioVersion)' == '14.0' And Exists('packages\Microsoft.VisualStudio.Sdk.BuildTasks.14.0.14.0…" />
```

* Сохраните файл csproj и закройте его. 
  * Обратите внимание, что если в решении используется более одного проекта, установите этот проект в качестве запускаемого проекта с помощью команды "Назначить запускаемым проектом" в контекстном меню проекта). Это гарантирует, что Visual Studio повторно откроет проект после его выгрузки.

## <a name="test-the-extension-installs-in-visual-studio-2015-and-visual-studio-2019-or-2017"></a>Тестирование установки расширения в Visual Studio 2015 и Visual Studio 2019 или 2017

На этом этапе проект должен быть готов к созданию VSIXv3, который можно установить как в Visual Studio 2015, так и в Visual Studio 2017.

* Откройте проект в Visual Studio 2015.
* Создайте проект и убедитесь, что в выходных данных правильно построен VSIX.
* Перейдите в каталог проекта.
* Откройте папку *\bin\Debug* .
* Дважды щелкните VSIX-файл и установите расширение в Visual Studio 2015 и Visual Studio 2019/2017.
* Убедитесь, что расширение можно увидеть в разделе **средства** > **расширения и обновления** раздела **установленные** .
* Попытайтесь запустить или использовать расширение, чтобы проверить его работоспособность.

![Найти VSIX](media/finding-a-VSIX-example.png)

> [!NOTE]
> Если проект зависает с сообщением, **открывающим файл**, принудительно завершит работу Visual Studio, перейдите в каталог проекта, отобразите скрытые папки и удалите папку *. VS* .
 
