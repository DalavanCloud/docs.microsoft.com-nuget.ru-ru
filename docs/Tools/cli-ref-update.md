---
title: "NuGet CLI обновление команды | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Ссылка для команды update nuget.exe"
keywords: "NuGet обновить ссылку, команда пакета обновления"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 891ce1f27102b16125c93e7a66ebd29f6fc626db
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2018
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="ba977-104">Команда обновления (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ba977-104">update command (NuGet CLI)</span></span>

<span data-ttu-id="ba977-105">**Применяется к:** пакета потребления &bullet; **поддерживаемые версии:** все</span><span class="sxs-lookup"><span data-stu-id="ba977-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="ba977-106">Обновляет все пакеты в проекте (с помощью `packages.config`) их последние версии.</span><span class="sxs-lookup"><span data-stu-id="ba977-106">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="ba977-107">Рекомендуется выполнять [«восстановление»](cli-ref-restore.md) перед запуском `update`.</span><span class="sxs-lookup"><span data-stu-id="ba977-107">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="ba977-108">(Чтобы обновить отдельный пакет, используйте [ `nuget install` ](cli-ref-install.md) без указания номера версии, в котором вариантов NuGet устанавливает последнюю версию.)</span><span class="sxs-lookup"><span data-stu-id="ba977-108">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="ba977-109">Примечание: `update` не работает с CLI, выполняемые с моно (Mac OSX и Linux) или при использовании формата PackageReference.</span><span class="sxs-lookup"><span data-stu-id="ba977-109">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="ba977-110">`update` Команда также обновляет ссылки на сборки в файл проекта, если те уже ссылается на существует.</span><span class="sxs-lookup"><span data-stu-id="ba977-110">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="ba977-111">Если обновленный пакет добавлены сборки, новая ссылка является *не* добавлен.</span><span class="sxs-lookup"><span data-stu-id="ba977-111">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="ba977-112">Новые зависимости пакета также нет ссылок на сборки, их добавить.</span><span class="sxs-lookup"><span data-stu-id="ba977-112">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="ba977-113">Чтобы включить эти операции как часть обновления, обновите пакет в Visual Studio с помощью пользовательского интерфейса диспетчера пакетов или консоли диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="ba977-113">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="ba977-114">Эта команда также может использоваться для обновления nuget.exe себя с помощью *-self* флаг.</span><span class="sxs-lookup"><span data-stu-id="ba977-114">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="ba977-115">Использование</span><span class="sxs-lookup"><span data-stu-id="ba977-115">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="ba977-116">где `<configPath>` идентифицирует либо `packages.config` или файл решения, который содержит список зависимостей проекта.</span><span class="sxs-lookup"><span data-stu-id="ba977-116">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="ba977-117">Параметры</span><span class="sxs-lookup"><span data-stu-id="ba977-117">Options</span></span>

| <span data-ttu-id="ba977-118">Параметр</span><span class="sxs-lookup"><span data-stu-id="ba977-118">Option</span></span> | <span data-ttu-id="ba977-119">Описание:</span><span class="sxs-lookup"><span data-stu-id="ba977-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ba977-120">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="ba977-120">ConfigFile</span></span> | <span data-ttu-id="ba977-121">Файл конфигурации NuGet вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="ba977-121">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ba977-122">Если не указан, *%AppData%\NuGet\NuGet.Config* используется.</span><span class="sxs-lookup"><span data-stu-id="ba977-122">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="ba977-123">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="ba977-123">FileConflictAction</span></span> | <span data-ttu-id="ba977-124">Указывает действие, выполняемое при появлении запроса, чтобы игнорировать существующие файлы, связанные с проектом или перезаписать.</span><span class="sxs-lookup"><span data-stu-id="ba977-124">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="ba977-125">Значения: *перезаписать, игнорировать none*.</span><span class="sxs-lookup"><span data-stu-id="ba977-125">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="ba977-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ba977-126">ForceEnglishOutput</span></span> | <span data-ttu-id="ba977-127">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="ba977-127">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ba977-128">Справка</span><span class="sxs-lookup"><span data-stu-id="ba977-128">Help</span></span> | <span data-ttu-id="ba977-129">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="ba977-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="ba977-130">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="ba977-130">Id</span></span> | <span data-ttu-id="ba977-131">Задает список идентификаторов для обновления пакета.</span><span class="sxs-lookup"><span data-stu-id="ba977-131">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="ba977-132">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="ba977-132">MSBuildPath</span></span> | <span data-ttu-id="ba977-133">*(4.0 +)*  Указывает путь к MSBuild для команды, переназначает `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="ba977-133">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="ba977-134">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="ba977-134">MSBuildVersion</span></span> | <span data-ttu-id="ba977-135">*(3.2 +)*  Указывает версию MSBuild для использования с помощью этой команды.</span><span class="sxs-lookup"><span data-stu-id="ba977-135">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="ba977-136">Поддерживаемые значения: 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="ba977-136">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="ba977-137">По умолчанию выбирается MSBuild в пути в противном случае по умолчанию наибольшую установленную версию MSBuild.</span><span class="sxs-lookup"><span data-stu-id="ba977-137">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="ba977-138">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="ba977-138">NonInteractive</span></span> | <span data-ttu-id="ba977-139">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="ba977-139">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="ba977-140">Предварительный выпуск</span><span class="sxs-lookup"><span data-stu-id="ba977-140">PreRelease</span></span> | <span data-ttu-id="ba977-141">Допускает обновление для предварительных версий.</span><span class="sxs-lookup"><span data-stu-id="ba977-141">Allows updating to prerelease versions.</span></span> <span data-ttu-id="ba977-142">Этот флаг не требуется при обновлении предварительные версии пакетов, которые уже установлены.</span><span class="sxs-lookup"><span data-stu-id="ba977-142">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="ba977-143">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="ba977-143">RepositoryPath</span></span> | <span data-ttu-id="ba977-144">Указывает локальную папку, где установлены пакеты.</span><span class="sxs-lookup"><span data-stu-id="ba977-144">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="ba977-145">Safe</span><span class="sxs-lookup"><span data-stu-id="ba977-145">Safe</span></span> | <span data-ttu-id="ba977-146">Указывает, обновляет только с самой высокой версией, доступной в пределах той же основной и дополнительный номера версии, установленный пакет будет установлен.</span><span class="sxs-lookup"><span data-stu-id="ba977-146">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="ba977-147">Самообслуживания</span><span class="sxs-lookup"><span data-stu-id="ba977-147">Self</span></span> | <span data-ttu-id="ba977-148">Nuget.exe обновления до последней версии; все остальные аргументы учитываются.</span><span class="sxs-lookup"><span data-stu-id="ba977-148">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="ba977-149">Исходный код</span><span class="sxs-lookup"><span data-stu-id="ba977-149">Source</span></span> | <span data-ttu-id="ba977-150">Указывает список источников пакетов (в виде URL-адреса) для обновления.</span><span class="sxs-lookup"><span data-stu-id="ba977-150">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="ba977-151">Если не указано, команда использует источники, предоставляемые в файлах конфигурации см. в разделе [NuGet Настройка поведения](../Consume-Packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="ba977-151">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md).</span></span> |
| <span data-ttu-id="ba977-152">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="ba977-152">Verbosity</span></span> | <span data-ttu-id="ba977-153">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="ba977-153">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="ba977-154">Версия</span><span class="sxs-lookup"><span data-stu-id="ba977-154">Version</span></span> | <span data-ttu-id="ba977-155">Если для одного идентификатора пакета, указывает версию пакета для обновления.</span><span class="sxs-lookup"><span data-stu-id="ba977-155">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="ba977-156">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ba977-156">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ba977-157">Примеры</span><span class="sxs-lookup"><span data-stu-id="ba977-157">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```