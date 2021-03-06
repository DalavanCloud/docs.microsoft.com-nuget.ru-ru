---
title: Вопросы и ответы по NuGet
description: Вопросы и ответы по использованию NuGet в командной строке и в Visual Studio, а также по работе с коллекцией NuGet.
author: karann-msft
ms.author: karann
ms.date: 01/11/2018
ms.topic: conceptual
ms.openlocfilehash: 93a22b423b193874c4c69c37ff9c6d9b4489a48d
ms.sourcegitcommit: 673e580ae749544a4a071b4efe7d42fd2bb6d209
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/06/2018
ms.locfileid: "52977580"
---
# <a name="nuget-frequently-asked-questions"></a>Вопросы и ответы по NuGet

**Что необходимо для запуска NuGet?**

Все данные по пользовательскому интерфейсу и средствам командной строки доступны в [руководстве по установке](../install-nuget-client-tools.md).

**Поддерживает ли NuGet Mono?**

Средство командной строки `nuget.exe` выполняет построение и запускается с помощью Mono 3.2 или более поздней версии и поддерживает создание пакетов в Mono.

Несмотря на то, что `nuget.exe` полностью работает в Windows, в Linux и OS X существуют известные проблемы. См. раздел GitHub, посвященный [проблемам с Mono](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono).

[Графический клиент](https://github.com/mrward/monodevelop-nuget-addin) доступен в виде надстройки для MonoDevelop.

**Как можно определить, что содержит пакет, и является ли он стабильным и полезным для моего приложения?**

Основным источником информации о пакете является его страница сведений на веб-сайте nuget.org (или в другом закрытом веб-канале). На странице каждого пакета на веб-сайте nuget.org приводится описание проекта, история его версий и статистика использования. В разделе **Сведения** на странице пакета также приводится ссылка на веб-сайт проекта, где обычно можно найти много примеров и других документов, с помощью которых можно оценить полезность пакета.

Дополнительные сведения см. в разделе [Поиск и выбор пакетов](../consume-packages/finding-and-choosing-packages.md).

## <a name="nuget-in-visual-studio"></a>NuGet в среде Visual Studio

**Каким образом обеспечивается поддержка NuGet в различных продуктах Visual Studio?**

- Visual Studio для Windows поддерживает [пользовательский интерфейс диспетчера пакетов](../tools/package-manager-ui.md) и [консоль диспетчера пакетов](../tools/package-manager-console.md).
- Visual Studio для Mac реализует встроенные возможности NuGet, которые описываются в разделе [Включение пакета NuGet в проект](/visualstudio/mac/nuget-walkthrough).
- Visual Studio Code для всех платформ не поддерживает прямую интеграцию с NuGet. Используйте [интерфейс командной строки NuGet](../tools/nuget-exe-cli-reference.md) или [интерфейс командной строки dotnet](../tools/dotnet-commands.md).
- Azure DevOps реализует [шаг построения для восстановления пакетов NuGet](/vsts/build-release/tasks/package/nuget). Также вы можете [разместить закрытые веб-каналы NuGet в Azure DevOps](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).

**Как определить точную версию устанавливаемых средств NuGet?**

В Visual Studio выберите **Справка > О Microsoft Visual Studio** и проверьте версию компонента **Диспетчер пакетов NuGet**.

Также можно запустить консоль диспетчера пакетов (**Сервис > Диспетчер пакетов NuGet > Консоль диспетчера пакетов**) и ввести `$host`, чтобы просмотреть сведения о версии NuGet и другую информацию.

**Какие языки программирования поддерживает NuGet?**

NuGet обычно работает с языками платформы .NET и предназначен для использования библиотек .NET в проекте. Поскольку для проектов некоторых типов также поддерживаются средства автоматизации MSBuild и Visual Studio, в определенной степени также поддерживаются другие проекты и языки.

Последняя версия NuGet поддерживает C#, Visual Basic, F#, WiX и C++.

**Какие шаблоны проектов поддерживает NuGet?**

NuGet обеспечивает полную поддержку множества шаблонов проектов, включая Windows, Интернет, облако, SharePoint, Wix и другие.

**Как обновить пакеты, которые являются частью шаблонов Visual Studio?**

Перейдите на вкладку **Обновления** в пользовательском интерфейсе диспетчера проектов и выберите **Обновить все** или воспользуйтесь [командой `Update-Package`](../tools/ps-ref-update-package.md) в консоли диспетчера проектов.

Чтобы обновить сам шаблон, необходимо вручную обновить репозиторий шаблонов. Дополнительные сведения по этой теме см. в [блоге Ксавье Декостера (Xavier Decoster)](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages). Обратите внимание, что все это вы делаете на свой страх и риск, поскольку ручное обновление может привести к повреждению шаблона в том случае, если последние версии всех зависимостей несовместимы друг с другом.

**Можно ли использовать NuGet вне среды Visual Studio?**

Да. NuGet работает непосредственно из командной строки. См. [руководство по установке](../install-nuget-client-tools.md) и [справочник по интерфейсу командной строки](../tools/nuget-exe-cli-reference.md).

## <a name="nuget-command-line"></a>Командная строка NuGet

**Как получить последнюю версию средства командной строки NuGet?**

См. [руководство по установке](../install-nuget-client-tools.md).

**Для чего нужна лицензия на веб-сайте nuget.exe?**

Вы можете распространить nuget.exe в соответствии с условиями лицензии MIT. Вы несете ответственность за обновление и обслуживание всех распространяемых вами копий nuget.exe.

**Можно ли расширить возможности средства командной строки NuGet?**

Да. Вы можете добавлять в `nuget.exe` собственные команды, как описывается в [статье Роба Рейнолда (Rob Reynold)](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a>Консоль диспетчера пакетов NuGet (Visual Studio для Windows)

**Как получить доступ к объекту DTE в консоли диспетчера пакетов?**

Объект верхнего уровня в объектной модели автоматизации Visual Studio называется объектом DTE (среда средств разработки). Этот объект предоставляется консолью с помощью переменной `$DTE`. Дополнительные сведения см. в разделе [Общие сведения о модели автоматизации](/visualstudio/extensibility/internals/automation-model-overview) в документации по расширению среды Visual Studio.

**При попытке привести переменную $DTE к типу DTE2 возникает ошибка: "Не удается преобразовать значение "EnvDTE.DTEClass" типа "EnvDTE.DTEClass" в тип "EnvDTE80.DTE2"". В чем проблема?**

Это известная проблема, связанная с взаимодействием PowerShell с COM-объектом. Попробуйте выполнить следующие действия:

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

`Get-Interface` — это вспомогательная функция, добавляемая узлом PowerShell NuGet.

## <a name="creating-and-publishing-packages"></a>Создание и публикация пакетов

**Как включить мой пакет в веб-канал?**

См. раздел [Создание и публикация пакетов](../quickstart/create-and-publish-a-package.md).

**У меня есть несколько версий библиотеки, предназначенных для различных версий платформы .NET Framework. Как построить единый пакет, поддерживающий такую реализацию?**

См. раздел [Поддержка нескольких версий и профилей платформы .NET Framework](../create-packages/supporting-multiple-target-frameworks.md).

**Как настроить свой собственный репозиторий или веб-канал?**

См. раздел [Общие сведения о размещении пакетов](../hosting-packages/overview.md).

**Как выполнить массовую загрузку пакетов в мой веб-канал NuGet?**

См. раздел [Массовая публикация пакетов NuGet](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).

## <a name="working-with-packages"></a>Работа с пакетами

**В чем разница между пакетами уровня проекта и уровня решения?**

Пакет уровня решения (NuGet версии 3.x или более поздней) устанавливается в решении только один раз и после этого доступен для всех проектов решения. Пакет уровня проекта устанавливается в каждом проекте, который его использует. Пакет уровня решения также может устанавливать новые команды, которые могут вызываться из консоли диспетчера пакетов.

**Можно ли устанавливать пакеты NuGet без подключения к Интернету?**

Да. См. статью блога Скотта Ханселмана (Scott Hanselman), посвященную [доступу к NuGet при неработающем веб-сайте nuget.org или во время полета на самолете](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).

**Можно ли устанавливать пакеты в папку, отличную от заданной по умолчанию?**

Задайте параметр [`repositoryPath`](../reference/nuget-config-file.md#config-section) в файле `Nuget.Config`, используя `nuget config -set repositoryPath=<path>`.

**Как избежать добавления папки пакетов NuGet в систему управления версиями?**

Присвойте свойству [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) в файле `Nuget.Config` значение `true`. Этот ключ работает на уровне решения и поэтому должен добавляться в файл `$(Solutiondir)\.nuget\Nuget.Config`. Если включить восстановление пакета из Visual Studio, этот файл будет создан автоматически.

**Как отключить восстановление пакетов?**

См. раздел [Включение и отключение восстановления пакетов](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).

**Почему при установке локального пакета с удаленными зависимостями возникает ошибка "Не удается разрешить зависимость"?**

При установке локального пакета в проект выберите источник **Все**. При этом вместо использования одного веб-канала будут объединены все веб-каналы. Причиной этой ошибки обычно является то, что пользователи локального репозитория часто стремятся избежать случайной установки удаленного пакета из-за требований корпоративной политики.

**У меня есть несколько проектов, расположенных в одной папке. Как использовать отдельные файлы packages.config для каждого проекта?**

В большинстве случаев, когда отдельные проекты располагаются в отдельных папках, это не проблема, поскольку NuGet идентифицирует файлы `packages.config` в каждом проекте. Если вы работаете с NuGet версии 3.3 или более поздней и размещаете несколько проектов в одной папке, вы можете вставить имя проекта в имена файлов `packages.config`, используя шаблон `packages.{project-name}.config`. NuGet будет использовать этот файл.

Это также не проблема при использовании PackageReference, поскольку каждый файл проекта содержит собственный список зависимостей.

**Я не вижу nuget.org в списке репозиториев. Как вернуть его?**

- Добавьте `https://api.nuget.org/v3/index.json` в список источников или
- Удалите файл `%appdata%\.nuget\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) и дождитесь, пока NuGet снова создаст его.

**Какие условия лицензирования применяются по умолчанию, если для пакета не указаны никакие сведения о лицензии?**

В отношении каждого пакета действуют входящие в него условия. Прежде чем получать доступ к пакетам, скачивать или получать их, необходимо ознакомиться с соответствующими условиями. Воспользуйтесь ссылкой **Сведения о лицензии** на странице пакета на веб-сайте nuget.org.

Если для пакета не заданы условия лицензии, следует обратиться непосредственно к владельцу пакета **по ссылке для связи с владельцем** на странице пакета на веб-сайте nuget.org. Корпорация Майкрософт не предоставляет вам лицензию на какую-либо интеллектуальную собственность сторонних поставщиков пакетов и не несет ответственность за сведения, предоставляемые третьими лицами.

## <a name="managing-packages-on-nugetorg"></a>Управление владельцами пакетов на веб-сайте nuget.org

**Можно ли изменить метаданные пакета после его отправки?**

NuGet рекомендует подписать все пакеты. Основополагающим принципом подписывания является то, что содержимое подписанного пакета, включая файл nuspec, является неизменным. При редактировании метаданных пакета изменяется файл nuspec, в результате чего существующие подписи становятся недействительными. Мы рекомендуем изменить существующие рабочие процессы таким образом, чтобы после создания пакета не требовалось редактирование его метаданных.

Обратите внимание, что перечисленные в пакете зависимости создаются автоматически на основании самого пакета и не могут быть изменены.

Кроме того, отправка пакета на веб-сайт [int.nugettest.org](https://int.nugettest.org) позволяет легко протестировать и проверить пакет, не публикуя его в общедоступной коллекции.

**Можно ли зарезервировать имена для пакетов, которые будут опубликованы в будущем?**

Да. Вы можете зарезервировать идентификаторы пакетов на веб-сайте [nuget.org](https://www.nuget.org/), запросив префикс идентификатора пакета для своей учетной записи. Чтобы запросить префикс идентификатора пакета, следуйте инструкциям в [документации](https://docs.microsoft.com/nuget/reference/id-prefix-reservation).

**Как заявить о правах владельца пакетов?**

См. раздел [Управление владельцами пакетов на веб-сайте nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).

**Что делать с владельцем пакета, который нарушает условия лицензии на мое программное обеспечение?**

В рамках сообщества NuGet мы пропагандируем тесное сотрудничество по вопросам разрешения любых разногласий, которые могут возникать между владельцами пакетов и другого программного обеспечения. Прежде чем обращаться к администраторам nuget.org, мы рекомендуем воспользоваться [процессом разрешения споров](../policies/dispute-resolution.md).

**Рекомендуется ли загружать тестовые пакеты на веб-сайт nuget.org?**

В целях тестирования вы можете использовать веб-сайт [int.nugettest.org](https://int.nugettest.org) или альтернативные общедоступные серверы NuGet, такие как [myget.org](https://myget.org) или [Azure DevOps](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).

Обратите внимание, что отправленные на веб-сайт int.nugettest.org пакеты могут не сохраняться.

**Каков максимальный размер пакетов, загружаемых на веб-сайт nuget.org?**

На веб-сайт nuget.org можно загружать пакеты размером до 250 МБ, однако мы рекомендуем по возможности не создавать пакеты размером более 1 МБ и использовать зависимости для установления связей между пакетами. Чтобы избежать конфликтов, рекомендуется включать в пакет только одну сборку.

NuGet использует для скачивания пакетов протокол HTTP, поэтому для крупных пакетов повышается вероятность сбоев при установке.

Вы можете использовать общие зависимости между несколькими пакетами, уменьшая общий размер скачиваемых клиентами пакетов NuGet.

В большинстве случаев зависимости являются статическими и никогда не изменяются. При исправлении ошибок в коде обновление зависимостей может не требоваться. Если вы объединяете зависимости в пакет, в конечном итоге вам придется каждый раз выполнять повторную доставку пакетов большого размера. Разбивая пакеты NuGet на взаимосвязанные зависимости, вы реализуете более детализированный процесс обновления пакетов для клиентов.

## <a name="nugetorg-not-accessible"></a>Отсутствие доступа к nuget.org

**Почему я не могу скачать пакеты с веб-сайта nuget.org или загрузить их на него?**

Во-первых, убедитесь, что вы используете последние версии NuGet. Если при работе такой версии продолжают возникать ошибки, [обратитесь в службу поддержки](https://www.nuget.org/policies/Contact) и предоставьте нам дополнительные сведения для устранения неполадок, в том числе следующие:

- Версия NuGet, которую вы используете
- Источники пакетов, которые вы используете
- Журнал восстановления с подробным уровнем детализации
- Данные трассировки MTR или Fiddler (см. ниже)
- Ваш географический регион
- Версия вашей операционной системы
- Конфигурация компьютера (ЦП, сетевые компоненты, жесткий диск)
- Защищена ли виртуальная машина прокси-сервером или брандмауэром
- Установленные на компьютере версии платформы .NET
- Версии кроссплатформенных средств, таких как интерфейс командной строки .NET или DNU, которые вы используете

*Получение трассировки MTR:*

- Скачайте WinMTR из [http://winmtr.net/download/](http://winmtr.net/).
- Введите имя узла `api.nuget.org` и щелкните **Пуск**.
- Дождитесь, пока значение в столбце **Отправлено** превысит 100.

    ![Получение трассировки MTR](media/mtr.png)

- Скопируйте текст в буфер обмена.

*Получение трассировки Fiddler:*

- Установите последнюю версию [Fiddler](http://www.telerik.com/download/fiddler).
- Запустите Fiddler и отключите запись трафика в меню **Файл > Запись трафика**.
- Удалите все сеансы (выделите все элементы в списке и нажмите клавишу **Delete**).
- Настройте Fiddler для записи трафика HTTPS, установив флажок **Расшифровывать трафик HTTPS** на вкладке **HTTPS** в меню **Сервис > Параметры Fiddler...**
- Закройте Visual Studio.
- Включите меню **Файл > Запись трафика**.
- Запустите исполняемый файл Visual Studio или nuget.exe и выполните действия, которые не получились ранее. Трафик, сформированный этими действиями, будет показан в Fiddler.
- После выполнения нужных действий выберите **Файл > Сохранить > Все сеансы**, чтобы сохранить записанные сеансы.

Примечание. Для маршрутизации трафика NuGet через Fiddler может потребоваться присвоить переменной среды `HTTP_PROXY` значение `http://127.0.0.1:8888`.

Если этот способ не помогает, попробуйте советы, приведенные в этой [статье на веб-сайте StackOverflow](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).

**Каковы конечные точки API для nuget.org?**

Версия 3: `https://api.nuget.org/v3/index.json` Версия 2: `https://www.nuget.org/api/v2/` (Обратите внимание, что все API версии 2 не рекомендуются к использованию и не работают с NuGet 4 или более поздних версий.)
