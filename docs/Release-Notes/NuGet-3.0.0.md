---
title: "Заметки о выпуске NuGet 3.0 | Документы Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Заметки о выпуске для NuGet 3.0.0, включая известные проблемы, исправленные ошибки, добавленные функции и DCR."
keywords: "NuGet 3.0.0 заметки о выпуске, исправления, известными проблемами, добавлены функции, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ef8557c37105eb7915919c7b15d41d024921761f
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="b0429-104">Заметки о выпуске 3.0 NuGet</span><span class="sxs-lookup"><span data-stu-id="b0429-104">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="b0429-105">[Заметки о выпуске версии-кандидата 2 NuGet 3.0](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 заметки о выпуске](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="b0429-105">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="b0429-106">NuGet 3.0 как расширение пакета Visual Studio 2015 был выпущен 20 июля 2015 г.</span><span class="sxs-lookup"><span data-stu-id="b0429-106">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="b0429-107">Мы помещено доставки этой версии с Visual Studio, чтобы процесс завершения обновленные NuGet 3.0 будет доступен для новых пользователей Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b0429-107">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="b0429-108">Эта версия расширения NuGet доступна только для Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="b0429-108">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="b0429-109">Мы рекомендуем разработчиков, которые имеют доступ к коллекции Visual Studio обновление до последней версии, которая доступна, как мы публикуем обновления вскоре после выпуска Visual Studio 2015, который включает в себя поддержку для разработки приложений Windows 10.</span><span class="sxs-lookup"><span data-stu-id="b0429-109">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="b0429-110">В итоге мы закрытых 240 проблем в версии 3.0, и можно будет просмотреть [полный список проблем на GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="b0429-110">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="b0429-111">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="b0429-111">Known Issues</span></span>

<span data-ttu-id="b0429-112">Несколько известных проблем, присутствующие в этом выпуске, и все эти элементы являются исправлено в нашем запланированных 3.1 совпадают с выпуска Windows 10 29 июля.</span><span class="sxs-lookup"><span data-stu-id="b0429-112">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="b0429-113">Можно обновить расширение Visual Studio из коллекции в течение или после этой даты, чтобы устранить эти проблемы.</span><span class="sxs-lookup"><span data-stu-id="b0429-113">You will be able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="b0429-114">Перевод для метки «Больше не показывать» в окне предварительного просмотра и метка «Авторы» в окне описания пакета не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="b0429-114">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="b0429-115">Если при работе над проектом с помощью TFS система управления версиями, NuGet нельзя представить диспетчер пакетов пользовательский интерфейс при Nuget.Config файл помечен как доступный только для чтения.</span><span class="sxs-lookup"><span data-stu-id="b0429-115">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="b0429-116">**Инструкции по решению** извлечь файл из Team Foundation Server.</span><span class="sxs-lookup"><span data-stu-id="b0429-116">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="b0429-117">Текст в желтый «перезапуск панель» в окне NuGet Powershell не отображается при использовании темной темами Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b0429-117">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="b0429-118">**Инструкции по решению** использование светлого оформления Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b0429-118">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="b0429-119">Сводка по верхней устранения проблем</span><span class="sxs-lookup"><span data-stu-id="b0429-119">Summary of top issues resolved</span></span>

* [<span data-ttu-id="b0429-120">Обновления сети часто вызывается, когда обновляет окно диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="b0429-120">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="b0429-121">Отложенная прокрутки установленные изменение на представление в диспетчере пакетов</span><span class="sxs-lookup"><span data-stu-id="b0429-121">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="b0429-122">Сетевые вызовы должны выполняться в фоновом потоке</span><span class="sxs-lookup"><span data-stu-id="b0429-122">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="b0429-123">Добавить флажок «Больше не показывать окно предварительного просмотра»</span><span class="sxs-lookup"><span data-stu-id="b0429-123">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="b0429-124">Добавленный процесс регулирования для уменьшения использования процессора</span><span class="sxs-lookup"><span data-stu-id="b0429-124">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="b0429-125">Улучшенная обработка библиотек классов portable ссылки</span><span class="sxs-lookup"><span data-stu-id="b0429-125">Improved portable-class-library reference handling</span></span>
    * [<span data-ttu-id="b0429-126">https://github.com/NuGet/Home/issues/562</span><span class="sxs-lookup"><span data-stu-id="b0429-126">https://github.com/NuGet/Home/issues/562</span></span>](https://github.com/NuGet/Home/issues/562)
    * [<span data-ttu-id="b0429-127">https://github.com/NuGet/Home/issues/454</span><span class="sxs-lookup"><span data-stu-id="b0429-127">https://github.com/NuGet/Home/issues/454</span></span>](https://github.com/NuGet/Home/issues/454)
    * [<span data-ttu-id="b0429-128">https://github.com/NuGet/Home/issues/440</span><span class="sxs-lookup"><span data-stu-id="b0429-128">https://github.com/NuGet/Home/issues/440</span></span>](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="b0429-129">Автозаполнение служба была с учетом регистра</span><span class="sxs-lookup"><span data-stu-id="b0429-129">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="b0429-130">Обновления, чтобы повторно ввести учетные данные Обычная проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="b0429-130">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="b0429-131">Улучшенная Ошибка ведения журнала</span><span class="sxs-lookup"><span data-stu-id="b0429-131">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="b0429-132">Powershell улучшенные сообщения об ошибках при вызове пакета обновления</span><span class="sxs-lookup"><span data-stu-id="b0429-132">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* [<span data-ttu-id="b0429-133">Исправлена ссылку «Дополнительные сведения о параметрах», чтобы предотвратить сбой в Windows 10</span><span class="sxs-lookup"><span data-stu-id="b0429-133">Fixed the 'Learn about Options' link to prevent crashing on Windows 10</span></span>](https://github.com/NuGet/Home/issues/822)
* [<span data-ttu-id="b0429-134">Следует помнить флажок предварительного выпуска параметр</span><span class="sxs-lookup"><span data-stu-id="b0429-134">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="b0429-135">Улучшенная сбора производительности путем кэширования результатов между проектами в решении</span><span class="sxs-lookup"><span data-stu-id="b0429-135">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="b0429-136">Параллельно можно собрать несколько пакетов</span><span class="sxs-lookup"><span data-stu-id="b0429-136">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="b0429-137">Удалить пакет установки-force команды</span><span class="sxs-lookup"><span data-stu-id="b0429-137">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="b0429-138">Пожалуйста, обратите внимание на [наш блог](http://blog.nuget.org) дополнительные хода выполнения и объявления как мы получаем готовы к предоставлению поддержка разработки Windows 10.</span><span class="sxs-lookup"><span data-stu-id="b0429-138">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>