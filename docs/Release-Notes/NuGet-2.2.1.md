---
title: "Заметки о выпуске NuGet 2.2.1 | Документы Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 39ceaeb3-2d33-4b1c-b195-eba36c6cbf9a
description: "Заметки о выпуске для NuGet 2.2.1, включая известные проблемы, исправленные ошибки, добавленные функции и DCR."
keywords: "NuGet 2.2.1 заметки о выпуске, исправления, известными проблемами, добавлены функции, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c31150572b4b6e066643ebcf0d92be16b25c6e19
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-221-release-notes"></a>Заметки о выпуске NuGet 2.2.1

[Заметки о выпуске NuGet 2.2](../release-notes/nuget-2.2.md) | [заметки о выпуске NuGet 2.5](../release-notes/nuget-2.5.md)

NuGet 2.2.1 был выпущен 15 февраля 2013 г.  Номер версии расширения VS, 2.2.40116.9051.

## <a name="localization-refresh"></a>Локализация обновления
Когда NuGet поставляется как часть Visual Studio 2012, он был полностью локализованы на английский + 13 языков.  С этого момента отправки NuGet 2.1 и 2.2, но локализации не были обновлены.  В выпуске NuGet 2.2.1 обновляет локализация.

Пользовательский Интерфейс и консоль PowerShell NuGet, локализованы на следующие языки:

1. Китайский (упрощенное письмо)
1. Китайский (традиционное письмо)
1. Чешский
1. Английский
1. Французский
1. Немецкий
1. Итальянский
1. Японский
1. Корейский
1. Польский
1. Португальский (Бразилия)
1. Русский
1. Испанский
1. Турецкий

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a>Шаблоны Visual Studio поддерживает несколько репозиториев предварительно установленного пакета
Если создать шаблоны Visual Studio можно использовать NuGet [выполнить предварительную установку пакетов](../visual-studio-extensibility/visual-studio-templates.md) как часть шаблона.  До этого момента, эта функция имеет ограничение необходимость все пакеты из одного источника.  С помощью NuGet 2.2.1, что пакеты, установленные из нескольких репозиториев (в шаблоне, расширение VSIX или папке на диске, определенные в реестре).

Основным сценарием для этой функции — пользовательские шаблоны проектов ASP.NET.  Встроенные шаблоны ASP.NET использовать предустановленных пакетов, получают пакеты с локального диска.  Теперь можно создать пользовательский шаблон проекта ASP.NET, который использует существующие пакеты, установленные с помощью ASP.NET, но добавление дополнительных пакетов NuGet в шаблон.

## <a name="bug-fixes"></a>Исправления ошибок
NuGet 2.2.1 включает несколько целевых исправления ошибок. Список рабочих элементов исправления в NuGet 2.2.1 представление [NuGet отслеживания проблем в этом выпуске](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).


## <a name="known-issues"></a>Известные проблемы

При расширении шаблоны проектов ASP.NET все репозитории предустановленных пакетов необходимо использовать то же значение для `isPreunzipped` атрибута.