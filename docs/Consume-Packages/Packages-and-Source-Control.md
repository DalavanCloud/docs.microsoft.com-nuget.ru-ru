---
title: "Пакеты NuGet и управление исходным кодом | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 2c874e6f-99eb-46dd-997f-f67d98d0237e
description: "Вопросы, касающиеся обработки пакетов NuGet в системах управления версиями и исходным кодом, а также пропуска пакетов с TFVC и GIT."
keywords: "управление исходным кодом NuGet, система управления версиями NuGet, NuGet и GIT, NuGet и TFS, NuGet и TFVC, пропуск пакетов, репозитории для управления исходным кодом, репозитории для управления версиями"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c73dea74f2363f49fb476a5812c29de63fec89a3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a>Пропуск пакетов NuGet в системах управления исходным кодом

Разработчики обычно пропускают пакеты NuGet из своих репозиториев управления исходным кодом и вместо этого полагаются на [восстановление пакетов](../consume-packages/package-restore.md) для переустановки зависимостей проекта перед сборкой.

К причинам использования восстановления пакетов относятся следующие:

1. Распределенные системы управления версиями, такие как Git, включают полные копии каждой версии каждого файла в репозитории. Часто обновляемые двоичные файлы приводят к значительному раздуванию и увеличивают время, необходимое для клонирования репозитория.
1. При включении пакетов в репозиторий разработчики должны добавлять ссылки непосредственно на содержимое пакета на диске, а не ссылаться на пакеты с помощью NuGet, что может привести к наличию в проекте жестко заданных путей.
1. Становится все труднее очистить решение от неиспользуемых папок пакетов, так как при этом нужно не удалить используемые папки пакетов.
1. Опуская пакеты, вы обеспечиваете четкие границы владения между вашим кодом и чужими пакетами, от которых вы зависите. Многие пакеты NuGet уже находятся в их собственных репозиториях управления исходным кодом.

Хотя восстановление пакетов является поведением NuGet по умолчанию, для пропуска пакетов&mdash;а именно папки `packages` в проекте&mdash;в системе управления исходным кодом требуется выполнить некоторые операции вручную, как описано в следующих разделах.

## <a name="omitting-packages-with-git"></a>Пропуск пакетов в Git

Используйте [файл GITIGNORE](https://git-scm.com/docs/gitignore), чтобы предотвратить включение папки `packages` в систему управления исходным кодом. Для справки см. [пример `.gitignore` для проектов Visual Studio](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).

Далее приведены важные части файла `.gitignore`:

```
# Ignore NuGet Packages
*.nupkg

# Ignore the packages folder
**/packages/*

# Include packages/build/, which is used as an MSBuild target
!**/packages/build/

# Uncomment if necessary; generally it's regenerated when needed
#!**/packages/repositories.config

# Ignore other intermediate files that NuGet might create. project.lock.json is used in conjunction
# with project.json; project.assets.json is used in conjunction with the PackageReference format.
project.lock.json
project.assets.json
*.nuget.props
```

## <a name="omitting-packages-with-team-foundation-version-control"></a>Пропуск пакетов в системе управления версиями Team Foundation

> [!Note]
> По возможности выполните эти инструкции *перед* добавлением проекта в систему управления исходным кодом. В противном случае вручную удалите папку `packages` из репозитория и верните это изменение, прежде чем продолжить.

Отключение интеграции системы управления исходным кодом с TFVC для выбранных файлов:

1. Создайте папку с именем `.nuget` в папке решения (где находится файл `.sln`).
    - Совет. Чтобы создать эту папку в проводнике Windows, используйте имя `.nuget.` *с* конечной точкой.

1. В этой папке создайте файл с именем `NuGet.Config` и откройте его для редактирования.

1. Добавьте хотя бы следующий текст, где параметр [disableSourceControlIntegration](../Schema/nuget-config-file.md#solution-section) предписывает Visual Studio пропустить все содержимое папки `packages`:

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. Если вы используете TFS 2010 или более ранней версии, замаскируйте папку `packages` в сопоставлениях рабочей области.

1. В TFS 2012 и более поздней версии или Visual Studio Team Services создайте файл `.tfignore`, как описано в статье [Добавление файлов на сервер](https://www.visualstudio.com/en-us/docs/tfvc/add-files-server#tfignore). Включите в этот файл приведенное ниже содержимое, чтобы явно игнорировать изменения в папке `\packages` на уровне репозитория и нескольких других промежуточных файлах. (Вы можете создать файл в проводнике Windows, используя имя `.tfignore.` с конечной точкой, но сначала вам может потребоваться отключить параметр "Hide known file extensions" (Скрыть известные расширения файлов).)

   ```
   # Ignore NuGet Packages
   *.nupkg   

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Include package target files which may be required for MSBuild, again prefixing the folder name as needed.
   !packages/*.targets

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. Добавьте `NuGet.Config` и `.tfignore` в систему управления исходным кодом и верните изменения.