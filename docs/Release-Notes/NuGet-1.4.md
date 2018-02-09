---
title: "Заметки о выпуске NuGet 1.4 | Документы Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Заметки о выпуске для NuGet 1.4, включая известные проблемы, исправленные ошибки, добавленные функции и DCR."
keywords: "NuGet 1.4 заметки о выпуске, исправления, известными проблемами, добавлены функции, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a69f4f5c7172817d711fa5e995cf6db3875c4810
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-14-release-notes"></a><span data-ttu-id="9615e-104">Заметки о выпуске 1,4 NuGet</span><span class="sxs-lookup"><span data-stu-id="9615e-104">NuGet 1.4 Release Notes</span></span>

<span data-ttu-id="9615e-105">[Заметки о выпуске NuGet 1.3](../release-notes/nuget-1.3.md) | [заметки о выпуске NuGet 1.5](../release-notes/nuget-1.5.md)</span><span class="sxs-lookup"><span data-stu-id="9615e-105">[NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md) | [NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md)</span></span>

<span data-ttu-id="9615e-106">17 июня 2011 г. была выпущена NuGet 1.4.</span><span class="sxs-lookup"><span data-stu-id="9615e-106">NuGet 1.4 was released on June 17, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="9615e-107">Функции</span><span class="sxs-lookup"><span data-stu-id="9615e-107">Features</span></span>

### <a name="update-package-improvements"></a><span data-ttu-id="9615e-108">Усовершенствования пакета обновления</span><span class="sxs-lookup"><span data-stu-id="9615e-108">Update-Package improvements</span></span>
<span data-ttu-id="9615e-109">NuGet 1.4 предоставляет много улучшений, появившихся в команду пакет обновления, облегчая сохранять пакеты в ту же версию несколькими проектами в решении.</span><span class="sxs-lookup"><span data-stu-id="9615e-109">NuGet 1.4 introduces a lot of improvements to the Update-Package command making it easier to keep packages at the same version across multiple projects in a solution.</span></span> <span data-ttu-id="9615e-110">Например при обновлении пакета до последней версии, очень часто требуется всех проектов с помощью этого пакета установки для того же verision обновления.</span><span class="sxs-lookup"><span data-stu-id="9615e-110">For example, when upgrading a package to the latest version, it's very common to want all projects with that package installed to be updated to the same verision.</span></span>

<span data-ttu-id="9615e-111">`Update-Package` Команда теперь становится проще:</span><span class="sxs-lookup"><span data-stu-id="9615e-111">The `Update-Package` command now makes it easier to:</span></span>

#### <a name="update-all-packages-in-a-single-project"></a><span data-ttu-id="9615e-112">Обновить все пакеты в одном проекте</span><span class="sxs-lookup"><span data-stu-id="9615e-112">Update all packages in a single project</span></span>

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a><span data-ttu-id="9615e-113">Обновить пакет во всех проектах</span><span class="sxs-lookup"><span data-stu-id="9615e-113">Update a package in all projects</span></span>

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a><span data-ttu-id="9615e-114">Обновить все пакеты во всех проектах</span><span class="sxs-lookup"><span data-stu-id="9615e-114">Update all packages in all projects</span></span>

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a><span data-ttu-id="9615e-115">Выполнить обновление «безопасной» во всех пакетах</span><span class="sxs-lookup"><span data-stu-id="9615e-115">Perform a "safe" update on all packages</span></span>
<span data-ttu-id="9615e-116">`-Safe` Флаг ограничивает обновления только версии с номерами основной и дополнительной версии одного компонента.</span><span class="sxs-lookup"><span data-stu-id="9615e-116">The `-Safe` flag constrains upgrades to only versions with the same Major and Minor version component.</span></span> <span data-ttu-id="9615e-117">Например, если установлена версия 1.0.0 пакета и в этом канале доступны версии 1.0.1, 1.0.2 и 1.1 `-Safe` флаг обновляет пакет до версии 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="9615e-117">For example, if version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2, and 1.1 are available in the feed, the `-Safe` flag updates the package to 1.0.2.</span></span> <span data-ttu-id="9615e-118">Обновления, не `-Safe` флаг и обновите его до последней версии 1.1.</span><span class="sxs-lookup"><span data-stu-id="9615e-118">Upgrading without the `-Safe` flag would upgrade the package to the latest version, 1.1.</span></span>

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a><span data-ttu-id="9615e-119">Управление пакетами на уровне решения</span><span class="sxs-lookup"><span data-stu-id="9615e-119">Managing Packages at the Solution Level</span></span>
<span data-ttu-id="9615e-120">До NuGet 1.4 установке пакета на несколько проектов не громоздким, с помощью диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="9615e-120">Prior to NuGet 1.4, installing a package into multiple projects was cumbersome using the dialog.</span></span> <span data-ttu-id="9615e-121">Он требуется запуск диалогового окна один раз в проекте.</span><span class="sxs-lookup"><span data-stu-id="9615e-121">It required launching the dialog once per project.</span></span>

<span data-ttu-id="9615e-122">NuGet 1.4 добавляет поддержку для установки или при удалении или обновлении пакетов в нескольких проектах, в то же время.</span><span class="sxs-lookup"><span data-stu-id="9615e-122">NuGet 1.4 adds support for installing/uninstalling/updating packages in multiple projects at the same time.</span></span> <span data-ttu-id="9615e-123">Просто запустите, щелкнув правой кнопкой мыши решение и выбрав **управление пакетами NuGet** пункт меню.</span><span class="sxs-lookup"><span data-stu-id="9615e-123">Simply launch the by right clicking the Solution and selecting the **Manage NuGet Packages** menu option.</span></span>

![Диалоговое окно Управление пакетами NuGet уровня решения](./media/manage-nuget-packages-solution-dialog.png)

<span data-ttu-id="9615e-125">Обратите внимание, что в строке заголовка диалогового окна отображается имя решения, а не имя проекта.</span><span class="sxs-lookup"><span data-stu-id="9615e-125">Notice that in the title bar of the dialog, the name of the solution is displayed, not the name of a project.</span></span>
<span data-ttu-id="9615e-126">Пакет управления теперь предоставляют список флажков со списком проектов, которые следует применить эту операцию для.</span><span class="sxs-lookup"><span data-stu-id="9615e-126">Package operations now provide a list of checkboxes with the list of projects the operation should apply to.</span></span>

![Выбор проекта NuGet пакетов управления](./media/manage-nuget-packages-project-selection.png)

<span data-ttu-id="9615e-128">Дополнительные сведения см. в разделе [управление пакетами для решения](../tools/package-manager-ui.md#managing-packages-for-the-solution).</span><span class="sxs-lookup"><span data-stu-id="9615e-128">For more details, see the topic on [Managing Packages for the Solution](../tools/package-manager-ui.md#managing-packages-for-the-solution).</span></span>

### <a name="constraining-upgrades-to-allowed-versions"></a><span data-ttu-id="9615e-129">Ограничивает обновления до версии допускается</span><span class="sxs-lookup"><span data-stu-id="9615e-129">Constraining Upgrades To Allowed Versions</span></span>
<span data-ttu-id="9615e-130">По умолчанию при выполнении `Update-Package` команды в пакете (или обновление пакета с помощью диалогового окна), обновляется до последней версии в канале.</span><span class="sxs-lookup"><span data-stu-id="9615e-130">By default, when running the `Update-Package` command on a package (or updating the package using dialog), it will be updated to the latest version in the feed.</span></span> <span data-ttu-id="9615e-131">И новая поддержка обновлении всех пакетов могут быть случаи, в которых требуется заблокировать диапазон конкретной версии пакета.</span><span class="sxs-lookup"><span data-stu-id="9615e-131">With the new support for updating all packages, there may be cases in which you want to lock a package to a specific version range.</span></span> <span data-ttu-id="9615e-132">Например известно заранее, приложение будет работать только с 2.\* версия пакета, но не 3.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="9615e-132">For example, you may know in advance that your application will only work with version 2.\* of a package, but not 3.0 and above.</span></span> <span data-ttu-id="9615e-133">Чтобы предотвратить случайное обновление пакета 3, NuGet 1.4 добавляет поддержку ограничивают диапазон версий, которые могут быть обновлены до пакетов, вручную изменив `packages.config` текстовый файл с помощью нового `allowedVersions` атрибута.</span><span class="sxs-lookup"><span data-stu-id="9615e-133">In order to prevent accidentally updating the package to 3, NuGet 1.4 adds support for constraining the range of versions that packages can be upgraded to by hand editing the `packages.config` file using the new `allowedVersions` attribute.</span></span>

<span data-ttu-id="9615e-134">Например, приведенный ниже показано, как заблокировать `SomePackage` пакета версии 2.0 – 3,0 (исключительно) в диапазоне.</span><span class="sxs-lookup"><span data-stu-id="9615e-134">For example, the following example shows how to lock the `SomePackage` package the version range 2.0 - 3.0 (exclusive).</span></span>
<span data-ttu-id="9615e-135">`allowedVersions` Атрибут принимает значения с помощью [формат версии диапазон](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="9615e-135">The `allowedVersions` attribute accepts values using the [version range format](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

<span data-ttu-id="9615e-136">Обратите внимание, что в версии 1.4, блокировка пакета диапазону конкретной версии необходимо изменить вручную.</span><span class="sxs-lookup"><span data-stu-id="9615e-136">Note that in 1.4, locking a package to a specific version range must be hand-edited.</span></span> <span data-ttu-id="9615e-137">В 1,5 NuGet планируется добавить поддержку для размещения этого диапазона через `Install-Package` команды.</span><span class="sxs-lookup"><span data-stu-id="9615e-137">In NuGet 1.5 we plan to add support for placing this range via the `Install-Package` command.</span></span>

### <a name="package-visualizer"></a><span data-ttu-id="9615e-138">Визуализатор пакета</span><span class="sxs-lookup"><span data-stu-id="9615e-138">Package Visualizer</span></span>
<span data-ttu-id="9615e-139">Новый пакет визуализатор, посредством **средства** -> **диспетчер пакетов библиотеки** -> **визуализатор пакета** позволяет параметр меню легко получить все проекты и зависимости пакетов в решении.</span><span class="sxs-lookup"><span data-stu-id="9615e-139">The new package visualizer, launched via the **Tools** -> **Library Package Manager** -> **Package Visualizer** menu option, enables you to easily visualize all the projects and their package dependencies within a solution.</span></span>

<span data-ttu-id="9615e-140">_**Важное замечание:** эта функция использует DGML поддержки в Visual Studio. Создание визуализации поддерживается только в Visual Studio Ultimate. Просмотр схемы DGML поддерживается только в Visual Studio Premium и выше._</span><span class="sxs-lookup"><span data-stu-id="9615e-140">_**Important Note:** This feature takes advantage of the DGML support in Visual Studio. Creating the visualization is only supported in Visual Studio Ultimate. Viewing a DGML diagram is only supported in Visual Studio Premium or Higher._</span></span>

![Визуализатор пакета](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a><span data-ttu-id="9615e-142">Автоматической проверки наличия обновлений для диалогового окна NuGet</span><span class="sxs-lookup"><span data-stu-id="9615e-142">Automatic Update Check for the NuGet Dialog</span></span>
<span data-ttu-id="9615e-143">В некоторых версиях NuGet включать новые компоненты, выраженное через `.nuspec` файл, который не распознаются в более ранних версиях диалогового окна NuGet.</span><span class="sxs-lookup"><span data-stu-id="9615e-143">Some versions of NuGet introduce new features expressed via the `.nuspec` file which are not understood by older versions of the NuGet dialog.</span></span>
<span data-ttu-id="9615e-144">Примером является введение в версии 1.4 NuGet для [указание сборки платформы](../release-notes/nuget-1.2.md#framework-assembly-refs).</span><span class="sxs-lookup"><span data-stu-id="9615e-144">One example is the introduction in NuGet 1.4 for [specifying framework assemblies](../release-notes/nuget-1.2.md#framework-assembly-refs).</span></span>
<span data-ttu-id="9615e-145">По этой причине необходимо использовать последнюю версию NuGet, чтобы убедиться, что можно использовать преимущества новейших функций пакетов.</span><span class="sxs-lookup"><span data-stu-id="9615e-145">Because of this, it's important to use the latest version of NuGet to ensure you can use packages taking advantage of the latest features.</span></span>
<span data-ttu-id="9615e-146">Для выполнения обновлений в NuGet более видимым, NuGet диалоговое окно содержит логику для выделения, когда доступна более новая версия.</span><span class="sxs-lookup"><span data-stu-id="9615e-146">To make updates to NuGet more visible, the NuGet dialog contains logic to highlight when a newer version is available.</span></span>

<span data-ttu-id="9615e-147">_**Примечание**: Проверка проводится только в том случае, если **Online** вкладку был выбран в текущем сеансе._</span><span class="sxs-lookup"><span data-stu-id="9615e-147">_**Note**: The check is only made if the **Online** tab has been selected in the current session._</span></span>

![Управление пакетами NuGet диалоговое окно с доступна новая версия](./media/manage-nuget-packages-update-notification.png)

<span data-ttu-id="9615e-149">Чтобы отказаться от автоматической проверки на наличие обновлений, перейдите в диалоговое окно параметров NuGet и снимите флажок **автоматически проверять наличие обновлений**.</span><span class="sxs-lookup"><span data-stu-id="9615e-149">To turn off the automatic check for updates, go to the NuGet settings dialog and uncheck **Automatically check for updates**.</span></span>

![Параметры NuGet](./media/nuget-settings.png)

<span data-ttu-id="9615e-151">Эта функция фактически была добавлена в версии 1.3 NuGet, но не будет видима, конечно, до обновления до версии 1.3, например NuGet 1.4, стало доступно.</span><span class="sxs-lookup"><span data-stu-id="9615e-151">This feature was actually added in NuGet 1.3, but would not be visible, of course, until an update to 1.3, such as NuGet 1.4, was made available.</span></span>

### <a name="package-manager-dialog-improvements"></a><span data-ttu-id="9615e-152">Усовершенствования в диалоговом окне диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="9615e-152">Package Manager Dialog Improvements</span></span>
* <span data-ttu-id="9615e-153">**Имена меню улучшена**: параметры меню для запуска диалогового окна были переименованы для ясности.</span><span class="sxs-lookup"><span data-stu-id="9615e-153">**Menu names improved**: Menu options to launch the dialog have been renamed for clarity.</span></span> <span data-ttu-id="9615e-154">Пункт меню становится **управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="9615e-154">The menu option is now **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="9615e-155">**Области сведений отображаются последние обновления**: NuGet диалоговое окно отображает дату последнего обновления в области сведений для пакета при **Online** или **обновляет** выделенной вкладки.</span><span class="sxs-lookup"><span data-stu-id="9615e-155">**Details pane shows latest update date**: The NuGet dialog displays the date of the latest update in the details pane for a package when the **Online** or **Updates** tab is selected.</span></span>
* <span data-ttu-id="9615e-156">**Список тегов отображается**: Отображение диалогового окна Nuget тегов.</span><span class="sxs-lookup"><span data-stu-id="9615e-156">**List of tags displayed**: The Nuget dialog displays tags.</span></span>

### <a name="powershell-improvements"></a><span data-ttu-id="9615e-157">Усовершенствования PowerShell</span><span class="sxs-lookup"><span data-stu-id="9615e-157">Powershell Improvements</span></span>
* <span data-ttu-id="9615e-158">**Подпись сценариев PowerShell**: NuGet включает включения использования в средах с более строгими знаком сценариев Powershell.</span><span class="sxs-lookup"><span data-stu-id="9615e-158">**Signed PowerShell scripts**: NuGet includes signed Powershell scripts enabling usage in more restrictive environments.</span></span>
* <span data-ttu-id="9615e-159">**Запрос поддержки**: консоль диспетчера пакетов теперь поддерживает запросы через `$host.ui.Prompt` и `$host.ui.PromptForChoice` команд.</span><span class="sxs-lookup"><span data-stu-id="9615e-159">**Prompting Support**: The Package Manager Console now supports prompting via the `$host.ui.Prompt` and `$host.ui.PromptForChoice` commands.</span></span>
* <span data-ttu-id="9615e-160">**Имена исходных пакетов**: при указании источника пакета с помощью указания имени источника пакета поддерживается `-Source` флаг.</span><span class="sxs-lookup"><span data-stu-id="9615e-160">**Package Source Names**: Supplying the name of a package source is supported when specifying a package source using the `-Source` flag.</span></span>

### <a name="nugetexe-command-line-improvements"></a><span data-ttu-id="9615e-161">Усовершенствования командной строки NuGet.exe</span><span class="sxs-lookup"><span data-stu-id="9615e-161">nuget.exe Command line improvements</span></span>
* <span data-ttu-id="9615e-162">**Пользовательские команды NuGet**: nuget.exe является расширяемым посредством пользовательских команд с помощью MEF.</span><span class="sxs-lookup"><span data-stu-id="9615e-162">**NuGet Custom Commands**: nuget.exe is extensible via custom commands using MEF.</span></span>
* <span data-ttu-id="9615e-163">**Простой рабочий процесс для создания пакетов символ**: `-Symbols` флаг может применяться к обычным соглашение на основе структура папок, создание пакета символов, только включив источника и `.pdb` файлы в папке.</span><span class="sxs-lookup"><span data-stu-id="9615e-163">**Simpler the workflow for creating symbol packages**: The `-Symbols` flag can be applied to a normal convention based folder structure creating a symbols package by only including the source and `.pdb` files within the folder.</span></span>
* <span data-ttu-id="9615e-164">**Указание нескольких источников**: `NuGet install` команда поддерживает задание нескольких источников, с помощью точки с запятой в качестве разделителя или путем указания `-Source` несколько раз.</span><span class="sxs-lookup"><span data-stu-id="9615e-164">**Specifying Multiple Sources**: The `NuGet install` command supports specifying multiple sources using semi-colons as a delimiter or by specifying `-Source` multiple times.</span></span>
* <span data-ttu-id="9615e-165">**Проверка подлинности прокси-сервер поддерживает**: 1,4 NuGet добавляет поддержку для запроса учетных данных пользователя при использовании NuGet через прокси, который требует проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="9615e-165">**Proxy Authentication Support**: NuGet 1.4 adds support for prompting for user credentials when using NuGet behind a proxy that requires authentication.</span></span>
* <span data-ttu-id="9615e-166">**NuGet.exe обновить критические изменения**: `-Self` флаг теперь доступен для nuget.exe для самостоятельного обновления.</span><span class="sxs-lookup"><span data-stu-id="9615e-166">**nuget.exe Update Breaking Change**: The `-Self` flag is now required for nuget.exe to update itself.</span></span> <span data-ttu-id="9615e-167">`nuget.exe Update`Теперь принимает путь к `packages.config` файл и попытается обновить пакеты.</span><span class="sxs-lookup"><span data-stu-id="9615e-167">`nuget.exe Update` now takes in a path to the `packages.config` file and will attempt to update packages.</span></span> <span data-ttu-id="9615e-168">Обратите внимание, что это обновление может содержать только в том, что он не будет: ** обновить, добавить, удалить содержимое из файла проекта.</span><span class="sxs-lookup"><span data-stu-id="9615e-168">Note that this update is limited in that it will not: ** Update, add, remove content in the project file.</span></span>
<span data-ttu-id="9615e-169">** Запустите скрипты Powershell в пакете.</span><span class="sxs-lookup"><span data-stu-id="9615e-169">** Run Powershell scripts within the package.</span></span>

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a><span data-ttu-id="9615e-170">Поддержка Server NuGet для принудительной отправки пакетов, с помощью nuget.exe</span><span class="sxs-lookup"><span data-stu-id="9615e-170">NuGet Server Support for Pushing Packages using nuget.exe</span></span>
<span data-ttu-id="9615e-171">Простой способ размещения включает NuGet [упрощенных веб репозитория NuGet](../hosting-packages/NuGet-Server.md) через `NuGet.Server` пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="9615e-171">NuGet includes a simple way to host a [lightweight web based NuGet repository](../hosting-packages/NuGet-Server.md) via the `NuGet.Server` NuGet package.</span></span> <span data-ttu-id="9615e-172">С помощью NuGet 1.4 облегченная версия сервера поддерживает принудительную и удаление пакетов с помощью nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="9615e-172">With NuGet 1.4, the lightweight server supports pushing and deleting packages using nuget.exe.</span></span>
<span data-ttu-id="9615e-173">Последнюю версию `NuGet.Server` добавляет новый `appSetting`с именем `apiKey`.</span><span class="sxs-lookup"><span data-stu-id="9615e-173">The latest version of `NuGet.Server` adds a new `appSetting`, named `apiKey`.</span></span> <span data-ttu-id="9615e-174">Когда ключ пропущен или оставить пустым, передача пакетов на веб-канала отключена.</span><span class="sxs-lookup"><span data-stu-id="9615e-174">When the key is omitted or left blank, pushing packages to the feed is disabled.</span></span> <span data-ttu-id="9615e-175">Установка apiKey значение (в идеале надежный пароль) включает принудительную отправку пакетов, с помощью nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="9615e-175">Setting the apiKey to a value (ideally a strong password) enables pushing packages using nuget.exe.</span></span>

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a><span data-ttu-id="9615e-176">Поддержка выпуска Mango средства Windows Phone</span><span class="sxs-lookup"><span data-stu-id="9615e-176">Support for Windows Phone Tools Mango Edition</span></span>
<span data-ttu-id="9615e-177">NuGet теперь поддерживается в версии-кандидата средства Windows Phone Mango.</span><span class="sxs-lookup"><span data-stu-id="9615e-177">NuGet is now supported in the release candidate version of Windows Phone Tools for Mango.</span></span>
<span data-ttu-id="9615e-178">В настоящее время средства Windows Phone не поддерживается для диспетчера таким образом установить NuGet для Windows Phone средства расширения Visual Studio, необходимо загрузить и запустить VSIX вручную.</span><span class="sxs-lookup"><span data-stu-id="9615e-178">Currently, Windows Phone Tools does not have support for the Visual Studio Extension manager so to install NuGet for Windows Phone Tools, you may need to download and run the VSIX manually.</span></span>

<span data-ttu-id="9615e-179">Чтобы удалить NuGet для Windows Phone средства, выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="9615e-179">To uninstall NuGet for Windows Phone Tools, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a><span data-ttu-id="9615e-180">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="9615e-180">Bug Fixes</span></span>
<span data-ttu-id="9615e-181">NuGet 1.4 было всего 88 рабочие элементы фиксированной.</span><span class="sxs-lookup"><span data-stu-id="9615e-181">NuGet 1.4 had a total of 88 work items fixed.</span></span> <span data-ttu-id="9615e-182">71 те из них были помечены как ошибки.</span><span class="sxs-lookup"><span data-stu-id="9615e-182">71 of those were marked as bugs.</span></span>

<span data-ttu-id="9615e-183">Полный список рабочих элементов исправления в NuGet 1.4 представление [NuGet отслеживания проблем в этом выпуске](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="9615e-183">For a full list of work items fixed in NuGet 1.4, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="9615e-184">Исправления следует отметить:</span><span class="sxs-lookup"><span data-stu-id="9615e-184">Bug fixes worth noting:</span></span>

* <span data-ttu-id="9615e-185">[Проблема 603](http://nuget.codeplex.com/workitem/603): зависимости пакетов через разные репозитории корректно разрешается при указании источника пакета.</span><span class="sxs-lookup"><span data-stu-id="9615e-185">[Issue 603](http://nuget.codeplex.com/workitem/603): Package dependencies across different repositories resolves correctly when specifying a specific package source.</span></span>
* <span data-ttu-id="9615e-186">[Проблема 1036](http://nuget.codeplex.com/workitem/1036): добавление `NuGet Pack SomeProject.csproj` в событие после построения больше не приводит к бесконечному циклу.</span><span class="sxs-lookup"><span data-stu-id="9615e-186">[Issue 1036](http://nuget.codeplex.com/workitem/1036): Adding `NuGet Pack SomeProject.csproj` to post-build event no longer causes an infinite loop.</span></span>
* <span data-ttu-id="9615e-187">[Проблема 961](http://nuget.codeplex.com/workitem/961): `-Source` флаг поддерживает относительные пути.</span><span class="sxs-lookup"><span data-stu-id="9615e-187">[Issue 961](http://nuget.codeplex.com/workitem/961): `-Source` flag supports relative paths.</span></span>

## <a name="nuget-14-update"></a><span data-ttu-id="9615e-188">Обновление 1.4 NuGet</span><span class="sxs-lookup"><span data-stu-id="9615e-188">NuGet 1.4 Update</span></span>
<span data-ttu-id="9615e-189">Вскоре после выпуска NuGet 1.4 обнаружено несколько проблем, которые были необходимо исправить.</span><span class="sxs-lookup"><span data-stu-id="9615e-189">Shortly after the release of NuGet 1.4, we found a couple of issues that were important to fix.</span></span>
<span data-ttu-id="9615e-190">Определенный номер версии этого обновления в версии 1.4 — 1.4.20615.9020.</span><span class="sxs-lookup"><span data-stu-id="9615e-190">The specific version number of this update to 1.4 is 1.4.20615.9020.</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="9615e-191">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="9615e-191">Bug Fixes</span></span>
* <span data-ttu-id="9615e-192">[Проблема 1220](http://nuget.codeplex.com/workitem/1220): пакет обновления не выполняет `install.ps1` / `uninstall.ps1` во всех проектах, если имеется более одного проекта</span><span class="sxs-lookup"><span data-stu-id="9615e-192">[Issue 1220](http://nuget.codeplex.com/workitem/1220): Update-Package doesnt execute `install.ps1`/`uninstall.ps1` in all projects when there is more than one project</span></span>
* <span data-ttu-id="9615e-193">[Проблема 1156](http://nuget.codeplex.com/workitem/1156): консоль диспетчера пакетов, прикрепленной W2K3/XP (если Powershell 2 не установлена)</span><span class="sxs-lookup"><span data-stu-id="9615e-193">[Issue 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Consol stuck on W2K3/XP (when Powershell 2 is not installed)</span></span>