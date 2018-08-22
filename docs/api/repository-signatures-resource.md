---
title: Репозиторий Signatures, NuGet API | Документация Майкрософт
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 3/2/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Ресурс подписи репозиторий позволяет клиентам источники пакетов рады сообщить о их репозитории, подписи возможности.
keywords: NuGet API репозитория signatures, nuget.org, сертификатов подписи, подписание пакета nuget.org
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 27c572a482fef791f19b3d32e816a41d8dc40b53
ms.sourcegitcommit: e9c58dbfc1af2876337dcc37b1b070e8ddec0388
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/09/2018
ms.locfileid: "40020565"
---
# <a name="repository-signatures"></a><span data-ttu-id="91ace-104">Репозиторий подписи</span><span class="sxs-lookup"><span data-stu-id="91ace-104">Repository signatures</span></span>

<span data-ttu-id="91ace-105">Если источник пакета поддерживает добавление подписей репозитория для опубликованных пакетов, можно для клиента определить сертификаты для подписи, используемые в источнике пакета.</span><span class="sxs-lookup"><span data-stu-id="91ace-105">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="91ace-106">Этот ресурс позволяет клиентам обнаруживать репозиторием подписи пакета было изменено или имеет непредвиденный сертификат для подписи.</span><span class="sxs-lookup"><span data-stu-id="91ace-106">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="91ace-107">Ресурс, используемый для получения сведения о подписи этот репозиторий является `RepositorySignatures` найти ресурс в [индекс службы](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="91ace-107">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

> [!Note]
> <span data-ttu-id="91ace-108">Запускает NuGet.org объявляет о `RepositorySignatures` ресурсов в ближайшем будущем.</span><span class="sxs-lookup"><span data-stu-id="91ace-108">NuGet.org will start announcing the `RepositorySignatures` resource in the near future.</span></span>

## <a name="versioning"></a><span data-ttu-id="91ace-109">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="91ace-109">Versioning</span></span>

<span data-ttu-id="91ace-110">Следующие `@type` используется значение:</span><span class="sxs-lookup"><span data-stu-id="91ace-110">The following `@type` value is used:</span></span>

<span data-ttu-id="91ace-111">Значение @type</span><span class="sxs-lookup"><span data-stu-id="91ace-111">@type value</span></span>                | <span data-ttu-id="91ace-112">Примечания</span><span class="sxs-lookup"><span data-stu-id="91ace-112">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="91ace-113">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="91ace-113">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="91ace-114">Первоначальный выпуск</span><span class="sxs-lookup"><span data-stu-id="91ace-114">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="91ace-115">Базовый URL-адрес</span><span class="sxs-lookup"><span data-stu-id="91ace-115">Base URL</span></span>

<span data-ttu-id="91ace-116">URL-адрес точки входа для следующих API-интерфейсов является значением `@id` свойство, связанное с ресурсом, упомянутых выше `@type` значение.</span><span class="sxs-lookup"><span data-stu-id="91ace-116">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="91ace-117">В этом разделе используется заполнитель URL-адреса `{@id}`.</span><span class="sxs-lookup"><span data-stu-id="91ace-117">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="91ace-118">Обратите внимание, что в отличие от других ресурсов, `{@id}` URL-адрес необходим обслуживаются по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="91ace-118">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="91ace-119">Методы HTTP</span><span class="sxs-lookup"><span data-stu-id="91ace-119">HTTP methods</span></span>

<span data-ttu-id="91ace-120">Все URL-адресов в ресурсов поддержки только HTTP репозитория сигнатур методов `GET` и `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="91ace-120">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="91ace-121">Индекс подписи репозитория</span><span class="sxs-lookup"><span data-stu-id="91ace-121">Repository signatures index</span></span>

<span data-ttu-id="91ace-122">Индекс подписи репозитория содержит два элемента информации:</span><span class="sxs-lookup"><span data-stu-id="91ace-122">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="91ace-123">Ли найти все пакеты в источнике, подписанные этого источника пакетов репозитория.</span><span class="sxs-lookup"><span data-stu-id="91ace-123">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="91ace-124">Список сертификатов, используемых источника пакета для подписания пакетов.</span><span class="sxs-lookup"><span data-stu-id="91ace-124">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="91ace-125">В большинстве случаев в списке сертификатов будут добавляться только на.</span><span class="sxs-lookup"><span data-stu-id="91ace-125">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="91ace-126">Новые сертификаты следует добавить в список при предыдущий сертификат для подписи истек, и источник пакета должен начать использовать новый сертификат подписи.</span><span class="sxs-lookup"><span data-stu-id="91ace-126">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="91ace-127">Если сертификат удаляется из списка, это означает, что все подписи пакетов, созданных с помощью удален сертификат для подписи больше не считается допустимым клиентом.</span><span class="sxs-lookup"><span data-stu-id="91ace-127">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="91ace-128">В этом случае подпись пакета (но не обязательно пакета) является недопустимым.</span><span class="sxs-lookup"><span data-stu-id="91ace-128">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="91ace-129">Политика клиента может разрешить установку пакета как число без знака.</span><span class="sxs-lookup"><span data-stu-id="91ace-129">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="91ace-130">В случае отзыва сертификатов (например клавиш) источник пакета должен заново подписать все пакеты, подписанные сертификатом уязвимой.</span><span class="sxs-lookup"><span data-stu-id="91ace-130">In the case of certificate revocation (e.g. key compromise), the package source is expected to resign all packages signed by the affected certificate.</span></span> <span data-ttu-id="91ace-131">Кроме того источник пакета следует удалить затронутых сертификат из списка сертификатов подписи.</span><span class="sxs-lookup"><span data-stu-id="91ace-131">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="91ace-132">Следующий запрос извлекает индекс сигнатуры репозитория.</span><span class="sxs-lookup"><span data-stu-id="91ace-132">The following request fetches the repository signatures index.</span></span>

    GET {@id}

<span data-ttu-id="91ace-133">Индекс подписи репозиторий является документ JSON, который содержит объект со следующими свойствами:</span><span class="sxs-lookup"><span data-stu-id="91ace-133">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="91ace-134">name</span><span class="sxs-lookup"><span data-stu-id="91ace-134">Name</span></span>                | <span data-ttu-id="91ace-135">Тип</span><span class="sxs-lookup"><span data-stu-id="91ace-135">Type</span></span>             | <span data-ttu-id="91ace-136">Обязательно</span><span class="sxs-lookup"><span data-stu-id="91ace-136">Required</span></span>
------------------- | ---------------- | --------
<span data-ttu-id="91ace-137">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="91ace-137">allRepositorySigned</span></span> | <span data-ttu-id="91ace-138">boolean</span><span class="sxs-lookup"><span data-stu-id="91ace-138">boolean</span></span>          | <span data-ttu-id="91ace-139">да</span><span class="sxs-lookup"><span data-stu-id="91ace-139">yes</span></span>
<span data-ttu-id="91ace-140">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="91ace-140">signingCertificates</span></span> | <span data-ttu-id="91ace-141">Массив объектов</span><span class="sxs-lookup"><span data-stu-id="91ace-141">array of objects</span></span> | <span data-ttu-id="91ace-142">да</span><span class="sxs-lookup"><span data-stu-id="91ace-142">yes</span></span>

<span data-ttu-id="91ace-143">`allRepositorySigned` Логическое значение присвоено значение false, если источник пакета имеет некоторые пакеты, имеющие подпись отсутствует репозиторий.</span><span class="sxs-lookup"><span data-stu-id="91ace-143">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="91ace-144">Если логическое выражение имеет значение true, все пакеты, доступные на источник должен иметь сигнатуре репозитория, которая создается по одному из сертификатов подписей, упомянутые в `signingCertificates`.</span><span class="sxs-lookup"><span data-stu-id="91ace-144">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

<span data-ttu-id="91ace-145">Должен быть один или несколько сертификатов подписи в `signingCertificates` массив Если `allRepositorySigned` логическое выражение имеет значение в значение true.</span><span class="sxs-lookup"><span data-stu-id="91ace-145">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="91ace-146">Если массив пуст и `allRepositorySigned` имеет значение true, все пакеты из источника должно считаться недействительным, несмотря на то, что политику клиента по-прежнему может разрешить использование пакетов.</span><span class="sxs-lookup"><span data-stu-id="91ace-146">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="91ace-147">Каждый элемент этого массива представляет собой объект JSON со следующими свойствами.</span><span class="sxs-lookup"><span data-stu-id="91ace-147">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="91ace-148">name</span><span class="sxs-lookup"><span data-stu-id="91ace-148">Name</span></span>         | <span data-ttu-id="91ace-149">Тип</span><span class="sxs-lookup"><span data-stu-id="91ace-149">Type</span></span>   | <span data-ttu-id="91ace-150">Обязательно</span><span class="sxs-lookup"><span data-stu-id="91ace-150">Required</span></span> | <span data-ttu-id="91ace-151">Примечания</span><span class="sxs-lookup"><span data-stu-id="91ace-151">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="91ace-152">contentUrl</span><span class="sxs-lookup"><span data-stu-id="91ace-152">contentUrl</span></span>   | <span data-ttu-id="91ace-153">string</span><span class="sxs-lookup"><span data-stu-id="91ace-153">string</span></span> | <span data-ttu-id="91ace-154">да</span><span class="sxs-lookup"><span data-stu-id="91ace-154">yes</span></span>      | <span data-ttu-id="91ace-155">Абсолютный URL-адрес в кодировке DER открытый сертификат</span><span class="sxs-lookup"><span data-stu-id="91ace-155">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="91ace-156">отпечатки пальцев</span><span class="sxs-lookup"><span data-stu-id="91ace-156">fingerprints</span></span> | <span data-ttu-id="91ace-157">object</span><span class="sxs-lookup"><span data-stu-id="91ace-157">object</span></span> | <span data-ttu-id="91ace-158">да</span><span class="sxs-lookup"><span data-stu-id="91ace-158">yes</span></span>      |
<span data-ttu-id="91ace-159">Тема</span><span class="sxs-lookup"><span data-stu-id="91ace-159">subject</span></span>      | <span data-ttu-id="91ace-160">string</span><span class="sxs-lookup"><span data-stu-id="91ace-160">string</span></span> | <span data-ttu-id="91ace-161">да</span><span class="sxs-lookup"><span data-stu-id="91ace-161">yes</span></span>      | <span data-ttu-id="91ace-162">Различающееся имя субъекта из сертификата</span><span class="sxs-lookup"><span data-stu-id="91ace-162">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="91ace-163">issuer</span><span class="sxs-lookup"><span data-stu-id="91ace-163">issuer</span></span>       | <span data-ttu-id="91ace-164">string</span><span class="sxs-lookup"><span data-stu-id="91ace-164">string</span></span> | <span data-ttu-id="91ace-165">да</span><span class="sxs-lookup"><span data-stu-id="91ace-165">yes</span></span>      | <span data-ttu-id="91ace-166">Различающееся имя издателя сертификата</span><span class="sxs-lookup"><span data-stu-id="91ace-166">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="91ace-167">notBefore</span><span class="sxs-lookup"><span data-stu-id="91ace-167">notBefore</span></span>    | <span data-ttu-id="91ace-168">string</span><span class="sxs-lookup"><span data-stu-id="91ace-168">string</span></span> | <span data-ttu-id="91ace-169">да</span><span class="sxs-lookup"><span data-stu-id="91ace-169">yes</span></span>      | <span data-ttu-id="91ace-170">Метка времени начала срока действия сертификата</span><span class="sxs-lookup"><span data-stu-id="91ace-170">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="91ace-171">notAfter</span><span class="sxs-lookup"><span data-stu-id="91ace-171">notAfter</span></span>     | <span data-ttu-id="91ace-172">string</span><span class="sxs-lookup"><span data-stu-id="91ace-172">string</span></span> | <span data-ttu-id="91ace-173">да</span><span class="sxs-lookup"><span data-stu-id="91ace-173">yes</span></span>      | <span data-ttu-id="91ace-174">Отметка времени окончания срока действия сертификата</span><span class="sxs-lookup"><span data-stu-id="91ace-174">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="91ace-175">Обратите внимание, что `contentUrl` должен обслуживаться по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="91ace-175">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="91ace-176">Этот URL-адрес имеет не определенному шаблону URL-адрес и должны быть динамически обнаружены при с помощью этого документа репозитория сигнатуры индекса.</span><span class="sxs-lookup"><span data-stu-id="91ace-176">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="91ace-177">Все свойства в этом объекте (помимо `contentUrl`) должен быть производное от сертификата, расположенный `contentUrl`.</span><span class="sxs-lookup"><span data-stu-id="91ace-177">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="91ace-178">Эти производное свойства предоставляются для удобства, чтобы свести к минимуму циклами.</span><span class="sxs-lookup"><span data-stu-id="91ace-178">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="91ace-179">`fingerprints` Объект имеет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="91ace-179">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="91ace-180">name</span><span class="sxs-lookup"><span data-stu-id="91ace-180">Name</span></span>                   | <span data-ttu-id="91ace-181">Тип</span><span class="sxs-lookup"><span data-stu-id="91ace-181">Type</span></span>   | <span data-ttu-id="91ace-182">Обязательно</span><span class="sxs-lookup"><span data-stu-id="91ace-182">Required</span></span> | <span data-ttu-id="91ace-183">Примечания</span><span class="sxs-lookup"><span data-stu-id="91ace-183">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="91ace-184">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="91ace-184">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="91ace-185">string</span><span class="sxs-lookup"><span data-stu-id="91ace-185">string</span></span> | <span data-ttu-id="91ace-186">да</span><span class="sxs-lookup"><span data-stu-id="91ace-186">yes</span></span>      | <span data-ttu-id="91ace-187">Отпечаток SHA-256</span><span class="sxs-lookup"><span data-stu-id="91ace-187">The SHA-256 fingerprint</span></span>

<span data-ttu-id="91ace-188">Имя ключа `2.16.840.1.101.3.4.2.1` — это идентификатор Объекта хэш-алгоритма SHA-256.</span><span class="sxs-lookup"><span data-stu-id="91ace-188">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="91ace-189">Все значения хэша должны быть строчные буквы, шестнадцатеричной кодировке строковые представления дайджест хэша.</span><span class="sxs-lookup"><span data-stu-id="91ace-189">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="91ace-190">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="91ace-190">Sample request</span></span>

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a><span data-ttu-id="91ace-191">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="91ace-191">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]