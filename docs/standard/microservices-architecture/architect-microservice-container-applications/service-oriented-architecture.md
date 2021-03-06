---
title: Сервисноориентированная архитектура
description: Архитектура микрослужб .NET для упакованных в контейнеры приложений .NET | Сервисноориентированная архитектура
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 05/26/2017
ms.openlocfilehash: 67560cc93b3d147be36a691af440bb78f2315557
ms.sourcegitcommit: 979597cd8055534b63d2c6ee8322938a27d0c87b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/29/2018
ms.locfileid: "37105009"
---
# <a name="service-oriented-architecture"></a>Сервисноориентированная архитектура 

Термин "сервисноориентированная архитектура" (SOA) перегружен значениями и для разных людей означает разные понятия. Но в качестве общего знаменателя термин SOA подразумевает структурирование приложения путем разделения его на несколько служб (наиболее часто HTTP-службы), которые можно классифицировать различными способами, например как подсистемы или уровни.

Теперь эти службы можно развернуть как контейнеры Docker, которые помогают решать проблемы развертывания, так как в образ контейнера включены все зависимости. Однако, если вы используете отдельные узлы Docker, то при необходимости масштабирования приложений SOA вы столкнетесь с проблемами масштабируемости и доступности. Именно для решения таких проблем предназначено программное обеспечение для кластеризации Docker, или оркестратор, которое описано в следующих разделах, где мы расскажем о способах развертывания микрослужб.

Контейнеры Docker являются полезным (но необязательным) элементом как для традиционных архитектур, ориентированных на службы, так и более сложных архитектур с микрослужбами.

Микрослужбы являются производными от архитектуры SOA, но эти архитектуры отличаются друг от друга. Для архитектуры SOA являются типичными такие компоненты, как большие центральные брокеры и центральные оркестраторы на уровне организации, а также [сервисная шина предприятия (ESB)](https://en.wikipedia.org/wiki/Enterprise_service_bus). Но для архитектуры микрослужб в большинстве случаев они являются признаком дурного тона. Некоторые специалисты даже утверждают, что "архитектура микрослужб — это правильно сделанный SOA".

Это руководство посвящено описанию микрослужб, поскольку подход SOA менее требователен по сравнению с требованиями и техниками архитектуры микрослужб. Если вы знаете, как создать приложение на основе технологии микрослужб, то вы сможете создать и простое сервисноориентированное приложение.




>[!div class="step-by-step"]
[Назад](docker-application-state-data.md)
[Вперед](microservices-architecture.md)
