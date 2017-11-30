---
title: "Patrón Anti-Corruption Layer"
description: "Implementa una capa de fachada o de adaptador entre una aplicación moderna y un sistema heredado."
author: dragon119
ms.date: 06/23/2017
ms.openlocfilehash: 590d5f3676c92f5f18661360106e2b2fdd4efbe1
ms.sourcegitcommit: b0482d49aab0526be386837702e7724c61232c60
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/14/2017
---
# <a name="anti-corruption-layer-pattern"></a><span data-ttu-id="5dfbe-103">Patrón Anti-Corruption Layer</span><span class="sxs-lookup"><span data-stu-id="5dfbe-103">Anti-Corruption Layer pattern</span></span>

<span data-ttu-id="5dfbe-104">Implementa una capa de fachada o de adaptador entre una aplicación moderna y un sistema heredado del que depende.</span><span class="sxs-lookup"><span data-stu-id="5dfbe-104">Implement a façade or adapter layer between a modern application and a legacy system that it depends on.</span></span> <span data-ttu-id="5dfbe-105">Esta capa traduce solicitudes entre la aplicación moderna y el sistema heredado.</span><span class="sxs-lookup"><span data-stu-id="5dfbe-105">This layer translates requests between the modern application and the legacy system.</span></span> <span data-ttu-id="5dfbe-106">Use este patrón para asegurarse de que el diseño de la aplicación no se vea limitado por dependencias de sistemas heredados.</span><span class="sxs-lookup"><span data-stu-id="5dfbe-106">Use this pattern to ensure that an application's design is not limited by dependencies on legacy systems.</span></span>

## <a name="context-and-problem"></a><span data-ttu-id="5dfbe-107">Contexto y problema</span><span class="sxs-lookup"><span data-stu-id="5dfbe-107">Context and problem</span></span>

<span data-ttu-id="5dfbe-108">La mayoría de las aplicaciones dependen de otros sistemas para obtener determinados datos o funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="5dfbe-108">Most applications rely on other systems for some data or functionality.</span></span> <span data-ttu-id="5dfbe-109">Por ejemplo, cuando se migra una aplicación heredada a un sistema moderno, es posible que siga necesitando recursos heredados existentes.</span><span class="sxs-lookup"><span data-stu-id="5dfbe-109">For example, when a legacy application is migrated to a modern system, it may still need existing legacy resources.</span></span> <span data-ttu-id="5dfbe-110">Las nuevas características deben poder llamar al sistema heredado.</span><span class="sxs-lookup"><span data-stu-id="5dfbe-110">New features must be able to call the legacy system.</span></span> <span data-ttu-id="5dfbe-111">Esto ocurre especialmente con las migraciones graduales, donde diversas características de una aplicación mayor se trasladan a un sistema moderno con el tiempo.</span><span class="sxs-lookup"><span data-stu-id="5dfbe-111">This is especially true of gradual migrations, where different features of a larger application are moved to a modern system over time.</span></span>

<span data-ttu-id="5dfbe-112">A menudo estos sistemas heredados experimentan problemas de calidad, como esquemas de datos convolucionados o API obsoletas.</span><span class="sxs-lookup"><span data-stu-id="5dfbe-112">Often these legacy systems suffer from quality issues such as convoluted data schemas or obsolete APIs.</span></span> <span data-ttu-id="5dfbe-113">Las características y tecnologías que se usan en sistemas heredados pueden variar ampliamente respecto a las empleadas en sistemas más modernos.</span><span class="sxs-lookup"><span data-stu-id="5dfbe-113">The features and technologies used in legacy systems can vary widely from more modern systems.</span></span> <span data-ttu-id="5dfbe-114">Para interoperar con el sistema heredado, puede que la nueva aplicación necesite admitir elementos no actualizados, como una infraestructura, protocolos, modelos de datos, API u otras características, que de lo contrario no incluiría en una aplicación moderna.</span><span class="sxs-lookup"><span data-stu-id="5dfbe-114">To interoperate with the legacy system, the new application may need to support outdated infrastructure, protocols, data models, APIs, or other features that you wouldn't otherwise put into a modern application.</span></span>

<span data-ttu-id="5dfbe-115">Mantener el acceso entre sistemas nuevos y heredados puede forzar al nuevo sistema a ajustarse a al menos algunas de las API o a una semántica distinta del sistema heredado.</span><span class="sxs-lookup"><span data-stu-id="5dfbe-115">Maintaining access between new and legacy systems can force the new system to adhere to at least some of the legacy system's APIs or other semantics.</span></span> <span data-ttu-id="5dfbe-116">Cuando estas características heredadas tienen problemas de calidad, al admitirlas se "corrompe" lo que, en caso contrario, podría ser una aplicación moderna con un diseño inmaculado.</span><span class="sxs-lookup"><span data-stu-id="5dfbe-116">When these legacy features have quality issues, supporting them "corrupts" what might otherwise be a cleanly designed modern application.</span></span> 

## <a name="solution"></a><span data-ttu-id="5dfbe-117">Solución</span><span class="sxs-lookup"><span data-stu-id="5dfbe-117">Solution</span></span>

<span data-ttu-id="5dfbe-118">Aísle los sistemas heredados y modernos mediante la colocación de una capa para evitar daños (Anti-Corruption Layer) entre ellos.</span><span class="sxs-lookup"><span data-stu-id="5dfbe-118">Isolate the legacy and modern systems by placing an anti-corruption layer between them.</span></span> <span data-ttu-id="5dfbe-119">Esta capa traduce las comunicaciones entre los dos sistemas, lo que permite al sistema heredado permanecer inalterado mientras la aplicación moderna evita comprometer su diseño y su enfoque tecnológico.</span><span class="sxs-lookup"><span data-stu-id="5dfbe-119">This layer translates communications between the two systems, allowing the legacy system to remain unchanged while the modern application can avoid compromising its design and technological approach.</span></span>

![](./_images/anti-corruption-layer.png) 

<span data-ttu-id="5dfbe-120">La comunicación entre la aplicación moderna y la capa para evitar daños siempre utiliza la arquitectura y el modelo de datos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5dfbe-120">Communication between the modern application and the anti-corruption layer always uses the application's data model and architecture.</span></span> <span data-ttu-id="5dfbe-121">Las llamadas de la capa para evitar daños al sistema heredado se ajustan al modelo de datos u otros métodos de ese sistema.</span><span class="sxs-lookup"><span data-stu-id="5dfbe-121">Calls from the anti-corruption layer to the legacy system conform to that system's data model or methods.</span></span> <span data-ttu-id="5dfbe-122">La capa para evitar daños contiene toda la lógica necesaria para traducir entre los dos sistemas.</span><span class="sxs-lookup"><span data-stu-id="5dfbe-122">The anti-corruption layer contains all of the logic necessary to translate between the two systems.</span></span> <span data-ttu-id="5dfbe-123">La capa puede implementarse como un componente dentro de la aplicación o como un servicio independiente.</span><span class="sxs-lookup"><span data-stu-id="5dfbe-123">The layer can be implemented as a component within the application or as an independent service.</span></span>

## <a name="issues-and-considerations"></a><span data-ttu-id="5dfbe-124">Problemas y consideraciones</span><span class="sxs-lookup"><span data-stu-id="5dfbe-124">Issues and considerations</span></span>

- <span data-ttu-id="5dfbe-125">La capa para evitar daños puede añadir latencia a las llamadas entre los dos sistemas.</span><span class="sxs-lookup"><span data-stu-id="5dfbe-125">The anti-corruption layer may add latency to calls made between the two systems.</span></span>
- <span data-ttu-id="5dfbe-126">La capa para evitar daños añade un servicio adicional que debe administrarse y mantenerse.</span><span class="sxs-lookup"><span data-stu-id="5dfbe-126">The anti-corruption layer adds an additional service that must be managed and maintained.</span></span>
- <span data-ttu-id="5dfbe-127">Tenga en cuenta cómo se escalará la capa para evitar daños.</span><span class="sxs-lookup"><span data-stu-id="5dfbe-127">Consider how your anti-corruption layer will scale.</span></span>
- <span data-ttu-id="5dfbe-128">Sopese si va a necesitar más de una capa para evitar daños.</span><span class="sxs-lookup"><span data-stu-id="5dfbe-128">Consider whether you need more than one anti-corruption layer.</span></span> <span data-ttu-id="5dfbe-129">Es posible que desee descomponer la funcionalidad en varios servicios con diferentes tecnologías o lenguajes o que, por otros motivos, desee crear particiones de la capa para evitar daños.</span><span class="sxs-lookup"><span data-stu-id="5dfbe-129">You may want to decompose functionality into multiple services using different technologies or languages, or there may be other reasons to partition the anti-corruption layer.</span></span>
- <span data-ttu-id="5dfbe-130">Tenga en cuenta cómo se administrará la capa para evitar daños en relación con sus otras aplicaciones o servicios.</span><span class="sxs-lookup"><span data-stu-id="5dfbe-130">Consider how the anti-corruption layer will be managed in relation with your other applications or services.</span></span> <span data-ttu-id="5dfbe-131">¿Cómo se integrará en sus procesos de supervisión, lanzamiento y configuración?</span><span class="sxs-lookup"><span data-stu-id="5dfbe-131">How will it be integrated into your monitoring, release, and configuration processes?</span></span>
- <span data-ttu-id="5dfbe-132">Asegúrese de mantener la coherencia de la transacción y los datos y de que se pueda supervisar.</span><span class="sxs-lookup"><span data-stu-id="5dfbe-132">Make sure transaction and data consistency are maintained and can be monitored.</span></span>
- <span data-ttu-id="5dfbe-133">Tenga en cuenta si será necesario que la capa para evitar daños administre todas las comunicaciones entre el sistema heredado y el moderno o si solo deberá controlar un subconjunto de características.</span><span class="sxs-lookup"><span data-stu-id="5dfbe-133">Consider whether the anti-corruption layer needs to handle all communication between legacy and modern systems, or just a subset of features.</span></span> 
- <span data-ttu-id="5dfbe-134">Considere si la capa para evitar daños será permanente o si se retirará más adelante cuando toda la funcionalidad heredada se haya migrado.</span><span class="sxs-lookup"><span data-stu-id="5dfbe-134">Consider whether the anti-corruption layer is meant to be permanent, or eventually retired once all legacy functionality has been migrated.</span></span>

## <a name="when-to-use-this-pattern"></a><span data-ttu-id="5dfbe-135">Cuándo usar este patrón</span><span class="sxs-lookup"><span data-stu-id="5dfbe-135">When to use this pattern</span></span>

<span data-ttu-id="5dfbe-136">Use este patrón cuando:</span><span class="sxs-lookup"><span data-stu-id="5dfbe-136">Use this pattern when:</span></span>

- <span data-ttu-id="5dfbe-137">Se haya planificado una migración en varias fases, pero deba mantenerse la integración entre el sistema nuevo y el heredado.</span><span class="sxs-lookup"><span data-stu-id="5dfbe-137">A migration is planned to happen over multiple stages, but integration between new and legacy systems needs to be maintained.</span></span>
- <span data-ttu-id="5dfbe-138">El sistema nuevo y el heredado usen una semántica diferente, pero necesiten comunicarse.</span><span class="sxs-lookup"><span data-stu-id="5dfbe-138">New and legacy system have different semantics, but still need to communicate.</span></span>

<span data-ttu-id="5dfbe-139">Este patrón puede no ser adecuado si no hay ninguna diferencia semántica importante entre el sistema nuevo y el heredado.</span><span class="sxs-lookup"><span data-stu-id="5dfbe-139">This pattern may not be suitable if there are no significant semantic differences between new and legacy systems.</span></span> 

## <a name="related-guidance"></a><span data-ttu-id="5dfbe-140">Instrucciones relacionadas</span><span class="sxs-lookup"><span data-stu-id="5dfbe-140">Related guidance</span></span>

- <span data-ttu-id="5dfbe-141">[Patrón Strangler][strangler]</span><span class="sxs-lookup"><span data-stu-id="5dfbe-141">[Strangler pattern][strangler]</span></span>

[strangler]: ./strangler.md