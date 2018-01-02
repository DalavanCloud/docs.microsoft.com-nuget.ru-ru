---
title: "Заметки о выпуске версии-Кандидата NuGet 3.0 | Документы Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: cd0c102f-bc33-4aa2-a921-61fa21d42b28
description: "Заметки о выпуске для RC NuGet 3.0, включая известные проблемы, исправленные ошибки, добавленные функции и DCR."
keywords: "Версия-Кандидат NuGet 3.0 заметки о выпуске, исправления ошибок, известные проблемы, добавлены функции, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5d0eeae479617bc30901b599251628f72950cc67
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-30-rc-release-notes"></a>Заметки о выпуске версии-Кандидата NuGet 3.0

[Заметки о выпуске бета-версии NuGet 3.0](../release-notes/nuget-3.0-beta.md) | [заметки о выпуске версии-кандидата 2 NuGet 3.0](../release-notes/nuget-3.0-RC2.md)

Версия-Кандидат NuGet 3.0 был выпущен 29 апреля 2015 г. с выпуском Visual Studio 2015 RC. Этот выпуск содержит ряд важных исправлений, повышение производительности и обновления для поддержки новых платформ.  Она доступна только для Visual Studio 2015.

### <a name="continued-focus-on-performance"></a>О производительности

Стабильность и производительность запросов NuGet остаются горячей раздела, мы сосредоточены на.  В этом выпуске необходимо запустить для просмотра операций очень быстрый поиск в NuGet пользовательского интерфейса и веб-сайта.  Мы отслеживании службу и как использовать службы, чтобы мы могли продолжать для настройки этих операций.

## <a name="significant-issues-resolved"></a>Значительные устранения проблем

Чтобы стабилизировать клиенты NuGet, была решена много проблем в рамках этого выпуска.  Ниже приведен лишь краткий перечень некоторые более важные устранения проблем:

* В ходе переименования K framework для ASP.NET 5, были обновлены моникеров платформы для обработки dnx и dnxcore [ссылку](https://github.com/NuGet/Home/issues/215)
* Добавлено в справочной документации по ссылкам в пользовательском Интерфейсе Visual Studio [ссылку](https://github.com/NuGet/Home/issues/232)
* Лучше обработка сложных ссылок в `.nuspec` со ссылками с разделителями запятыми framework [ссылку](https://github.com/NuGet/Home/issues/276)
* Исправлена поддержки японского языка и региональных параметров [ссылку](https://github.com/NuGet/Home/issues/253)
* Обновленный клиент, чтобы разрешить проекты ASP.NET 5, чтобы использовать новые конечные точки v3 [ссылку](https://github.com/NuGet/Home/issues/219)
* Обновленные лучше дескриптор папку пакеты с системой управления версиями [ссылку](https://github.com/NuGet/Home/issues/56)
* Исправлена поддержка вспомогательных пакетов [ссылку](https://github.com/NuGet/Home/issues/17)
* Исправлено поддержка специфичная для платформы файлы содержимого [ссылку](https://github.com/NuGet/Home/issues/18)

## <a name="github-presence-overhaul"></a>Пересмотренную видеодрайверов присутствие GitHub

Мы внесли некоторые изменения в наших [источника репозитории кода на GitHub](http://github.com/nuget/home).  При наличии проблем с помощью клиента NuGet Visual Studio, команды Powershell или командной строки исполняемый файл можно войти этих проблем и отслеживать ход выполнения работ в нашем [списка проблем репозитория GitHub домашней](http://github.com/nuget/home/issues).  Мы отслеживаем проблемы для коллекции на нашем [репозитория GitHub NuGetGallery](http://github.com/nuget/NuGetGallery/issues).


## <a name="stay-tuned"></a>Следите за новостями

Пожалуйста, обратите внимание на [наш блог](http://blog.nuget.org) дополнительные хода выполнения и объявления для NuGet 3.0!