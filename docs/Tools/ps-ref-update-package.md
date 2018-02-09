---
title: "Справочник по PowerShell пакет обновления NuGet | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Ссылка для команды PowerShell пакета обновления в консоли диспетчера пакетов NuGet в Visual Studio."
keywords: "Пакет NuGet консоли диспетчера, команд NuGet Powershell, справочник по NuGet Powershell, пакет обновления"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 768fdb4d7c785b4f3ed9e70958390676ea965794
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2018
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="4be52-104">Обновление (консоль диспетчера пакетов в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="4be52-104">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="4be52-105">*Доступен только в пределах [консоль диспетчера пакетов NuGet](Package-Manager-Console.md) в Visual Studio в Windows.*</span><span class="sxs-lookup"><span data-stu-id="4be52-105">*Available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="4be52-106">Обновляет пакет и его зависимости, а также все пакеты в проекте, до более новой версии.</span><span class="sxs-lookup"><span data-stu-id="4be52-106">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="4be52-107">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="4be52-107">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="4be52-108">В NuGet 2.8 + `Update-Package` можно использовать для возврата к предыдущей версии существующего пакета в проекте.</span><span class="sxs-lookup"><span data-stu-id="4be52-108">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="4be52-109">Например при наличии 5.1.0-rc1 Microsoft.AspNet.MVC установлен следующая команда будет понизить его до 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="4be52-109">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

<span data-ttu-id="4be52-110">NuGet 2.7 или более ранних версий выдает ошибку, о том, что уже установлена более новая версия.</span><span class="sxs-lookup"><span data-stu-id="4be52-110">NuGet 2.7 and earlier gives an error saying that a newer version is already installed.</span></span>

## <a name="parameters"></a><span data-ttu-id="4be52-111">Параметры</span><span class="sxs-lookup"><span data-stu-id="4be52-111">Parameters</span></span>

|  <span data-ttu-id="4be52-112">Параметр</span><span class="sxs-lookup"><span data-stu-id="4be52-112">Parameter</span></span> | <span data-ttu-id="4be52-113">Описание:</span><span class="sxs-lookup"><span data-stu-id="4be52-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4be52-114">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="4be52-114">Id</span></span> | <span data-ttu-id="4be52-115">Идентификатор пакета для обновления.</span><span class="sxs-lookup"><span data-stu-id="4be52-115">The identifier of the package to update.</span></span> <span data-ttu-id="4be52-116">Если не указано, все пакеты обновления.</span><span class="sxs-lookup"><span data-stu-id="4be52-116">If omitted, updates all packages.</span></span> <span data-ttu-id="4be52-117">— Идентификатор коммутатора сам является необязательным.</span><span class="sxs-lookup"><span data-stu-id="4be52-117">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="4be52-118">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="4be52-118">IgnoreDependencies</span></span> | <span data-ttu-id="4be52-119">Пропускает обновление зависимости пакета.</span><span class="sxs-lookup"><span data-stu-id="4be52-119">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="4be52-120">ИмяПроекта</span><span class="sxs-lookup"><span data-stu-id="4be52-120">ProjectName</span></span> | <span data-ttu-id="4be52-121">Имя проекта, содержащего пакеты для обновления, установка значений по умолчанию для всех проектов.</span><span class="sxs-lookup"><span data-stu-id="4be52-121">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="4be52-122">Версия</span><span class="sxs-lookup"><span data-stu-id="4be52-122">Version</span></span> | <span data-ttu-id="4be52-123">Версия, используемая для обновления, установка значений по умолчанию до последней версии.</span><span class="sxs-lookup"><span data-stu-id="4be52-123">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="4be52-124">В NuGet 3.0 + значение версии должно быть одним из *Lowest, самое высокое, HighestMinor*, или *HighestPatch* (эквивалентно - безопасный).</span><span class="sxs-lookup"><span data-stu-id="4be52-124">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor*, or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="4be52-125">Safe</span><span class="sxs-lookup"><span data-stu-id="4be52-125">Safe</span></span> | <span data-ttu-id="4be52-126">Ограничивает только версии с той же номерами основной и дополнительной версии, в настоящее время установленного пакета обновления.</span><span class="sxs-lookup"><span data-stu-id="4be52-126">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="4be52-127">Исходный код</span><span class="sxs-lookup"><span data-stu-id="4be52-127">Source</span></span> | <span data-ttu-id="4be52-128">Путь URL-адрес или папку источника пакета для поиска.</span><span class="sxs-lookup"><span data-stu-id="4be52-128">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="4be52-129">Пути к локальной папке может быть абсолютным или относительным для текущей папки.</span><span class="sxs-lookup"><span data-stu-id="4be52-129">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="4be52-130">Если не указано, `Uninstall-Package` выполняет поиск в текущем выбранном источнике пакетов.</span><span class="sxs-lookup"><span data-stu-id="4be52-130">If omitted, `Uninstall-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="4be52-131">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="4be52-131">IncludePrerelease</span></span> | <span data-ttu-id="4be52-132">Включает предварительные версии пакетов обновления.</span><span class="sxs-lookup"><span data-stu-id="4be52-132">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="4be52-133">Переустановка</span><span class="sxs-lookup"><span data-stu-id="4be52-133">Reinstall</span></span> | <span data-ttu-id="4be52-134">Resintalls пакетов с помощью текущей установленной версии.</span><span class="sxs-lookup"><span data-stu-id="4be52-134">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="4be52-135">В разделе [путем переустановки и обновления пакетов](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="4be52-135">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="4be52-136">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="4be52-136">FileConflictAction</span></span> | <span data-ttu-id="4be52-137">Действие, выполняемое при появлении запроса, чтобы игнорировать существующие файлы, связанные с проектом или перезаписать.</span><span class="sxs-lookup"><span data-stu-id="4be52-137">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="4be52-138">Возможными значениями являются *перезаписи, пропустить, None, OverwriteAll*, и *IgnoreAll* (3.0 +).</span><span class="sxs-lookup"><span data-stu-id="4be52-138">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="4be52-139">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="4be52-139">DependencyVersion</span></span> | <span data-ttu-id="4be52-140">Версия пакеты зависимостей для использования, которые может принимать одно из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="4be52-140">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="4be52-141">*Наименьший* (по умолчанию): самая ранняя версия</span><span class="sxs-lookup"><span data-stu-id="4be52-141">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="4be52-142">*HighestPatch*: версия с исправлением минимально основных минимально дополнительный: наибольшая</span><span class="sxs-lookup"><span data-stu-id="4be52-142">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="4be52-143">*HighestMinor*: версия с наименьшим основной, наивысший дополнительный номер: наибольшая исправления</span><span class="sxs-lookup"><span data-stu-id="4be52-143">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="4be52-144">*Наибольший* (по умолчанию для пакета обновления без параметров): самую новую версию</span><span class="sxs-lookup"><span data-stu-id="4be52-144">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="4be52-145">Можно задать значение по умолчанию с помощью [ `dependencyVersion` ](../Schema/nuget-config-file.md#config-section) в `Nuget.Config` файла.</span><span class="sxs-lookup"><span data-stu-id="4be52-145">You can set the default value using the [`dependencyVersion`](../Schema/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="4be52-146">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="4be52-146">ToHighestPatch</span></span> | <span data-ttu-id="4be52-147">Ограничивает только версии с той же дополнительный номер версии, в настоящее время установленного пакета обновления.</span><span class="sxs-lookup"><span data-stu-id="4be52-147">Constrains upgrades to only versions with the same Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="4be52-148">ToHighestMinor</span><span class="sxs-lookup"><span data-stu-id="4be52-148">ToHighestMinor</span></span> | <span data-ttu-id="4be52-149">Ограничивает только версии с одной и той же основной версии, установленный пакет обновления.</span><span class="sxs-lookup"><span data-stu-id="4be52-149">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="4be52-150">WhatIf</span><span class="sxs-lookup"><span data-stu-id="4be52-150">WhatIf</span></span> | <span data-ttu-id="4be52-151">Показывает, что произойдет при запуске команды без фактического выполнения обновления.</span><span class="sxs-lookup"><span data-stu-id="4be52-151">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="4be52-152">Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.</span><span class="sxs-lookup"><span data-stu-id="4be52-152">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="4be52-153">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="4be52-153">Common Parameters</span></span>

<span data-ttu-id="4be52-154">`Update-Package`поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="4be52-154">`Update-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="4be52-155">Примеры</span><span class="sxs-lookup"><span data-stu-id="4be52-155">Examples</span></span>

```ps
# Updates all packages in every project of the solution
Update-Package

# Updates every package in the MvcApplication1 project
Update-Package -ProjectName MvcApplication1

# Updates the Elmah package in every project to the latest version
Update-Package Elmah

# Updates the Elmah package to version 1.1.0 in every project showing optional -Id usage
Update-Package -Id Elmah -Version 1.1.0

# Updates the Elmah package within the MvcApplication1 project to the highest "safe" version.
# For example, if Elmah version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2,
# and 1.1 are available in the feed, the -Safe parameter updates the package to 1.0.2 instead
# of 1.1 as it would otherwise.
Update-Package Elmah -ProjectName MvcApplication1 -Safe

# Reinstall the same version of the original package, but with the latest version of dependencies
# (subject to version constraints). If this command rolls a dependency back to an earlier version,
# use Update-Package <dependency_name> to reinstall that one dependency without affecting the
# dependent package.
Update-Package ELmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package ELmah –reinstall -ignoreDependencies
```