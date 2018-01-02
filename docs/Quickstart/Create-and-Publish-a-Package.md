---
title: "Вводное руководство по созданию и публикации пакета NuGet | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/3/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 91781ed6-da5c-49f0-b973-16dd8ad84229
description: "Пошаговый учебник по созданию и публикации пакета NuGet с помощью интерфейса командной строки nuget.exe и Visual Studio."
keywords: "создание пакетов NuGet, публикация пакетов NuGet, учебник NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 36a7c2b1d056dddf07a59737de1c3e94294689ac
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="create-and-publish-a-package"></a><span data-ttu-id="6ff0b-104">Создание и публикация пакета</span><span class="sxs-lookup"><span data-stu-id="6ff0b-104">Create and publish a package</span></span>

<span data-ttu-id="6ff0b-105">Создание пакета NuGet из библиотеки классов .NET и его публикация на сайте nuget.org выполняются очень просто. Ниже показано, как сделать это с помощью интерфейса командной строки NuGet и Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="6ff0b-105">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org. The following steps walk you through the process using the NuGet command-line interface (CLI) and Visual Studio:</span></span>

- [<span data-ttu-id="6ff0b-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6ff0b-106">Pre-requisites</span></span>](#install-pre-requisites)
- [<span data-ttu-id="6ff0b-107">Создание файла манифеста пакета NUSPEC</span><span class="sxs-lookup"><span data-stu-id="6ff0b-107">Create the .nuspec package manifest file</span></span>](#create-the-nuspec-package-manifest-file)
- [<span data-ttu-id="6ff0b-108">Выполнение команды pack</span><span class="sxs-lookup"><span data-stu-id="6ff0b-108">Run the pack command</span></span>](#run-the-pack-command)
- [<span data-ttu-id="6ff0b-109">Публикация пакета</span><span class="sxs-lookup"><span data-stu-id="6ff0b-109">Publish the package</span></span>](#publish-the-package)

## <a name="pre-requisites"></a><span data-ttu-id="6ff0b-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6ff0b-110">Pre-requisites</span></span>

1. <span data-ttu-id="6ff0b-111">Установите любой выпуск Visual Studio 2017 со страницы [visualstudio.com](https://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="6ff0b-111">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/).</span></span>

1. <span data-ttu-id="6ff0b-112">Установите средство интерфейса командной строки NuGet `nuget.exe`, скачав последнюю версию `nuget.exe` со страницы [nuget.org/downloads](https://nuget.org/downloads) и сохранив `.exe` в расположении, указанном в переменной PATH.</span><span class="sxs-lookup"><span data-stu-id="6ff0b-112">Install the NuGet CLI tool, `nuget.exe`, by downloading the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), and saving the `.exe` to a location in your PATH.</span></span> <span data-ttu-id="6ff0b-113">Обратите внимание, что скачивается *само* средство, а не установщик.</span><span class="sxs-lookup"><span data-stu-id="6ff0b-113">Note that the download *is* the tool itself, not an installer.</span></span>

1. <span data-ttu-id="6ff0b-114">Создайте подходящий проект библиотеки классов .NET для кода, который нужно упаковать.</span><span class="sxs-lookup"><span data-stu-id="6ff0b-114">Create a suitable .NET Class Library project for the code you want to package.</span></span> <span data-ttu-id="6ff0b-115">Если у вас еще нет проекта, вы можете создать его следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6ff0b-115">If you don't already have a project, you can create a simple one as follows:</span></span>
    1. <span data-ttu-id="6ff0b-116">В Visual Studio выберите **Файл > Создать > Проект**, разверните узел **Visual C# > Windows**, выберите шаблон "Библиотека классов", назовите проект "AppLogger" и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6ff0b-116">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > Windows** node, select the "Class Library" template, name the project AppLogger, and click **OK**.</span></span>
    1. <span data-ttu-id="6ff0b-117">Щелкните правой кнопкой мыши полученный файл проекта и выберите пункт **Сборка**, чтобы убедиться, что проект создан правильно.</span><span class="sxs-lookup"><span data-stu-id="6ff0b-117">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="6ff0b-118">Библиотека DLL находится в папке Debug (или папке Release, если вы используете конфигурацию выпуска для сборки).</span><span class="sxs-lookup"><span data-stu-id="6ff0b-118">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

    <span data-ttu-id="6ff0b-119">В реальном пакете NuGet вы, конечно же, реализовали бы множество полезных возможностей, с помощью которых другие пользователи могли бы создавать приложения.</span><span class="sxs-lookup"><span data-stu-id="6ff0b-119">Within a real NuGet package, of course, you'll implement many useful features upon which others can build applications.</span></span> <span data-ttu-id="6ff0b-120">Однако в этом пошаговом руководстве вы не будете писать дополнительный код, так как библиотеки классов из шаблона достаточно для создания пакета.</span><span class="sxs-lookup"><span data-stu-id="6ff0b-120">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span>

## <a name="create-the-nuspec-package-manifest-file"></a><span data-ttu-id="6ff0b-121">Создание файла манифеста пакета NUSPEC</span><span class="sxs-lookup"><span data-stu-id="6ff0b-121">Create the .nuspec package manifest file</span></span>

<span data-ttu-id="6ff0b-122">Каждому пакету NuGet нужен манифест &mdash; файл `.nuspec` &mdash; для описания его содержимого и зависимостей.</span><span class="sxs-lookup"><span data-stu-id="6ff0b-122">Every NuGet package needs a manifest&mdash;a `.nuspec` file&mdash;to describe its contents and its dependencies.</span></span> <span data-ttu-id="6ff0b-123">Команда `nuget spec` создает этот файл, который затем можно настроить.</span><span class="sxs-lookup"><span data-stu-id="6ff0b-123">The `nuget spec` command creates this file for you, which you then customize.</span></span> <span data-ttu-id="6ff0b-124">В этом примере вы создаете `.nuspec` из файла проекта. Манифест можно создать и другими средствами, как описано в статье [Создание пакета](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="6ff0b-124">In this example you create the `.nuspec` from a project file; you can also create the manifest through other means as described on [Create a Package](../create-packages/creating-a-package.md).</span></span>

1. <span data-ttu-id="6ff0b-125">Откройте командную строку и перейдите в папку, содержащую файл проекта (`.csproj`).</span><span class="sxs-lookup"><span data-stu-id="6ff0b-125">Open a command prompt and navigate to the folder containing your project file (`.csproj`).</span></span>

1. <span data-ttu-id="6ff0b-126">Запустите команду `spec` интерфейса командной строки NuGet, чтобы создать манифест, которому присваивается имя проекта, то есть `AppLogger.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="6ff0b-126">Run the NuGet CLI `spec` command to generate the manifest, which is named after your project, such as `AppLogger.nuspec`:</span></span>

    ```
    nuget spec
    ```

1. <span data-ttu-id="6ff0b-127">Откройте файл в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="6ff0b-127">Open the file in a text editor.</span></span> <span data-ttu-id="6ff0b-128">Манифест похож на приведенный ниже код, где токены вида *$`<token>`$* заменяются во время обработки упаковки на значения из файла Properties/AssemblyInfo.cs проекта.</span><span class="sxs-lookup"><span data-stu-id="6ff0b-128">The manifest looks something like the code below, where tokens in the form *$`<token>`$* are be replaced during the packaging process with values from the project's Properties/AssemblyInfo.cs file.</span></span> <span data-ttu-id="6ff0b-129">Дополнительные сведения о токенах см. в разделе [Создание файла NUSPEC](../create-packages/creating-a-package.md#creating-the-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="6ff0b-129">For more details on tokens, see [Creating a .nuspec file](../create-packages/creating-a-package.md#creating-the-nuspec-file).</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>$id$</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>$author$</authors>
        <owners>$author$</owners>
        <licenseUrl>http://LICENSE_URL_HERE_OR_DELETE_THIS_LINE</licenseUrl>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>$description$</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>Tag1 Tag2</tags>
        </metadata>
    </package>
    ```

1. <span data-ttu-id="6ff0b-130">Выберите идентификатор пакета, который уникален в пределах сайта nuget.org. Мы рекомендуем использовать соглашения об именовании, описанные в разделе [Создание пакета](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="6ff0b-130">Select a package ID that is unique across nuget.org. We recommend using the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="6ff0b-131">Обновите теги автора и описания, в противном случае на следующем шаге возникнет ошибка.</span><span class="sxs-lookup"><span data-stu-id="6ff0b-131">Be sure to update the author and description tags or you get an error in the next step.</span></span> <span data-ttu-id="6ff0b-132">Вот пример обновленного файла `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="6ff0b-132">Here's an updated `.nuspec` file as an example:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>MyCompanyName.MyProductName.MyPackageName</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>kraigb</authors>
        <owners>kraigb</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>application app logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Note]
> <span data-ttu-id="6ff0b-133">Если пакет будет общедоступным, обратите особое внимание на элемент `<tags>`, так как эти теги помогают найти ваш пакет и понять его назначение.</span><span class="sxs-lookup"><span data-stu-id="6ff0b-133">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="6ff0b-134">Выполнение команды pack</span><span class="sxs-lookup"><span data-stu-id="6ff0b-134">Run the pack command</span></span>

<span data-ttu-id="6ff0b-135">Чтобы выполнить сборку пакета NuGet (файла `.nupkg`) из проекта, запустите команду `pack`:</span><span class="sxs-lookup"><span data-stu-id="6ff0b-135">To build a NuGet package (a `.nupkg` file) from a project, run the `pack` command:</span></span>

```
nuget pack AppLogger.csproj
```

<span data-ttu-id="6ff0b-136">Она создает `AppLogger.1.0.0.0.nupkg` с помощью имени пакета и номера версии из файла `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="6ff0b-136">This command creates `AppLogger.1.0.0.0.nupkg` using the package name and version number from the `.nuspec` file.</span></span> <span data-ttu-id="6ff0b-137">Эта команда выдает предупреждения, если вы еще не изменили значения по умолчанию в различных полях файла `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="6ff0b-137">The command issues warnings if you haven't updated various fields in the `.nuspec` file from their default values.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="6ff0b-138">Публикация пакета</span><span class="sxs-lookup"><span data-stu-id="6ff0b-138">Publish the package</span></span>

<span data-ttu-id="6ff0b-139">Получив файл `.nupkg`, вы публикуете его на сайте nuget.org с помощью команды `push`.</span><span class="sxs-lookup"><span data-stu-id="6ff0b-139">Once you have a `.nupkg` file, you publish it to nuget.org using the `push` command.</span></span> <span data-ttu-id="6ff0b-140">(Кроме того, можно использовать [рабочий процесс публикации nuget.org](../create-packages/publish-a-package.md#publish-to-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="6ff0b-140">(Alternately, you can use the [nuget.org publishing workflow](../create-packages/publish-a-package.md#publish-to-nugetorg).</span></span>

> [!Warning]
> <span data-ttu-id="6ff0b-141">Пакеты, публикуемые на сайте nuget.org, видны всем другим разработчикам.</span><span class="sxs-lookup"><span data-stu-id="6ff0b-141">The packages you publish to nuget.org are publicly visible to other developers.</span></span> <span data-ttu-id="6ff0b-142">Чтобы разместить пакеты частным образом, см. раздел [Размещение пакетов](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="6ff0b-142">To host packages privately, see [Hosting packages](../hosting-packages/overview.md).</span></span>


1. <span data-ttu-id="6ff0b-143">Создайте бесплатную учетную запись на сайте [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) или войдите, если она у вас уже есть.</span><span class="sxs-lookup"><span data-stu-id="6ff0b-143">Create a free account on [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), or log in if you already have one.</span></span> <span data-ttu-id="6ff0b-144">При создании учетной записи вам направляется сообщение электронной почты с подтверждением.</span><span class="sxs-lookup"><span data-stu-id="6ff0b-144">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="6ff0b-145">Перед отправкой пакета вам нужно подтвердить учетную запись.</span><span class="sxs-lookup"><span data-stu-id="6ff0b-145">You must confirm the account before you can upload a package.</span></span>

1. <span data-ttu-id="6ff0b-146">После входа выберите свое имя пользователя (в правом верхнем углу) и затем пункт **Ключи API**.</span><span class="sxs-lookup"><span data-stu-id="6ff0b-146">Once logged in, select your user name (on the upper right), then select **API Keys**.</span></span>

1. <span data-ttu-id="6ff0b-147">Выберите **Создать**, укажите имя для ключа, выберите **Выбрать области > Отправить** в области **Ключ API**, введите * в поле **Glob pattern** (Стандартная маска), а затем выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="6ff0b-147">Select **Create**, provide a name for your key, select **Select Scopes > Push**Under **API Key**, enter * for **Glob pattern**, then select **Create**.</span></span>

1. <span data-ttu-id="6ff0b-148">После создания ключа выберите **Копировать** для получения ключа доступа, который потребуется в интерфейсе командной строки:</span><span class="sxs-lookup"><span data-stu-id="6ff0b-148">Once the key is created, select **Copy** to retrieve the access key you'll need in the CLI:</span></span>

    ![Копирование ключа API в буфер обмена](media/QS_Create-02-APIKey.png)

    > [!Warning]
    > <span data-ttu-id="6ff0b-150">Сохраните ключ в безопасном месте и не сообщайте никому.</span><span class="sxs-lookup"><span data-stu-id="6ff0b-150">Save your key in a secure location and keep is a secret.</span></span> <span data-ttu-id="6ff0b-151">Если ваш ключ будет случайно раскрыт, вы можете создать его повторно в любое время.</span><span class="sxs-lookup"><span data-stu-id="6ff0b-151">If your key is accidentally revealed, you can always regenerate it at any time.</span></span> <span data-ttu-id="6ff0b-152">Вы также можете удалить ключ API, если больше не хотите отправлять пакеты через интерфейс командной строки.</span><span class="sxs-lookup"><span data-stu-id="6ff0b-152">You can also remove the API key if you no longer want to push packages via the CLI.</span></span>

1. <span data-ttu-id="6ff0b-153">В командной строке выполните следующую команду, указав имя пакета и заменив ключ на значение, скопированное на шаге 4:</span><span class="sxs-lookup"><span data-stu-id="6ff0b-153">At a command prompt, run the following command, specifying your package name and replacing the key with the value copied in step 4:</span></span>

    ```
    nuget push AppLogger.1.0.0.0.nupkg 47be3377-c434-4c29-8576-af7f6993a54b -Source https://api.nuget.org/v3/index.json
    ```
    
1. <span data-ttu-id="6ff0b-154">nuget.exe отображает результаты публикации:</span><span class="sxs-lookup"><span data-stu-id="6ff0b-154">nuget.exe displays the results of the publishing process:</span></span>

    ```
    Pushing AppLogger.1.0.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed. 
    ```

1. <span data-ttu-id="6ff0b-155">В своем профиле на сайте nuget.org выберите **Управление пакетами**, чтобы отобразить опубликованный вами пакет.</span><span class="sxs-lookup"><span data-stu-id="6ff0b-155">From your profile on nuget.org, Select **Manage Packages** to see the one you just published.</span></span> <span data-ttu-id="6ff0b-156">Вы также получите подтверждение по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="6ff0b-156">You also receive a confirmation email.</span></span> <span data-ttu-id="6ff0b-157">Обратите внимание, что пакет индексируется и будет появляться в результатах поиска для других пользователей спустя определенное время.</span><span class="sxs-lookup"><span data-stu-id="6ff0b-157">Note that it might take a while for your package to be indexed and appear in search results where others can find it.</span></span> <span data-ttu-id="6ff0b-158">В этот период на странице вашего пакета отображается следующее сообщение:</span><span class="sxs-lookup"><span data-stu-id="6ff0b-158">During that time your package page shows the message below:</span></span>

    ![This package has not been indexed yet.](media/QS_Create-03-NotIndexed.png)

> [!Note]
> <span data-ttu-id="6ff0b-161">**Проверка на вирусы**: перед публикацией все пакеты, загружаемые на веб-сайт nuget.org, проверяются на вирусы, и в случае обнаружения вирусов отклоняются.</span><span class="sxs-lookup"><span data-stu-id="6ff0b-161">**Virus scanning**: All packages uploaded to nuget.org are scanned for viruses and rejected if any viruses are found.</span></span> <span data-ttu-id="6ff0b-162">Кроме того, периодическую проверку проходят все пакеты, представленные на веб-сайте nuget.org.</span><span class="sxs-lookup"><span data-stu-id="6ff0b-162">All packages listed on nuget.org are also scanned periodically.</span></span>

<span data-ttu-id="6ff0b-163">Вот и все!</span><span class="sxs-lookup"><span data-stu-id="6ff0b-163">And that's it!</span></span> <span data-ttu-id="6ff0b-164">Вы только что опубликовали на сайте [nuget.org](https://www.nuget.org/) свой первый пакет NuGet, который другие разработчики могут использовать в своих собственных проектах.</span><span class="sxs-lookup"><span data-stu-id="6ff0b-164">You've just published your first NuGet package to [nuget.org](https://www.nuget.org/), that other developers can use in their own projects.</span></span>

## <a name="related-topics"></a><span data-ttu-id="6ff0b-165">См. также</span><span class="sxs-lookup"><span data-stu-id="6ff0b-165">Related topics</span></span>

- [<span data-ttu-id="6ff0b-166">Создание пакета</span><span class="sxs-lookup"><span data-stu-id="6ff0b-166">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="6ff0b-167">Публикация пакета</span><span class="sxs-lookup"><span data-stu-id="6ff0b-167">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="6ff0b-168">Поддержка нескольких целевых платформ</span><span class="sxs-lookup"><span data-stu-id="6ff0b-168">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="6ff0b-169">Управление версиями пакета</span><span class="sxs-lookup"><span data-stu-id="6ff0b-169">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="6ff0b-170">Создание локализованных пакетов</span><span class="sxs-lookup"><span data-stu-id="6ff0b-170">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)