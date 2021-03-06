---
title: Получение сведений о службе из хранилища параметров | Документация Майкрософт
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 7028d440-d16d-4b08-9b94-eb8cc93b25fc
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 51aa0369793fe5dc4b39fe510c069a7ec93d102a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/19/2019
ms.locfileid: "72647982"
---
# <a name="get-service-information-from-the-settings-store"></a>Получение сведений о службе из хранилища параметров
С помощью хранилища параметров можно найти все доступные службы или определить, установлена ли определенная служба. Необходимо иметь представление о типе класса службы.

## <a name="to-list-the-available-services"></a>Перечисление доступных служб

1. Создайте проект VSIX с именем `FindServicesExtension`, а затем добавьте пользовательскую команду с именем `FindServicesCommand`. Дополнительные сведения о создании пользовательской команды см. в разделе [Создание расширения с помощью команды меню](../extensibility/creating-an-extension-with-a-menu-command.md) .

2. В *FindServicesCommand.CS*добавьте следующие директивы using:

    ```csharp
    using System.Collections.Generic;
    using Microsoft.VisualStudio.Settings;
    using Microsoft.VisualStudio.Shell.Settings;
    using System.Windows.Forms;
    ```

3. Получите хранилище параметров конфигурации, а затем найдите вложенную коллекцию с именем Services. Эта коллекция включает все доступные службы. В методе `MenuItemCommand` удалите существующий код и замените его следующим:

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);
        SettingsStore configurationSettingsStore = settingsManager.GetReadOnlySettingsStore(SettingsScope.Configuration);
        string message = "Available services:\n";
        IEnumerable<string> collection = configurationSettingsStore.GetSubCollectionNames("Services");
        int n = 0;
        foreach (string service in collection)
        {
            message += configurationSettingsStore.GetString("Services\\" + service, "Name", "Unknown") + "\n";
        }

        MessageBox.Show(message);
    }
    ```

4. Выполните сборку решения и запустите отладку. Откроется экспериментальный экземпляр.

5. В экспериментальном экземпляре в меню **Сервис** выберите команду **вызвать финдсервицескомманд**.

     Должно отобразиться окно сообщения со списком всех служб.

     Чтобы проверить эти параметры, можно использовать редактор реестра.

## <a name="find-a-specific-service"></a>Поиск конкретной службы
 Можно также использовать метод <xref:Microsoft.VisualStudio.Settings.SettingsStore.CollectionExists%2A>, чтобы определить, установлена ли определенная служба. Необходимо иметь представление о типе класса службы.

1. В Менуитемкаллбакк проекта, созданного в предыдущей процедуре, выполните поиск в хранилище параметров конфигурации для коллекции `Services`, которая содержит подколлекцию с именем по идентификатору GUID службы. В этом случае мы будем искать службу справки.

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);
        SettingsStore configurationSettingsStore = settingsManager.GetReadOnlySettingsStore(SettingsScope.Configuration);
        string helpServiceGUID = typeof(SVsHelpService).GUID.ToString("B").ToUpper();
        bool hasHelpService = configurationSettingsStore.CollectionExists("Services\\" + helpServiceGUID);
        string message = "Help Service Available: " + hasHelpService;

        MessageBox.Show(message);
    }
    ```

2. Выполните сборку решения и запустите отладку.

3. В экспериментальном экземпляре в меню **Сервис** выберите команду **вызвать финдсервицескомманд**.

     Должно отобразиться сообщение со **справочной службой "текст справки":** , за которым следует **значение true** или **false**. Чтобы проверить этот параметр, можно использовать редактор реестра, как показано на предыдущих шагах.
