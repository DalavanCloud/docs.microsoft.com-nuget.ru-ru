---
title: "Служба индекс, NuGet API | Документы Microsoft"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Служба индекс является точкой входа NuGet HTTP API и перечисляет возможности сервера."
keywords: "Точка входа NuGet API, NuGetA PI обнаружения конечной точки"
ms.reviewer:
- karann
- unnir
ms.openlocfilehash: 9d0bb421c163520df4a1f0e9f3f71aab823aace3
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2018
---
# <a name="service-index"></a><span data-ttu-id="e2820-104">Служба индекс.</span><span class="sxs-lookup"><span data-stu-id="e2820-104">Service index</span></span>

<span data-ttu-id="e2820-105">Индекс службы является документом JSON, — это точка входа для источника пакета NuGet и позволяет ознакомиться с возможностями источника пакета реализации клиента.</span><span class="sxs-lookup"><span data-stu-id="e2820-105">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="e2820-106">Служба индекс — это объект JSON со два обязательных свойства: `version` (версия схемы индекса службы) и `resources` (конечные точки или возможностях исходного пакета).</span><span class="sxs-lookup"><span data-stu-id="e2820-106">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="e2820-107">Индекс службы NuGet.org находится в каталоге `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="e2820-107">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="e2820-108">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="e2820-108">Versioning</span></span>

<span data-ttu-id="e2820-109">`version` Значение представляет собой строку непригодными для синтаксического анализа версии SemVer 2.0.0, который указывает версию схемы индекса службы.</span><span class="sxs-lookup"><span data-stu-id="e2820-109">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span>
<span data-ttu-id="e2820-110">API требует, что строка версии имеет номер основной версии `3`.</span><span class="sxs-lookup"><span data-stu-id="e2820-110">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="e2820-111">Некритических изменений, выполненных в схеме индекса службы, строку версии, дополнительный номер версии увеличивается.</span><span class="sxs-lookup"><span data-stu-id="e2820-111">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="e2820-112">Каждый ресурс в индексе службы с версиями, независимо от версии службы индекса схемы.</span><span class="sxs-lookup"><span data-stu-id="e2820-112">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="e2820-113">Текущая версия схемы `3.0.0-beta.1`.</span><span class="sxs-lookup"><span data-stu-id="e2820-113">The current schema version is `3.0.0-beta.1`.</span></span>

## <a name="http-methods"></a><span data-ttu-id="e2820-114">Методы HTTP</span><span class="sxs-lookup"><span data-stu-id="e2820-114">HTTP methods</span></span>

<span data-ttu-id="e2820-115">Индекс службы можно получить через HTTP-методов `GET` и `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="e2820-115">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="e2820-116">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="e2820-116">Resources</span></span>

<span data-ttu-id="e2820-117">`resources` Свойство содержит массив ресурсов, поддерживаемые источником этого пакета.</span><span class="sxs-lookup"><span data-stu-id="e2820-117">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="e2820-118">Ресурс</span><span class="sxs-lookup"><span data-stu-id="e2820-118">Resource</span></span>

<span data-ttu-id="e2820-119">Ресурс — это объект в `resources` массива.</span><span class="sxs-lookup"><span data-stu-id="e2820-119">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="e2820-120">Он представляет функцию с версиями источника пакета.</span><span class="sxs-lookup"><span data-stu-id="e2820-120">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="e2820-121">Ресурс имеет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="e2820-121">A resource has the following properties:</span></span>

<span data-ttu-id="e2820-122">name</span><span class="sxs-lookup"><span data-stu-id="e2820-122">Name</span></span>          | <span data-ttu-id="e2820-123">Тип</span><span class="sxs-lookup"><span data-stu-id="e2820-123">Type</span></span>   | <span data-ttu-id="e2820-124">Обязательно</span><span class="sxs-lookup"><span data-stu-id="e2820-124">Required</span></span> | <span data-ttu-id="e2820-125">Примечания</span><span class="sxs-lookup"><span data-stu-id="e2820-125">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="e2820-126">string</span><span class="sxs-lookup"><span data-stu-id="e2820-126">string</span></span> | <span data-ttu-id="e2820-127">да</span><span class="sxs-lookup"><span data-stu-id="e2820-127">yes</span></span>      | <span data-ttu-id="e2820-128">URL-адрес ресурса</span><span class="sxs-lookup"><span data-stu-id="e2820-128">The URL to the resource</span></span>
@type         | <span data-ttu-id="e2820-129">string</span><span class="sxs-lookup"><span data-stu-id="e2820-129">string</span></span> | <span data-ttu-id="e2820-130">да</span><span class="sxs-lookup"><span data-stu-id="e2820-130">yes</span></span>      | <span data-ttu-id="e2820-131">Строковая константа, представляющая тип ресурса</span><span class="sxs-lookup"><span data-stu-id="e2820-131">A string constant representing the resource type</span></span>
<span data-ttu-id="e2820-132">комментарий</span><span class="sxs-lookup"><span data-stu-id="e2820-132">comment</span></span>       | <span data-ttu-id="e2820-133">string</span><span class="sxs-lookup"><span data-stu-id="e2820-133">string</span></span> | <span data-ttu-id="e2820-134">Нет</span><span class="sxs-lookup"><span data-stu-id="e2820-134">no</span></span>       | <span data-ttu-id="e2820-135">Понятное описание ресурса</span><span class="sxs-lookup"><span data-stu-id="e2820-135">A human readable description of the resource</span></span>

<span data-ttu-id="e2820-136">`@id` : URL-адрес, который должен быть абсолютным и должен либо иметь схемы HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e2820-136">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="e2820-137">`@type` Используется для идентификации конкретного протокола для использования при взаимодействии с ресурсом.</span><span class="sxs-lookup"><span data-stu-id="e2820-137">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="e2820-138">Тип ресурса непрозрачная строка, но обычно имеет следующий формат:</span><span class="sxs-lookup"><span data-stu-id="e2820-138">The type of the resource is an opaque string but generally has the format:</span></span>

    {RESOURCE_NAME}/{RESOURCE_VERSION}

<span data-ttu-id="e2820-139">Клиенты должны жестко `@type` значения их понимания и находить их в индексе источник пакета службы.</span><span class="sxs-lookup"><span data-stu-id="e2820-139">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="e2820-140">Точное `@type` значения в настоящее время выполняется перечисление на конкретный ресурс справочные документы, перечисленные в [Обзор интерфейса API](overview.md#resources-and-schema).</span><span class="sxs-lookup"><span data-stu-id="e2820-140">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="e2820-141">Для обеспечения этой документации, документацию по различным ресурсам по существу группируются по `{RESOURCE_NAME}` найден в индексе службы, который является аналогом группирования по сценарию.</span><span class="sxs-lookup"><span data-stu-id="e2820-141">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="e2820-142">Не требуется, чтобы каждый ресурс имеет уникальный `@id` или `@type`.</span><span class="sxs-lookup"><span data-stu-id="e2820-142">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="e2820-143">Это зависит от реализации клиента, чтобы определить, какие ресурсы предпочитают на другое.</span><span class="sxs-lookup"><span data-stu-id="e2820-143">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="e2820-144">Является одной из возможных реализаций, ресурсы одинаковые или совместимые `@type` может использоваться в циклического перебора, в случае сбоя или сервера ошибка подключения.</span><span class="sxs-lookup"><span data-stu-id="e2820-144">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="e2820-145">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="e2820-145">Sample request</span></span>

<span data-ttu-id="e2820-146">GET https://api.nuget.org/v3/index.json</span><span class="sxs-lookup"><span data-stu-id="e2820-146">GET https://api.nuget.org/v3/index.json</span></span>

### <a name="sample-response"></a><span data-ttu-id="e2820-147">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="e2820-147">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
