---
title: Сведения о конфигурации системы управления версиями | Документация Майкрософт
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], configuration details
ms.assetid: adbee9fc-7a2e-4abe-a3b8-e6615bcd797f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0a6c51dfe4ad9378af04da61dbd7e9011c4678f1
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/22/2019
ms.locfileid: "72723794"
---
# <a name="source-control-configuration-details"></a>Сведения о конфигурации системы управления версиями
Для реализации системы управления версиями необходимо правильно настроить систему проекта или редактор, чтобы сделать следующее:

- Запрос разрешения на переход в измененное состояние

- Запрос разрешения на сохранение файла

- Запрос разрешения на добавление, удаление или переименование файлов в проекте

## <a name="request-permission-to-transition-to-changed-state"></a>Запрос разрешения на переход в измененное состояние
 Проект или редактор должны запрашивать разрешение на переход в измененное состояние (Dirty) путем вызова <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>. Каждый редактор, реализующий <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData.IsDocDataDirty%2A>, должен вызвать <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> и получить утверждение, чтобы изменить документ из среды перед возвратом `True` для <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData.IsDocDataDirty%2A>. Проект, по сути, является редактором для файла проекта, и поэтому несет ответственность за реализацию отслеживания измененных состояний для файла проекта в качестве текстового редактора для своих файлов. Среда обрабатывает измененное состояние решения, но необходимо обработать измененное состояние любого объекта, на который ссылается решение, но не хранить, например файл проекта или его элементы. Как правило, если проект или редактор отвечает за управление сохраняемостью для элемента, то он отвечает за реализацию отслеживания измененных состояний.

 В ответ на вызов `IVsQueryEditQuerySave2::QueryEditFiles` среда может выполнять следующие действия:

- Отклоните вызов Change, в этом случае редактор или проект должны остаться в неизмененном (чистом) состоянии.

- Указывает, что необходимо перезагрузить данные документа. Для проекта среда выполнит перезагрузку данных для проекта. Редактор должен перезагрузить данные с диска с помощью своей реализации <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.ReloadDocData%2A>. В любом случае контекст в проекте или редакторе может измениться при повторной загрузке данных.

  Это сложная и сложная задача модифицировать соответствующие `IVsQueryEditQuerySave2::QueryEditFiles` вызовы на существующую базу кода. В результате эти вызовы должны быть интегрированы во время создания проекта или редактора.

## <a name="request-permission-to-save-a-file"></a>Запрос разрешения на сохранение файла
 Прежде чем проект или редактор сохранит файл, он должен вызвать <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFile%2A> или <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A>. Для файлов проекта эти вызовы автоматически выполняются решением, которое знает, когда следует сохранять файл проекта. Редакторы отвечают за выполнение этих вызовов, если только в реализации редактора `IVsPersistDocData2` не используется вспомогательная функция <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SaveDocDataToFile%2A>. Если редактор реализует `IVsPersistDocData2` таким образом, вызывается метод `IVsQueryEditQuerySave2::QuerySaveFile` или `IVsQueryEditQuerySave2::QuerySaveFiles`.

> [!NOTE]
> Всегда вынимайте эти вызовы с вытеснением, то есть в тот момент, когда редактор сможет получить отмену.

## <a name="request-permission-to-add-remove-or-rename-files-in-the-project"></a>Запрос разрешения на добавление, удаление или переименование файлов в проекте
 Прежде чем проект сможет добавить, переименовать или удалить файл или каталог, он должен вызвать соответствующий метод `IVsTrackProjectDocuments2::OnQuery*`, чтобы запросить разрешение в среде. Если разрешение предоставлено, проект должен завершить операцию, а затем вызвать соответствующий метод `IVsTrackProjectDocuments2::OnAfter*`, чтобы уведомить среду о завершении операции. Проект должен вызывать методы интерфейса <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> для всех файлов (например, специальных файлов), а не только для родительских файлов. Вызовы файлов являются обязательными, но вызовы каталогов являются необязательными. Если проект содержит сведения о каталоге, то он должен вызвать соответствующие методы <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>, но если эти сведения отсутствуют, среда выводит сведения о каталоге.

 Проект не должен вызывать методы `IVsTrackProjectDocuments2` в проекте Open или Close. Прослушиватели, которые хотят получить эту информацию при запуске, могут подождать события <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenSolution%2A> и выполнить итерацию по решению, чтобы найти необходимые сведения. При завершении работы эти сведения не требуются. `IVsTrackProjectDocuments2` предоставляется из <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>.

 Для каждого действия Add, Rename и Remove существует метод `OnQuery*` и метод `OnAfter*`. Вызовите метод `OnQuery*`, чтобы запросить разрешение на добавление, переименование или удаление файла или каталога. Вызовите метод `OnAfter*` после добавления, переименования или удаления файла или каталога, а также состояние проекта, отражающее новое состояние.

## <a name="see-also"></a>См. также

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFile%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SaveDocDataToFile%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>
- [Поддержка системы управления версиями](../../extensibility/internals/supporting-source-control.md)