---
title: "Протоколы NuGet.org | Документы Microsoft"
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 10/30/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: ba1d9742-9f1c-42ff-8c30-8e953e23c501
description: "Протоколы развивающейся nuget.org взаимодействовать с клиентами NuGet."
ms.reviewer:
- kraigb
- karann-msft
ms.openlocfilehash: 097b7a86d056b692c52d6de76bc2fb99d1b58c6f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="nugetorg-protocols"></a>Протоколы NuGet.org

Для взаимодействия с nuget.org, клиенты должны следовать определенным протоколам. Так как эти протоколы сохранить развиваться, клиенты необходимо определить версию протокола, которые они используют при вызове конкретного nuget.org API-интерфейсы. Это позволяет nuget.org необходимо ввести изменения в виде неразрывные старые клиенты.

> [!Note]
> Интерфейсы API, описанных на этой странице относятся к nuget.org и нет никаких предположений относительного других реализациях серверов NuGet представить эти API-интерфейсы. 

Сведения об API NuGet, широко осуществляемая экосистема NuGet см. в разделе [Обзор интерфейса API](overview.md).

В этом разделе перечислены различные протоколы, как и когда они поступают существование.

## <a name="nuget-protocol-version-410"></a>Версия протокола NuGet 4.1.0

4.1.0 протокола задает использование ключей проверки области для взаимодействия со службами, отличные от nuget.org, чтобы проверить пакет учетной записи nuget.org. Обратите внимание, что `4.1.0` версия номер непрозрачная строка, но происходит совпадать с первой версии официальный NuGet клиента, который поддерживает этот протокол.

Проверка гарантирует, что API ключей, созданных пользователем используются только вместе с nuget.org и этой проверки или проверки службы сторонних осуществляется при помощи ключей проверки области однократного использования. Эти ключи проверки области можно использовать для проверки пакета принадлежит конкретного пользователя (учетная запись) в nuget.org.

### <a name="client-requirement"></a>Требования клиента

Клиентам требуется передать следующий заголовок при вызове API **принудительной** пакетов nuget.org:

```
X-NuGet-Protocol-Version: 4.1.0
```

Обратите внимание, что предварительно `X-NuGet-Client-Version` заголовок используется для той же цели, но теперь устарело и больше не может использоваться.

**Принудительной** сам протокол описан в документации по [ `PackagePublish` ресурсов](package-publish-resource.md).

Если клиент взаимодействует с внешних служб и потребностей для проверки принадлежности пакета для конкретного пользователя (учетная запись), необходимо использовать следующий протокол и использовать ключи Проверьте область и не ключи API из nuget.org.

### <a name="api-to-request-a-verify-scope-key"></a>API для запроса ключа убедитесь области

Этот API используется для получения ключа Проверьте область для nuget.org автору, чтобы проверить правильность пакета, который владеет этим пользователем.

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a>Параметры запроса

Имя           | Увеличение     | Тип   | Обязательно | Примечания
-------------- | ------ | ------ | -------- | -----
Идентификатор             | URL-адрес    | string | да      | Identidier пакета, для которого запрашивается ключ области проверьте
VERSION        | URL-адрес    | string | Нет       | Версия пакета
X-NuGet-ApiKey | Header | string | да      | Например `X-NuGet-ApiKey: {USER_API_KEY}`.

#### <a name="response"></a>Ответ

```
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a>API, чтобы убедиться, что ключ области проверьте

Этот API используется для проверки области Проверьте ключ для принадлежащих nuget.org автора пакета.

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a>Параметры запроса

Имя           | Увеличение     | Тип   | Обязательно | Примечания
-------------  | ------ | ------ | -------- | -----
Идентификатор             | URL-адрес    | string | да      | Идентификатор пакета, для которого запрашивается ключ области проверьте
VERSION        | URL-адрес    | string | Нет       | Версия пакета
X-NuGet-ApiKey | Header | string | да      | Например `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`.

> [!Note]
> Этот ключ API области проверьте, в дневное время истечения срока действия или при первом использовании произойдет раньше.

#### <a name="response"></a>Ответ

Код состояния | Значение
----------- | -------
200         | Ключ API является допустимым
403         | Ключ API является недопустимым или не авторизован для передачи для пакета
404         | Пакет ссылается `ID` и `VERSION` (необязательно) не существует