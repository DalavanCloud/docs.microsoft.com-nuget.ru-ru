---
title: Способы установки пакетов NuGet | Документация Майкрософт
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/12/2018
ms.topic: overview
ms.prod: nuget
ms.technology: ''
description: В этой статье описывается процесс установки пакетов NuGet в проект, включая процессы на диске и все происходящее с применимыми файлами проекта.
keywords: установка NuGet, использование пакета NuGet, установка пакетов NuGet, ссылки на пакеты NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: b8cce7bd6c1bd73eb018b8891ddd72b2f4432d55
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="different-ways-to-install-a-nuget-package"></a>Способы установки пакета NuGet

Пакеты NuGet можно загрузить и установить с помощью любого из методов, приведенных в таблице ниже (если клиентские средства NuGet не установлены, [узнайте, как это сделать](../install-nuget-client-tools.md)). Вместо загрузки пакет можно извлечь из кэша.

| Метод | Описание: |
| --- | --- |
| Интерфейс командной строки dotnet.exe<br/>`dotnet add package <package_name>` | (Все платформы.) Извлекает пакет, определенный атрибутом \<имя_пакета\>, и развертывает его содержимое в папку в текущем каталоге, а затем добавляет ссылку в файл проекта. Кроме того, извлекает и устанавливает зависимости.<ul><li>[Установка и использование пакета (dotnet CLI)](../quickstart/install-and-use-a-package-using-the-dotnet-cli.md)</li><li>[Команда dotnet add package](/dotnet/core/tools/dotnet-add-package)</li></ul> |
| Пользовательский интерфейс диспетчера пакетов (Visual Studio) | (Компьютеры с Windows и Mac.) Пользовательский интерфейс, через который можно просматривать, выбирать и устанавливать в проект пакеты и их зависимости из указанного источника пакетов. Добавляет ссылки на установленные пакеты в файл проекта.<ul><li>[Установка и использование пакета (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Справочник по пользовательскому интерфейсу диспетчера пакетов для компьютеров с Windows](../tools/package-manager-ui.md)</li><li>[Включение пакета NuGet в проект](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| Консоль диспетчера пакетов (Visual Studio)<br/>`Install-Package <package_name>` | (Только компьютеры с Windows.) Извлекает пакет, определенный атрибутом \<имя_пакета\>, из выбранного источника и устанавливает его в указанный проект в решении, а затем добавляет ссылку в файл проекта. Кроме того, извлекает и устанавливает зависимости.<ul><li>[Установка и использование пакета (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Руководство по консоли диспетчера пакетов](../tools/package-manager-console.md)</li></ul> |
| Интерфейс командной строки nuget.exe<br/>`nuget install <package_name>` | (Все платформы.) Извлекает пакет, определенный атрибутом \<package_name\>, и развертывает его содержимое в папку в текущем каталоге. Кроме того, может извлекать все пакеты, перечисленные в файле `packages.config`. Извлекает и устанавливает зависимости, но не вносит никаких изменений в файлы проекта или файл `packages.config`.<ul><li>[Команда install](../tools/cli-ref-install.md)</li></ul> |

## <a name="what-happens-when-a-package-is-installed"></a>Процесс установки пакета

Попросту говоря, различные средства NuGet обычно создают ссылку на пакет в файле проекта или файле `packages.config`, а затем восстанавливают пакет, фактически устанавливая его. Исключение составляет команда `nuget install`, которая только добавляет пакет в папку `packages` и не меняет какие-либо другие файлы.

Общий процесс выглядит следующим образом:

1. (Все средства, кроме `nuget.exe`.) Записывает идентификатор и версию пакета в файл проекта или файл `packages.config`.

1. Получает сам пакет:
    - Проверяет, установлен ли пакет (по точному идентификатору и номеру версии) в папке *global-packages*, как описано в статье [Управление папкой установки глобальных пакетов, кэшем и временными папками](managing-the-global-packages-and-cache-folders.md).

    - Если пакета нет в папке *global-packages*, выполняется попытка извлечь пакет из источников, перечисленных в [файлах конфигурации](Configuring-NuGet-Behavior.md). Если источники сетевые, выполняется попытка извлечь пакет из кэша, когда не указан параметр `-NoCache` с помощью команды `nuget.exe` или параметр `--no-cache` с помощью команды `dotnet restore`. (Visual Studio и `dotnet add package` всегда используют кэш.) При использовании пакета из кэша в выходных данных отображается параметр CACHE. Срок действия кэша составляет 30 минут.

    - Если пакета нет в кэше, выполняется попытка скачать его из источников, перечисленных в файлах конфигурации. После скачивания пакета в выходных данных отображается параметр GET и ОК.

    - Если пакет не удается извлечь из любых источников, на этом этапе установка завершится ошибкой, например [NU1103](../reference/errors-and-warnings.md#nu1103). Обратите внимание, что в выходных данных ошибок выполнения команд `nuget.exe` отображается только последний проверенный источник, но подразумевается, что пакет отсутствует во всех.

    При извлечении пакета с помощью NuGet источники проверяются в таком порядке:
      - В проектах, использующих формат PackageReference, NuGet проверяет папку локальных источников и сетевые папки, а затем источники HTTP.
      - В проектах, в которых используется формат управления `packages.config`, NuGet применяет порядок источников в файлах конфигурации. Исключение — это операции восстановления, в случае которых порядок проверки не учитывается и NuGet использует пакет из любого первого ответившего источника.
      - В целом порядок проверки источников NuGet не особенно важен, так как любой конкретный пакет с указанным идентификатором и номером версии будет одним и тем же для всех источников.

1. (Все средства, кроме `nuget.exe`.) Сохраняет копию пакета и другие сведения в папке *http-cache*, как описано в статье [Управление папкой установки глобальных пакетов, кэшем и временными папками](managing-the-global-packages-and-cache-folders.md).

1. После загрузки устанавливает в папке *global-packages* пользователя. NuGet создает вложенную папку для каждого идентификатора пакета, а затем создает вложенные папки для каждой установленной версии пакета.

1. Обновление других файлов и папок проекта:

    - В проектах, использующих PackageReference, обновляет схему зависимостей пакетов, хранящихся в файле `obj/project.assets.json`. Само содержимое пакета не копируется в какую-либо папку проекта.
    - В проектах, использующих `packages.config`, копирует совпадающие с требуемой версией .NET Framework части расширенного пакета в папку проекта `packages`. (При использовании `nuget install` копируется весь расширенный пакет, так как `nuget.exe` не проверяет файлы проекта на наличие требуемой версии .NET Framework.)
    - Обновляет `app.config` и (или) `web.config`, если пакет использует [преобразования источника и файла конфигурации](../create-packages/source-and-config-file-transformations.md).

1. Устанавливает все зависимости нижнего уровня в случае их отсутствия в проекте. Этот процесс может обновить версии пакетов, как описано в статье [Принципы разрешения зависимостей пакетов в NuGet](../consume-packages/dependency-resolution.md).

1. (Только Visual Studio.) Отображает файл сведений пакета (если он доступен) в окне Visual Studio.

## <a name="related-articles"></a>Связанные статьи

- [Общие сведения и процесс использования пакетов](../consume-packages/overview-and-workflow.md)
- [Поиск и выбор пакетов](../consume-packages/finding-and-choosing-packages.md)
- [Управление папкой установки глобальных пакетов, кэшем и временными папками](managing-the-global-packages-and-cache-folders.md)
- [Настройка поведения NuGet](../consume-packages/configuring-nuget-behavior.md)