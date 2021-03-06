---
title: Заметки о выпуске NuGet 3.2 RC
description: Заметки о выпуске для NuGet 3.2 RC, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: eafdedc3ad022a6794dbeb390de87d7f317e28f1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551502"
---
# <a name="nuget-32-rc-release-notes"></a>Заметки о выпуске NuGet 3.2 RC

[Заметки о выпуске NuGet 3.1.1](../release-notes/nuget-3.1.1.md) | [заметки о выпуске NuGet 3.2](../release-notes/nuget-3.2.md)

Была выпущена версия-кандидат NuGet 3.2 выпуск 2 сентября 2015 г. как совокупность улучшений и исправлений для 3.1.1.  Кроме того это первый выпуск, сначала опубликованные на новый репозиторий dist.nuget.org.

## <a name="new-features"></a>Новые функции

* Проекты, находящиеся в той же папке, теперь могут иметь разные `project.json` файлы в этой папке, относящуюся к каждому проекту.  Для каждого проекта, имя `project.json` файл `{ProjectName}.project.json` и NuGet правильно будет ссылаться и использовать содержимое, для каждого проекта, соответствующим образом.  Это поддерживает новую функцию [1102](https://github.com/NuGet/Home/issues/1102)
* `NuGet.Config` Теперь поддерживает globalPackagesFolder как относительный путь - [1062](https://github.com/NuGet/Home/issues/1062)

## <a name="command-line-updates"></a>Обновления командной строки

Это первая версия nuget.exe клиента, который поддерживает серверы v3 NuGet и восстановление пакетов для проектов, управляемых с помощью `project.json` файл.

#### <a name="there-were-a-number-of-authenticated-feed-issues-that-were-addressed-in-this-release-to-improve-interactions-with-the-client"></a>Произошли количество прошедших проверку подлинности веб-канала проблемы, устраненные в этом выпуске для улучшения взаимодействия с клиентом.

* Установить / восстановления взаимодействия отправлять только те учетные данные для исходного запроса, прошедшего проверку подлинности веб-канал - [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456)
* Команда Push не разрешить учетные данные из конфигурации - [1248](https://github.com/NuGet/Home/issues/1248)
* Агент пользователя и заголовки теперь отправляются в репозитории NuGet для отслеживания статистики - [929](https://github.com/NuGet/Home/issues/929)

#### <a name="we-made-a-number-of-improvements-to-better-handle-network-failures-while-attempting-to-work-with-a-remote-nuget-repository"></a>Мы внесли ряд улучшений для улучшения обработки сбоев сети при попытке работы с удаленным репозиторием NuGet:

* Улучшены сообщения об ошибках, когда не удается подключиться к удаленной веб-каналы - [1238](https://github.com/NuGet/Home/issues/1238)
* Исправлена команда восстановления NuGet для правильно возвращается значение 1, когда возникает ошибка - [1186](https://github.com/NuGet/Home/issues/1186)
* Теперь повторная попытка сетевые подключения каждые 200 мс, не более 5 попыток в случае ошибки HTTP 5xx - [1120](https://github.com/NuGet/Home/issues/1120)
* Улучшенную обработку ответа перенаправления сервера во время команда push - [1051](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source` Теперь поддерживает имя URL-адрес или репозитория из Nuget.Config в качестве аргумента - [1046](https://github.com/NuGet/Home/issues/1046)
* Отсутствующие пакеты, которые не были расположены в репозитории во время восстановления теперь выводятся как ошибки вместо предупреждения [1038](https://github.com/NuGet/Home/issues/1038)
* Исправлена обработка multipartwebrequest \r\n для сценариев Unix/Linux - [776](https://github.com/NuGet/Home/issues/776)

#### <a name="there-are-a-number-of-fixes-to-issues-with-various-commands"></a>Существует ряд исправлений для проблем с различными командами:

* Команда Push более не поддерживает запрос GET, прежде чем запрос PUT в источнике пакета - [1237](https://github.com/NuGet/Home/issues/1237)
* Команда list больше не повторяется номера версий - [1185](https://github.com/NuGet/Home/issues/1185)
* Пакет с аргументом - сборки теперь правильно поддерживает C# 6.0 - [1107](https://github.com/NuGet/Home/issues/1107)
* Исправленные проблемы, выполняется попытка упаковать проект F #, созданные с помощью Visual Studio 2015 — [1048](https://github.com/NuGet/Home/issues/1048)
* Если пакеты уже существует - восстановить холостой командой теперь [1040](https://github.com/NuGet/Home/issues/1040)
* Улучшенная ошибка сообщения, когда `packages.config` файл имеет неправильный формат - [1034](https://github.com/NuGet/Home/issues/1034)
* Исправлена Команда restore с `-SolutionDirectory` коммутатора для работы с относительными путями - [992](https://github.com/NuGet/Home/issues/992)
* Улучшена команда обновлено для поддержки обновления решения - [924](https://github.com/NuGet/Home/issues/924)

Полный список ошибок, устраненных в этом выпуске можно найти в NuGet GitHub [командной строки вехи](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate).

## <a name="visual-studio-extension-updates"></a>Обновление расширений Visual Studio

### <a name="new-features-in-visual-studio"></a>Новые возможности в Visual Studio

* Был добавлен новый пункт контекстного меню в обозревателе решений узел решения, позволяющий пакеты для восстановления без построения решения ([1274](https://github.com/NuGet/Home/issues/1274)).

![Новый «Восстановить пакеты» пункт контекстного меню](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>Обновления и исправления в Visual Studio

#### <a name="the-fixes-for-authenticated-feeds-were-rolled-up-and-addressed-in-the-extension-as-well--the-following-authentication-items-were-also-addressed-in-the-extension"></a>Исправления для каналы с проверкой подлинности были сведены, а также опишем в расширении также.  Параметры проверки подлинности также были решены в расширении:

* Теперь правильно их обработке NuGet 3 веб-каналы выполнена проверка подлинности, а не v2 проверки подлинности веб-каналы - [1216](https://github.com/NuGet/Home/issues/1216)
* Исправленный запрос учетных данных проверки подлинности в проектах, использующих `project.json` и обмена данными с веб-каналов версии 2 - [1082](https://github.com/NuGet/Home/issues/1082)

#### <a name="network-connectivity-had-affected-the-user-interface-in-visual-studio-and-we-addressed-this-with-the-following-fixes"></a>Сетевое подключение касается пользовательского интерфейса в Visual Studio, а мы устранили с следующие исправления:

* Улучшенное обслуживание в локальном кэше версии пакетов - [тезисы:](https://github.com/NuGet/Home/issues/1096)
* Изменено поведение сбоя при подключении к версии 3, веб-канал больше не попытка рассматривать ее как веб-канала версии 2 - [1253](https://github.com/NuGet/Home/issues/1253)
* Сбои теперь предотвращение установки при установке пакета с помощью нескольких источников пакетов - [1183](https://github.com/NuGet/Home/issues/1183)

Мы улучшили обработку взаимодействия с операциями сборки:

* Теперь построение проектов, если восстановление пакетов для одного проекта завершается ошибкой - [1169](https://github.com/NuGet/Home/issues/1169)
* Установка пакета в проект, который является зависимыми от другого проекта в решении вызывает повторное построение решения - [981](https://github.com/NuGet/Home/issues/981)
* Исправлено неудачном выполнении пакета установки до правильно откат изменений в проект - [1265](https://github.com/NuGet/Home/issues/1265)
* Исправлено непреднамеренным удалением `developmentDependency` атрибута пакета в `packages.config`  -  [1263](https://github.com/NuGet/Home/issues/1263)
* Вызовы `install.ps1` теперь имеют правильное `$package.AssemblyReferences` объект, переданный - [1245](https://github.com/NuGet/Home/issues/1245)
* Больше не препятствует удаление пакетов в проектах универсальной платформы Windows, когда проект находится в неисправном состоянии - [1128](https://github.com/NuGet/Home/issues/1128)
* Решений, содержащих сочетание `packages.config` и `project.json` проекты теперь правильно построены без необходимости второй операции - сборки [1122](https://github.com/NuGet/Home/issues/1122)
* Правильно размещение файлов app.config, если они связаны, или также находится в другой папке - [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894)
* Проекты универсальной платформы Windows теперь можно установить исключенные пакеты - [1109](https://github.com/NuGet/Home/issues/1109)
* Восстановление пакетов теперь разрешено, хотя это решение не находится в сохраненном состоянии - [1081](https://github.com/NuGet/Home/issues/1081)


Обработка обновлений для конфигурации, которые были исправлены файлы:

* Больше не удаление файла целевых объектов доставляется из пакета на последующих сборках `project.json` управляемый проект - [1288](https://github.com/NuGet/Home/issues/1288)
* Больше не изменяя файлы Nuget.Config во время построения решения ASP.NET 5 - [1201](https://github.com/NuGet/Home/issues/1201)
* Больше не изменение допускается ограничение версий во время обновления пакета - [1130](https://github.com/NuGet/Home/issues/1130)
* Блокировка файлов теперь оставаться заблокированными во время сборки - [1127](https://github.com/NuGet/Home/issues/1127)
* Теперь изменение `packages.config` и не переписывая его во время обновления - [585](https://github.com/NuGet/Home/issues/585)


Улучшение взаимодействия с системой управления версиями TFS:

* Больше не сбой установки для пакетов, привязанных к TFS - [1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980)
* Исправленный пользовательский интерфейс NuGet для разрешения интеграции TFS 2013 - [1071](https://github.com/NuGet/Home/issues/1071)
* Исправлены ссылки на пакеты восстановлены надлежащим образом приходят из папки пакетов - [1004](https://github.com/NuGet/Home/issues/1004)

Наконец мы также улучшили следующие элементы:

* Уменьшить уровень детализации сообщений журнала для `project.json` управляемых проектов - [1163](https://github.com/NuGet/Home/issues/1163)
* Теперь правильно отображение установленной версии пакета в пользовательском интерфейсе - [1061](https://github.com/NuGet/Home/issues/1061)


Полный список проблемы для расширения Visual Studio можно найти в NuGet GitHub [3,2 вехи](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)

## <a name="known-issues"></a>Известные проблемы

Мы продолжаем для отслеживания проблем в нашем списке проблемы GitHub, который можно найти в: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)