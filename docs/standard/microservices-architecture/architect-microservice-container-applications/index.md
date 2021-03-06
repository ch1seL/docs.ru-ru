---
title: Проектирование архитектуры приложений на основе контейнеров и микрослужб
description: Архитектура микрослужб .NET для упакованных в контейнеры приложений .NET | Проектирование архитектуры приложений на основе контейнеров и микрослужб
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 05/26/2017
ms.openlocfilehash: 185279cb4df70d9896d7e11c995170e7cd214f73
ms.sourcegitcommit: 979597cd8055534b63d2c6ee8322938a27d0c87b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/29/2018
ms.locfileid: "37106818"
---
# <a name="architecting-container--and-microservice-based-applications"></a>Проектирование архитектуры приложений на основе контейнеров и микрослужб

*Микрослужбы дают большие преимущества, но в то же время создают новые проблемы. Шаблоны архитектуры микрослужб являются основополагающим элементом при создании приложения на основе микрослужб.*

Ранее в этом руководстве вы ознакомились с основными понятиями, связанными с контейнерами и Docker. Это минимальная информация, необходимая для того, чтобы приступить к работе с контейнерами. Хотя контейнеры обеспечивают широкие возможности и отлично подходят для микрослужб, они не обязательны для архитектуры микрослужб. Многие архитектурные решения, описываемые в этом разделе, можно реализовать и без контейнеров. Но в данном руководстве основное внимание уделяется совместному использованию этих сущностей из-за уже упоминавшейся важности контейнеров.

Корпоративные приложения могут быть сложными и часто состоят из нескольких служб, а не одной. В таких случаях необходимо разбираться в дополнительных подходах к проектированию архитектуры, таких как использование микрослужб, а также определенных шаблонах проектирования на основе доменов и принципах оркестрации контейнеров. Имейте в виду, что в этой главе описываются не только микрослужбы в контейнерах, но и любые контейнерные приложения.

## <a name="container-design-principles"></a>Принципы проектирования контейнеров

В модели на основе контейнеров экземпляр образа контейнера представляет отдельный процесс. Определив образ контейнера как границу процесса, вы можете создавать примитивы, с помощью которых можно масштабировать процесс или помещать его в пакет.

Когда вы проектируете образ контейнера, в Dockerfile имеется определение [ENTRYPOINT](https://docs.docker.com/engine/reference/builder/). С его помощью определяется процесс, время существования которого контролирует время существования контейнера. По завершении процесса время существования контейнера истекает. Контейнеры могут представлять как длительные процессы, например веб-серверы, так и кратковременные, например пакетные задания, которые ранее могли реализовываться как [веб-задания](https://docs.microsoft.com/azure/app-service-web/websites-webjobs-resources) Azure.

В случае сбоя процесса работа контейнера завершается и оркестратор принимает управление. Если в оркестраторе настроена поддержка пяти выполняющихся экземпляров, то в случае сбоя одного из них оркестратор создаст ему на замену еще один экземпляр контейнера. В пакетном задании процесс запускается с параметрами. По завершении выполнения процесса работа считается выполненной. В этом руководстве оркестраторы будут рассматриваться более подробно позже.

Возможны ситуации, когда в одном контейнере желательно выполнять несколько процессов. Так как каждый контейнер может иметь только одну точку входа, в таком случае в контейнере можно использовать скрипт, который будет запускать нужное количество программ. Например, можно использовать [Supervisor](http://supervisord.org/) или аналогичное средство, отвечающее за запуск нескольких процессов в одном контейнере. Но хотя архитектуры, предусматривающие несколько процессов в контейнере, встречаются, такой подход применяется нечасто.


>[!div class="step-by-step"]
[Назад](../net-core-net-framework-containers/official-net-docker-images.md)
[Вперед](containerize-monolithic-applications.md)
