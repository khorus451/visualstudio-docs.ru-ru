---
title: Использование MSBuild | Документация Майкрософт
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, compiling with MSBuild
- MSBuild, extensibility
- packages, compiling with MSBuild
ms.assetid: 9d38c388-1f64-430e-8f6c-e88bc99a4260
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c199df38f2cd51307861462af49f58996fe84fe4
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/22/2019
ms.locfileid: "72722159"
---
# <a name="using-msbuild"></a>Использование MSBuild
MSBuild предоставляет четко определенный расширяемый XML-формат для создания файлов проекта, которые полностью описывают элементы проекта для построения, задачи сборки и конфигурации сборки.

## <a name="general-msbuild-considerations"></a>Общие рекомендации по MSBuild
 Файлы проекта MSBuild, например [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]. csproj и [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]. vbproj, содержат данные, используемые во время сборки, но также могут содержать данные, используемые во время разработки. Данные времени сборки хранятся с помощью примитивов MSBuild, включая [элемент Item (MSBuild)](../../msbuild/item-element-msbuild.md) и [элемент Property (MSBuild)](../../msbuild/property-element-msbuild.md). Данные времени разработки, которые являются данными, относящимися к типу проекта и всем связанным подтипам проекта, хранятся в XML-файле произвольной формы, зарезервированном для него.

 MSBuild не поддерживает встроенную поддержку объектов конфигурации, но предоставляет условные атрибуты для указания данных, относящихся к конфигурации. Пример:

```xml
<OutputDir Condition="'$(Configuration)'=="release'">Bin\MyReleaseConfig</OutputDir>
```

 Дополнительные сведения об условных атрибутах см. в разделе [Условные конструкции](../../msbuild/msbuild-conditional-constructs.md).

### <a name="extending-msbuild-for-your-project-type"></a>Расширение MSBuild для типа проекта
 Интерфейсы и API MSBuild могут быть изменены в будущих версиях [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]. Таким образом, разумно использовать классы Managed Package Framework (MPF), так как они обеспечивают экранирование от изменений.

 Платформа управляемых пакетов для проектов (Мпфпрож) предоставляет вспомогательные классы для создания новой системы проектов и управления ею. Исходный код и инструкции по компиляции можно найти по адресу [MPF for Projects-Visual Studio 2013](https://github.com/tunnelvisionlabs/MPFProj10).

 Классы MPF, относящиеся к проекту, выглядят следующим образом:

|Class|Реализация|
|-----------|--------------------|
|`Microsoft.VisualStudio.Package.ProjectNode`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents>|
|`Microsoft.VisualStudio.Package.ProjectFactory`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>|
|`Microsoft.VisualStudio.Package.HierarchyNode`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>|
|`Microsoft.VisualStudio.Package.ProjectConfig`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg>|
|`Microsoft.VisualStudio.Package.SettingsPage`|<xref:Microsoft.VisualStudio.OLE.Interop.IPropertyPageSite>|

 `Microsoft.VisualStudio.Package.ProjectElement` класс является оболочкой для элементов MSBuild.

#### <a name="single-file-generators-vs-msbuild-tasks"></a>Генераторы одиночных файлов и задачи MSBuild
 Генераторы отдельных файлов доступны только во время разработки, но задачи MSBuild можно использовать во время разработки и во время сборки. Для максимальной гибкости, следовательно, используйте задачи MSBuild для преобразования и создания кода. Дополнительные сведения см. в разделе [Custom Tools](../../extensibility/internals/custom-tools.md).

## <a name="see-also"></a>См. также
- [Справочные сведения о MSBuild](../../msbuild/msbuild-reference.md)
- [MSBuild](../../msbuild/msbuild.md)
- [Настраиваемые средства](../../extensibility/internals/custom-tools.md)