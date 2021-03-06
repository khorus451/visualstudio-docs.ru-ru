---
title: Пошаговое руководство. Создание базового приложения изолированной оболочки | Документация Майкрософт
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio shell, walkthroughs
- Shell [Visual Studio], walkthroughs
- walkthroughs [Visual Studio], isolated shell-based application
ms.assetid: 8b12e223-aae3-4c23-813d-ede1125f5f69
caps.latest.revision: 55
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6192eb5583e7d0bc37518e995aacccad643cc9ec
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/10/2020
ms.locfileid: "75850351"
---
# <a name="walkthrough-creating-a-basic-isolated-shell-application"></a>Пошаговое руководство. Создание базового приложения изолированной оболочки
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

В этом пошаговом руководстве показано, как создать изолированное решение оболочки, настроить окно справки о средстве и создать программу установки, устанавливающую изолированную оболочку.  
  
## <a name="prerequisites"></a>Prerequisites  
 Для выполнения этого пошагового руководства необходимо установить пакет SDK для Visual Studio. Дополнительные сведения см. в разделе [пакет SDK для Visual Studio](../extensibility/visual-studio-sdk.md). Чтобы развернуть изолированную оболочку, необходимо также использовать распространяемый пакет оболочки Visual Studio (изолированной).  
  
## <a name="creating-an-isolated-shell-solution"></a>Создание решения изолированной оболочки  
 В этом разделе показано, как использовать шаблон проекта изолированной оболочки Visual Studio для создания изолированного решения оболочки. Решение содержит следующие проекты:  
  
- *Имя_решения*. Проект Абаутбокспаккаже, позволяющий настраивать внешний вид окна "Справка/о программе".  
  
- Проект Шеллекстенсионсвсикс, содержащий файл Source. extension. vsixmanifest, который определяет различные компоненты приложения изолированной оболочки.  
  
- Проект *имяРешения* , создающий исполняемый файл, вызывающий приложение изолированной оболочки. Этот проект содержит папку «Настройка оболочки», которая позволяет настраивать внешний вид и поведение приложения изолированной оболочки.  
  
- Проект пользовательского интерфейса *имяРешения* , создающий вспомогательную сборку, которая определяет команды активного меню и локализуемые строки.  
  
#### <a name="to-create-a-basic-isolated-shell-solution"></a>Создание базового решения изолированной оболочки  
  
1. Откройте Visual Studio и создайте новый проект.  
  
2. В окне **Новый проект** разверните узел **другие типы проектов** , а затем выберите **расширяемость**. Выберите шаблон проекта **изолированная оболочка Visual Studio** .  
  
3. Присвойте проекту имя `MyVSShellStub` и укажите расположение. Убедитесь, что установлен флажок **создать каталог для решения** , и нажмите кнопку **ОК**.  
  
     Новое решение появится в **Обозреватель решений**.  
  
4. Создайте решение и начните отладку приложения изолированной оболочки.  
  
     Откроется изолированная оболочка Visual Studio. В строке заголовка считывается **мивсшеллстуб**. Значок строки заголовка создается из \Мивсшеллстуб\ресаурце Филес\аппликатионикон.ИКО.  
  
## <a name="customizing-the-application-name-and-icon"></a>Настройка имени и значка приложения  
 Вам может потребоваться фирменная символика приложения, используя название компании и ее эмблему в заголовке окна. В следующих шагах показано, как изменить имя и значок, отображаемые в строке заголовка пользовательского приложения, изменив файл определения пакета Мивсшеллстуб. Application. pkgdef.  
  
#### <a name="to-customize-the-application-name-and-icon"></a>Настройка имени и значка приложения  
  
1. В проекте Мивсшеллстуб откройте \Шелл Кустомизатион\мивсшеллстуб.аппликатион.пкгдеф.  
  
2. Измените значение элемента `AppName` на **«AppName» = «Fabrikam Music Editor»** .  
  
3. Чтобы изменить значок приложения, скопируйте другой значок в каталог \Мивсшеллстуб\мивсшеллстуб\мивсшеллстуб\. Переименуйте существующий файл ApplicationIcon. ico в ApplicationIcon1. ico. Переименуйте новый файл в ApplicationIcon. ico.  
  
4. Постройте решение и запустите отладку. Появится интегрированная среда разработки (IDE) изолированной оболочки. В строке заголовка рядом со словами " **музыкальный редактор" компании Fabrikam**будет создан новый значок.  
  
## <a name="customizing-the-default-web-browser-home-page"></a>Настройка домашней страницы веб-браузера по умолчанию  
 В этом разделе показано, как изменить домашнюю страницу по умолчанию в окне **веб-браузера** , изменив файл определения пакета.  
  
#### <a name="to-customize-the-default-web-browser-home-page"></a>Настройка домашней страницы веб-браузера по умолчанию  
  
1. В файле Мивсшеллстуб. Application. pkgdef измените значение элемента `DefaultHomePage` на "<https://www.microsoft.com>".  
  
2. Перестройте проект Мивсшеллстуб.  
  
3. Постройте решение и запустите отладку.  
  
4. В **представлении или других окнах**щелкните **веб-браузер**. В окне **веб-браузера** отображается домашняя страница корпорации Майкрософт.  
  
## <a name="removing-the-print-command"></a>Удаление команды Print  
 Файл. vsct в проекте изолированного интерфейса оболочки состоит из набора объявлений формы `<Define name=No_`*элемента*`>`, где *элемент* является одним из стандартных меню и команд Visual Studio.  
  
 Если объявление не Добавлено в комментарий, это меню или команда исключается из изолированной оболочки. И наоборот, если объявление снабжено комментарием, меню или команда включается в изолированную оболочку.  
  
 В следующих шагах команда раскомментировать печать в файле. vsct.  
  
#### <a name="to-remove-the-print-command"></a>Удаление команды Print  
  
1. Убедитесь, что команда **Печать** появилась в меню **файл** в приложении изолированной оболочки.  
  
2. В проекте Мивсшеллстубуи откройте \Ресаурце Филес\мивсшеллстубуи.вскт для редактирования.  
  
3. Раскомментировать следующую строку:  
  
    ```  
    <!-- <Define name="No_PrintChildrenCommand"/> -->  
    ```  
  
4. При этом удаляется команда Print.  
  
5. Начните отладку приложения изолированной оболочки. Убедитесь, что команда **File/Print** исчезла.  
  
## <a name="removing-features-from-the-isolated-shell"></a>Удаление компонентов из изолированной оболочки  
 Некоторые из пакетов, загруженных в Visual Studio, можно удалить, отредактировав файл pkgundef, если эти функции не нужны в пользовательском приложении изолированной оболочки. Пакет указывается в одном из подразделов раздела реестра $RootKey $ \Паккажес.  
  
> [!NOTE]
> Чтобы найти идентификаторы GUID компонентов Visual Studio, см. раздел [идентификаторы GUID пакета компонентов Visual Studio](../extensibility/package-guids-of-visual-studio-features.md).  
  
 В следующей процедуре показано, как удалить редактор XML из изолированной оболочки.  
  
#### <a name="to-remove-the-xml-editor"></a>Удаление редактора XML  
  
1. Откройте файл Мивсшеллстуб. pkgundef в папке настройки оболочки проекта Мивсшеллстуб.  
  
2. Раскомментируйте следующую строку:  
  
     [$RootKey $ \Паккажес\\{87569308-4813-40a0-9cd0-d7a30838ca3f}]  
  
3. Перестройте решение и начните отладку изолированной оболочки. Откройте XML-файл, например \Мивсшеллстуб\мивсшеллстуб\мивсшеллстубуи\мивсшеллстубуи.вскт. Убедитесь, что ключевые слова XML в файле не являются цветовыми и что ввод "<" в строке не приводит к XML-подсказкам.  
  
## <a name="customizing-the-helpabout-box"></a>Настройка окна «Справка/сведения»  
 Можно настроить окно "Справка/сведения", которое создается как часть шаблона проекта изолированной оболочки.  
  
#### <a name="to-customize-the-company-name"></a>Настройка названия компании  
  
1. Название компании, сведения об авторских правах, версия продукта и описание продукта находятся в проекте Мивсшеллстуб. Абаутбокспаккаже в файле \Пропертиес\ассемблинфо.КС. Откройте этот файл.  
  
2. Измените значение `AssemblyCompany` на **Fabrikam**, `AssemblyProduct` и `AssemblyTitle` значения на " **музыкальный редактор Fabrikam**", а `AssemblyCopyright` значение на " **авторские права" © Fabrikam 2015**:  
  
    ```  
    [assembly: AssemblyTitle("Fabrikam Music Editor")]  
    [assembly: AssemblyDescription("")]  
    [assembly: AssemblyConfiguration("")]  
    [assembly: AssemblyCompany("Fabrikam")]  
    [assembly: AssemblyProduct("Fabrikam Music Editor")]  
    [assembly: AssemblyCopyright("Copyright © Fabrikam 2015")] [assembly: AssemblyCompany("Fabrikam")]  
    [assembly: AssemblyProduct("Fabrikam Music Editor ")]  
    [assembly: AssemblyCopyright("Copyright © Fabrikam 2015”)]  
    ```  
  
3. Чтобы добавить описание продукта, измените значение `AssemblyDescription` на **Описание для музыкального редактора Fabrikam.**  
  
    ```  
    [assembly: AssemblyDescription("The description of Fabrikam Music editor.”)]  
    ```  
  
4. Запустите отладку и в приложении изолированной оболочки откройте окно **Справка/о программе** . Вы должны увидеть измененные строки. Заголовок окна "Справка/сведения" совпадает со значением `AssemblyTitle` в AssemblyInfo.cs.  
  
5. Свойства самого поля " **Справка"/"о программе** " находятся в файле мивсшеллстуб. абаутбокспаккаже\абаутбокс.ксамл. Чтобы изменить ширину окна "Справка/о программе", перейдите к блоку `AboutDialogStyle` и задайте для свойства `Width` значение 200:  
  
    ```  
    <Style x:Key="AboutDialogStyle" TargetType="Window">  
        <Setter Property="Height" Value="Auto" />  
        <Setter Property="Width" Value="200" />  
        <Setter Property="ShowInTaskbar" Value="False" />  
        <Setter Property="ResizeMode" Value="NoResize" />  
        <Setter Property="WindowStyle" Value="SingleBorderWindow" />  
        <Setter Property="SizeToContent" Value="Height" />  
    </Style>  
    ```  
  
6. Перестройте решение и начните отладку изолированной оболочки. Окно "Справка/о программе" должно иметь приблизительно квадрат.  
  
## <a name="before-you-deploy-the-isolated-shell-application"></a>Перед развертыванием приложения изолированной оболочки  
 Приложение изолированной оболочки можно установить на любой компьютер с распространяемым пакетом Visual Studio Shell (изолированной). Дополнительные сведения о распространяемом пакете см. на веб-сайте [загрузки Visual Studio Extensibility](https://msdn.microsoft.com/vstudio/bb984878.aspx) .  
  
## <a name="deploying-the-isolated-shell-application"></a>Развертывание приложения изолированной оболочки  
 Чтобы развернуть приложение изолированной оболочки на целевом компьютере, создайте проект установки. Необходимо указать следующие элементы:  
  
- Макет папок и файлов на целевом компьютере.  
  
- Условия запуска, гарантирующие, что .NET Framework и среда выполнения оболочки Visual Studio установлены на целевом компьютере.  
  
  В следующей процедуре потребуется установить InstallShield Limited Edition на компьютер.  
  
#### <a name="to-create-the-setup-project"></a>Создание проекта установки  
  
1. В **Обозреватель решений**щелкните правой кнопкой мыши узел решения и выберите команду **Добавить новый проект**.  
  
2. В диалоговом окне **Новый проект** разверните узел **другие типы проектов** , а затем выберите пункт **Установка и развертывание**. Выберите шаблон InstallShield. Присвойте новому проекту имя `MySetup` а затем нажмите кнопку **ОК**.  
  
3. Если InstallShield Limited Edition уже установлен, перейдите к следующему шагу.  
  
    Если InstallShield Limited Edition еще не установлен, откроется страница загрузки InstallShield. Следуйте инструкциям по загрузке и установке продукта, выбрав версию InstallShield, совместимую с вашей версией Visual Studio. Необходимо решить, следует ли регистрировать установку InstallShield или использовать ее в качестве ознакомительной версии. После завершения установки необходимо перезапустить Visual Studio.  
  
   > [!IMPORTANT]
   > Перед созданием проекта InstallShield необходимо запустить Visual Studio от имени администратора. Если этого не сделать, при построении проекта возникнет ошибка.  
  
   Дальнейшие действия показывают, как настроить проект установки.  
  
> [!IMPORTANT]
> Убедитесь, что вы создали конфигурацию выпуска проекта изолированной оболочки по крайней мере один раз перед настройкой проекта установки.  
  
#### <a name="to-configure-the-setup-project"></a>Настройка проекта установки  
  
1. В **Обозреватель решений**в проекте **MySetup** выберите **Project Assistant (помощник по проекту**). В нижней строке окна **помощника по проекту** выберите **сведения о приложении**. В качестве имени приложения введите **Fabrikam** в качестве имени вашей компании и в качестве **музыкального редактора Fabrikam** . Щелкните стрелку вперед в правом нижнем углу **помощника по проекту**.  
  
2. Выберите **Да** в разделе **, если приложению требуется установить любое программное обеспечение на компьютере** , а затем выберите **Microsoft .NET Framework 4,5 полный пакет**.  
  
3. Нажмите кнопку **файлы приложения** в нижней части окна и убедитесь, что выбрана папка « **редактор музыки» компании Fabrikam** .  
  
4. Нажмите кнопку **Добавить файлы** . В диалоговом окне **Добавление файлов** добавьте следующие файлы из папки **мивсшеллстуб\релеасе** :  
  
    1. Мивсшеллстуб. exe. config  
  
    2. DebuggerProxy. dll  
  
    3. DebuggerProxy. dll. manifest  
  
    4. Мивсшеллстуб. pkgdef  
  
    5. Мивсшеллстуб. pkgundef  
  
    6. Мивсшеллстуб. винпрф  
  
    7. Splash. bmp  
  
5. Нажмите кнопку **Добавить выходные данные проекта** и добавьте **Мивсшеллстуб/основные выходные данные**. Нажмите кнопку **ОК**.  
  
6. В левой области в разделе **конечный компьютер**щелкните правой кнопкой мыши узел " **музыкальные редакторы Fabrikam" [INSTALLDIR]** и добавьте **новую папку** с именем **Extensions**.  
  
7. Щелкните правой кнопкой мыши узел **расширения** на левой панели и добавьте новую папку с именем **приложение**.  
  
8. Выберите папку **приложения** и нажмите кнопку **Добавить выходные данные проекта** , а затем выберите Основные выходные данные проекта мивсшеллстуб. абаутбокспаккаже.  
  
9. Нажмите кнопку **Добавить файлы** и из папки \мивсшеллстуб\релеасе\екстенсионс\аппликатион\ добавьте следующие файлы:  
  
    - Мивсшеллстуб. Абаутбокспаккаже. pkgdef  
  
    - Мивсшеллстуб. Application. pkgdef  
  
10. Щелкните правой кнопкой мыши узел " **музыкальные редакторы Fabrikam [INSTALLDIR]** " на левой панели и добавьте новую папку с именем **1033**.  
  
11. Выберите папку 1033, а затем нажмите кнопку **Добавить выходные данные проекта** и выберите Основные выходные данные проекта мивсшеллстубуи.  
  
12. Перейдите в окно **ярлыки приложений** .  
  
13. Щелкните **создать** , чтобы создать ярлык, и выберите **[ProgramFilesFolder] \Фабрикам\фабрикам Music едитор\мивсшеллстуб.ПРИМАРИ Output**.  
  
14. Перейдите в область **интервью по установке** .  
  
15. Установите для всех элементов значение **нет**.  
  
16. В **Обозреватель решений**в проекте MySetup откройте окно **Определение требований и действий установки \ требования**. Откроется окно **требования** .  
  
17. Щелкните правой кнопкой мыши **требования к системному программному обеспечению** и выберите **создать новое условие запуска**. Откроется **Мастер поиска системы** .  
  
18. В области **что вы хотите найти?** выберите в раскрывающемся списке пункт **запись реестра** и нажмите кнопку **Далее**.  
  
19. В области **как вы хотите искать?** выберите **HKEY_LOCAL_MACHINE** в качестве корня реестра. Введите **SOFTWARE\Wow6432Node\Microsoft\DevDiv\vs\Servicing\14.0\isoshell** для 64-разрядных систем или **SOFTWARE\Microsoft\DevDiv\vs\Servicing\14.0\isoshell** для 32-разрядных систем и введите в качестве значения реестра **Install** . Нажмите кнопку **Далее**.  
  
20. В области **что вы хотите сделать с панелью значение?** введите **этот продукт, для которого необходимо установить распространяемый компонент изолированной оболочки Visual Studio 2015.** в качестве отображаемого текста и нажмите кнопку **Готово**.  
  
21. Перестройте решение изолированной оболочки, чтобы создать проект установки.  
  
     Файл Setup. exe можно найти в следующей папке:  
  
     \MyVSShellStub\MySetup\MySetup\Express\SingleImage\DiskImages\DISK1  
  
## <a name="testing-the-installation-program"></a>Тестирование программы установки  
 Чтобы протестировать программу установки, скопируйте файл Setup. exe на другой компьютер и запустите исполняемый файл программы установки. Вы сможете запустить приложение изолированной оболочки.
