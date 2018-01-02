---
title: "Преобразования исходного кода и файла конфигурации для пакетов NuGet | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 4/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 20991d69-9e2e-4881-bbf2-96ae634e1872
description: "Сведения о возможности преобразования исходного кода и файлов конфигурации в формате XML для пакетов NuGet при установке."
keywords: "установка пакета NuGet, преобразования пакета NuGet, изменение файлов конфигурации, изменение исходного кода"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: 7d380b7f2ff52ec39a2ac9a2b939ee51db6054f3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="transforming-source-code-and-configuration-files"></a><span data-ttu-id="6c982-104">Преобразования исходного кода и файлов конфигурации</span><span class="sxs-lookup"><span data-stu-id="6c982-104">Transforming source code and configuration files</span></span>

<span data-ttu-id="6c982-105">Для проектов, использующих `packages.config` или `project.json`, NuGet поддерживает возможность выполнять преобразования исходного кода и файлов конфигурации при установке или удалении пакета.</span><span class="sxs-lookup"><span data-stu-id="6c982-105">For projects using `packages.config` or `project.json`, NuGet supports the ability to make transformations to source code and configuration files at package install and uninstall times.</span></span>

> [!Note]
> <span data-ttu-id="6c982-106">Преобразования исходного кода и файла конфигурации не применяются при установке пакета в проект с использованием [ссылок на пакеты в файлах проекта](../Consume-Packages/Package-References-in-Project-Files.md).</span><span class="sxs-lookup"><span data-stu-id="6c982-106">Source and configuration file transformations are not applied when a package is installed in a project using [Package References in project files](../Consume-Packages/Package-References-in-Project-Files.md).</span></span> 

<span data-ttu-id="6c982-107">**Преобразование исходного кода** применяет одностороннюю замену маркера к файлам в папке `content` пакета при установке пакета в тех случаях, когда маркеры ссылаются на [свойства проекта](https://msdn.microsoft.com/library/vslangproj.projectproperties_properties.aspx) Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6c982-107">A **source code transformation** applies one-way token replacement to files in the package's `content` folder when the package is installed, where tokens refer to Visual Studio [project properties](https://msdn.microsoft.com/library/vslangproj.projectproperties_properties.aspx).</span></span> <span data-ttu-id="6c982-108">Это позволяет вставить файл в пространство имен проекта или настроить код, который обычно обращается к `global.asax` в проекте ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="6c982-108">This allows you to insert a file into the project's namespace, or to customize code that would typically go into `global.asax` in an ASP.NET project.</span></span>

<span data-ttu-id="6c982-109">**Преобразование файла конфигурации** позволяет изменять файлы, уже существующие в целевом проекте, такие как `web.config` и `app.config`.</span><span class="sxs-lookup"><span data-stu-id="6c982-109">A **config file transformation** allows you to modify files that already exist in a target project, such as `web.config` and `app.config`.</span></span> <span data-ttu-id="6c982-110">Например, для пакета может потребоваться добавить элемент в раздел `modules` файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6c982-110">For example, your package might need to add an item to the `modules` section in the config file.</span></span> <span data-ttu-id="6c982-111">Это преобразование осуществляется путем включения в пакет особых файлов, которые описывают разделы, добавляемые в файлы конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6c982-111">This transformation is done by including special files in the package that describe the sections to add to the configuration files.</span></span> <span data-ttu-id="6c982-112">При удалении пакета внесенные изменения отменяются, благодаря чему это преобразование является двусторонним.</span><span class="sxs-lookup"><span data-stu-id="6c982-112">When a package is uninstalled, those same changes are then reversed, making this a two-way transformation.</span></span>


## <a name="specifying-source-code-transformations"></a><span data-ttu-id="6c982-113">Определение преобразований исходного кода</span><span class="sxs-lookup"><span data-stu-id="6c982-113">Specifying source code transformations</span></span>

1. <span data-ttu-id="6c982-114">Файлы, которые требуется вставить в проект из пакета, должны располагаться в папке `content` пакета.</span><span class="sxs-lookup"><span data-stu-id="6c982-114">Files that you want to insert from the package into the project must be located within the package's `content` folder.</span></span> <span data-ttu-id="6c982-115">Например, если требуется установить файл `ContosoData.cs` в папку `Models` целевого проекта, этот файл должен находиться в папке `content\Models` пакета.</span><span class="sxs-lookup"><span data-stu-id="6c982-115">For example, if you want a file called `ContosoData.cs` to be installed in a `Models` folder of the target project, it must be inside the `content\Models` folder in the package.</span></span>

2. <span data-ttu-id="6c982-116">Чтобы задать в NuGet инструкцию для применения замены маркера во время установки, добавьте к имени файла исходного кода расширение `.pp`.</span><span class="sxs-lookup"><span data-stu-id="6c982-116">To instruct NuGet to apply token replacement at install time, append `.pp` to the source code file name.</span></span> <span data-ttu-id="6c982-117">После установки расширение `.pp` у файла будет удалено.</span><span class="sxs-lookup"><span data-stu-id="6c982-117">After installation, the file will not have the `.pp` extension.</span></span>

    <span data-ttu-id="6c982-118">Например, чтобы выполнить преобразования в `ContosoData.cs`, присвойте файлу в пакете имя `ContosoData.cs.pp`.</span><span class="sxs-lookup"><span data-stu-id="6c982-118">For example, to make transformations in `ContosoData.cs`, name the file in the package `ContosoData.cs.pp`.</span></span> <span data-ttu-id="6c982-119">После установки он будет иметь имя `ContosoData.cs`.</span><span class="sxs-lookup"><span data-stu-id="6c982-119">After installation it will appear as `ContosoData.cs`.</span></span>

3. <span data-ttu-id="6c982-120">В файле исходного кода используйте маркеры без учета регистра символов вида `$token$`, чтобы указать значения, которые NuGet будет заменять свойствами проекта:</span><span class="sxs-lookup"><span data-stu-id="6c982-120">In the source code file, use case-insensitive tokens of the form `$token$` to indicate values that NuGet should replace with project properties:</span></span>

    ```cs
    namespace $rootnamespace$.Models
    {
        public struct CategoryInfo
        {
            public string categoryid;
            public string description;
            public string htmlUrl;
            public string rssUrl;
            public string title;
        }
    }
    ```

    <span data-ttu-id="6c982-121">При установке NuGet заменяет `$rootnamespace$` на `Fabrikam`, используя свойства целевого проекта, корневым пространством имен которого является `Fabrikam`.</span><span class="sxs-lookup"><span data-stu-id="6c982-121">Upon installation, NuGet replaces `$rootnamespace$` with `Fabrikam` assuming the target project's whose root namespace is `Fabrikam`.</span></span>

<span data-ttu-id="6c982-122">Маркер `$rootnamespace$` является одним из самых часто используемых свойств проекта. Остальные маркеры перечислены в разделе [Свойства проекта](https://msdn.microsoft.com/library/vslangproj.projectproperties_properties.aspx) документации на веб-сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="6c982-122">The `$rootnamespace$` token is the most commonly used project property; all others are listed in the [Project Properties](https://msdn.microsoft.com/library/vslangproj.projectproperties_properties.aspx) documentation on MSDN.</span></span> <span data-ttu-id="6c982-123">Естественно, необходимо учитывать, что некоторые свойства могут зависеть от типа проекта.</span><span class="sxs-lookup"><span data-stu-id="6c982-123">Be mindful, of course, that some properties might be specific to the project type.</span></span>


## <a name="specifying-config-file-transformations"></a><span data-ttu-id="6c982-124">Определение преобразований файла конфигурации</span><span class="sxs-lookup"><span data-stu-id="6c982-124">Specifying config file transformations</span></span>

<span data-ttu-id="6c982-125">Как описывается в следующих разделах, преобразования файла конфигурации могут быть выполнены двумя способами:</span><span class="sxs-lookup"><span data-stu-id="6c982-125">As described in the sections that follow, config file transformations can be done in two ways:</span></span>

- <span data-ttu-id="6c982-126">Включите файлы `app.config.transform` и `web.config.transform` в папку `content` пакета. Расширение `.transform` указывает NuGet на то, что эти файлы содержат XML-код, который следует добавить в файлы конфигурации при установке пакета.</span><span class="sxs-lookup"><span data-stu-id="6c982-126">Include `app.config.transform` and `web.config.transform` files in your package's `content` folder, where the `.transform` extension tells NuGet that these files contain the XML to merge with existing config files when the package is installed.</span></span> <span data-ttu-id="6c982-127">При удалении пакета такой XML-код также удаляется.</span><span class="sxs-lookup"><span data-stu-id="6c982-127">When a package is uninstalled, that same XML is removed.</span></span>
- <span data-ttu-id="6c982-128">(NuGet 2.6 и более поздней версии) Включите файлы `app.config.install.xdt` и `web.config.install.xdt` в папку `content` пакета, используя [синтаксис XDT](https://msdn.microsoft.com/library/dd465326.aspx) для описания необходимых изменений.</span><span class="sxs-lookup"><span data-stu-id="6c982-128">(NuGet 2.6 and later) Include `app.config.install.xdt` and `web.config.install.xdt` files in your package's `content` folder, using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx) to describe the desired changes.</span></span> <span data-ttu-id="6c982-129">В этом случае также можно включить файл `.uninstall.xdt`, который необходим для отмены изменений при удалении пакета из проекта.</span><span class="sxs-lookup"><span data-stu-id="6c982-129">With this option you can also include a `.uninstall.xdt` file to reverse changes when the package is removed from a project.</span></span>

> [!Note]
> <span data-ttu-id="6c982-130">Преобразования не применяются к файлам `.config`, на которые задаются ссылки в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6c982-130">Transformations are not applied to `.config` files referenced as a link in Visual Studio.</span></span>

<span data-ttu-id="6c982-131">Преимуществом использования XDT является то, что вместо простого объединения двух файлов предоставляется синтаксис для операций со структурой модели DOM XML с использованием элемента и атрибута, соответствующих применению полной поддержки XPath.</span><span class="sxs-lookup"><span data-stu-id="6c982-131">The advantage of using XDT is that instead of simply merging two static files, it provides a syntax for manipulating the structure of an XML DOM using element and attribute matching using full XPath support.</span></span> <span data-ttu-id="6c982-132">XDT позволяет добавлять, обновлять и удалять элементы, помещать новые элементы в конкретное место, а также заменять или удалять элементы (включая дочерние узлы).</span><span class="sxs-lookup"><span data-stu-id="6c982-132">XDT can then add, update, or remove elements, place new elements at a specific location, or replace/remove elements (including child nodes).</span></span> <span data-ttu-id="6c982-133">Это позволяет легко создавать преобразования при удалении, которые обеспечивают отмену всех преобразований, выполненных во время установки пакета.</span><span class="sxs-lookup"><span data-stu-id="6c982-133">This makes it straightforward to create uninstall transforms that back out all transformations done during package installation.</span></span>

### <a name="xml-transforms"></a><span data-ttu-id="6c982-134">Преобразования XML</span><span class="sxs-lookup"><span data-stu-id="6c982-134">XML transforms</span></span>

<span data-ttu-id="6c982-135">Файлы `app.config.transform` и `web.config.transform` в папке `content` пакета содержат только те элементы, которые будут добавлены в существующие файлы `app.config` и `web.config` проекта.</span><span class="sxs-lookup"><span data-stu-id="6c982-135">The `app.config.transform` and `web.config.transform` in a package's `content` folder contain only those elements to merge into the project's existing `app.config` and `web.config` files.</span></span>

<span data-ttu-id="6c982-136">Допустим, файл `web.config` проекта изначально имеет следующее содержимое:</span><span class="sxs-lookup"><span data-stu-id="6c982-136">As an example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    <system.webServer>
</configuration>
```

<span data-ttu-id="6c982-137">Чтобы добавить элемент `MyNuModule` в раздел `modules` во время установки пакета, создайте файл `web.config.transform` в папке `content` пакета, который будет иметь следующий вид:</span><span class="sxs-lookup"><span data-stu-id="6c982-137">To add a `MyNuModule` element to the `modules` section during package install, create a `web.config.transform` file in the package's `content` folder that looks like this:</span></span>

    
```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    <system.webServer>
</configuration>
```

<span data-ttu-id="6c982-138">После того как NuGet установит пакет, файл `web.config` будет иметь следующий вид:</span><span class="sxs-lookup"><span data-stu-id="6c982-138">After NuGet installs the package, `web.config` will appear as follows:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    <system.webServer>
</configuration>
```

<span data-ttu-id="6c982-139">Обратите внимание, что NuGet не заменяет раздел `modules`, а добавляет в него новую запись с новыми элементами и атрибутами.</span><span class="sxs-lookup"><span data-stu-id="6c982-139">Notice that NuGet didn't replace the `modules` section, it just merged the new entry into it by adding only new elements and attributes.</span></span> <span data-ttu-id="6c982-140">NuGet не изменяет какие-либо существующие элементы или атрибуты.</span><span class="sxs-lookup"><span data-stu-id="6c982-140">NuGet will not change any existing elements or attributes.</span></span>

<span data-ttu-id="6c982-141">При удалении пакета NuGet снова проверяет файлы `.transform` и удаляет содержащиеся в них элементы из соответствующих файлов `.config`.</span><span class="sxs-lookup"><span data-stu-id="6c982-141">When the package is uninstalled, NuGet will examine the `.transform` files again and remove the elements it contains from the appropriate `.config` files.</span></span> <span data-ttu-id="6c982-142">Обратите внимание, что этот процесс не затрагивает строки файла `.config`, которые были изменены после установки пакета.</span><span class="sxs-lookup"><span data-stu-id="6c982-142">Note that this process will not affect any lines in the `.config` file that you modify after package installation.</span></span>

<span data-ttu-id="6c982-143">В качестве расширенного примера можно привести пакет [модулей ведения журнала и обработки ошибок ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/), который добавляет множество записей в файл `web.config`. При удалении пакета эти записи будут удалены.</span><span class="sxs-lookup"><span data-stu-id="6c982-143">As a more extensive example, the [Error Logging Modules and Handlers for ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) package adds many entries into `web.config`, which are again removed when a package is uninstalled.</span></span>

<span data-ttu-id="6c982-144">Чтобы изучить соответствующий файл `web.config.transform`, скачайте пакет ELMAH по приведенной выше ссылке, измените расширение пакета с `.nupkg` на `.zip`, после чего откройте файл `content\web.config.transform`, содержащийся в этом ZIP-файле.</span><span class="sxs-lookup"><span data-stu-id="6c982-144">To examine its `web.config.transform` file, download the ELMAH package from the link above, change the package extension from `.nupkg` to `.zip`, and then open `content\web.config.transform` in that ZIP file.</span></span>

<span data-ttu-id="6c982-145">Чтобы просмотреть последствия установки и удаления пакета, создайте в Visual Studio новый проект ASP.NET (шаблон в разделе **Visual C# > Интернет** диалогового окна "Новый проект") и выберите приложение ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="6c982-145">To see the effect of installing and uninstalling the package, create a new ASP.NET project in Visual Studio (the template is under **Visual C# > Web** in the New Project dialog), and select an empty ASP.NET application.</span></span> <span data-ttu-id="6c982-146">Откройте файл `web.config`, чтобы просмотреть его первоначальное состояние.</span><span class="sxs-lookup"><span data-stu-id="6c982-146">Open `web.config` to see its initial state.</span></span> <span data-ttu-id="6c982-147">Щелкните проект правой кнопкой мыши, выберите пункт **Управление пакетами NuGet**, перейдите к пакету ELMAH на веб-сайте nuget.org и установите его последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="6c982-147">Then right-click the project, select **Manage NuGet Packages**, browse for ELMAH on nuget.org, and install the latest version.</span></span> <span data-ttu-id="6c982-148">Обратите внимание на все изменения в файле `web.config`.</span><span class="sxs-lookup"><span data-stu-id="6c982-148">Notice all the changes to `web.config`.</span></span> <span data-ttu-id="6c982-149">Удалите пакет. Вы увидите, что было восстановлено исходное состояние файла `web.config`.</span><span class="sxs-lookup"><span data-stu-id="6c982-149">Now uninstall the package and you'll see `web.config` revert to its prior state.</span></span>


### <a name="xdt-transforms"></a><span data-ttu-id="6c982-150">Преобразования XDT</span><span class="sxs-lookup"><span data-stu-id="6c982-150">XDT transforms</span></span>

<span data-ttu-id="6c982-151">В NuGet 2.6 и более поздних версий можно изменять файлы конфигурации с помощью [синтаксиса XDT](https://msdn.microsoft.com/library/dd465326.aspx).</span><span class="sxs-lookup"><span data-stu-id="6c982-151">With NuGet 2.6 and later, you can modify config files using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx).</span></span> <span data-ttu-id="6c982-152">Кроме того, NuGet может заменять маркеры [свойствами проекта](https://msdn.microsoft.com/library/vslangproj.projectproperties_properties.aspx), включая имена свойств с разделителями `$` (без учета регистра символов).</span><span class="sxs-lookup"><span data-stu-id="6c982-152">You can also have NuGet replace tokens with [Project Properties](https://msdn.microsoft.com/library/vslangproj.projectproperties_properties.aspx) by including the property name within `$` delimeters (case-insensitive).</span></span>

<span data-ttu-id="6c982-153">Например, следующий файл `app.config.install.xdt` вставит элемент `appSettings` в файл `app.config`, содержащий значения `FullPath`, `FileName` и `ActiveConfigurationSettings` из проекта:</span><span class="sxs-lookup"><span data-stu-id="6c982-153">For example, the following `app.config.install.xdt` file will insert an `appSettings` element into `app.config` containing the `FullPath`, `FileName`, and `ActiveConfigurationSettings` values from the project:</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <appSettings xdt:Transform="Insert">
        <add key="FullPath" value="$FullPath$" />
        <add key="FileName" value="$filename$" />
        <add key="ActiveConfigurationSettings " value="$ActiveConfigurationSettings$" />
    </appSettings>
</configuration>
```

<span data-ttu-id="6c982-154">Предположим, файл `web.config` проекта изначально имеет следующее содержимое:</span><span class="sxs-lookup"><span data-stu-id="6c982-154">For another example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    <system.webServer>
</configuration>
```

<span data-ttu-id="6c982-155">Чтобы добавить элемент `MyNuModule` в раздел `modules` при установке пакета, файл `web.config.install.xdt` пакета должен иметь следующее содержимое:</span><span class="sxs-lookup"><span data-stu-id="6c982-155">To add a `MyNuModule` element to the `modules` section during package install, the package's `web.config.install.xdt` would contain the following:</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" xdt:Transform="Insert" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="6c982-156">После установки пакета файл `web.config` будет иметь следующий вид:</span><span class="sxs-lookup"><span data-stu-id="6c982-156">After installing the package, `web.config` will look like this:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    <system.webServer>
</configuration>
```

<span data-ttu-id="6c982-157">Чтобы удалить только элемент `MyNuModule` во время удаления пакета, файл `web.config.uninstall.xdt` должен иметь следующее содержимое:</span><span class="sxs-lookup"><span data-stu-id="6c982-157">To remove only the `MyNuModule` element during package uninstall, the `web.config.uninstall.xdt` file should contain the following:</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <system.webServer>
        <modules>
            <add name="MyNuModule" xdt:Transform="Remove" xdt:Locator="Match(name)" />
        </modules>
    </system.webServer>
</configuration>
```