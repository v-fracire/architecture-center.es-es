---
title: Estilo de arquitectura de microservicios
description: Describe las ventajas, las dificultades y los procedimientos recomendados para las arquitecturas de microservicios en Azure.
author: MikeWasson
ms.openlocfilehash: 6426b3342a319832baf5eec35e9c783ba9348bdd
ms.sourcegitcommit: b0482d49aab0526be386837702e7724c61232c60
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/14/2017
---
# <a name="microservices-architecture-style"></a><span data-ttu-id="63513-103">Estilo de arquitectura de microservicios</span><span class="sxs-lookup"><span data-stu-id="63513-103">Microservices architecture style</span></span>

<span data-ttu-id="63513-104">Una arquitectura de microservicios consta de una colección de servicios autónomos y pequeños.</span><span class="sxs-lookup"><span data-stu-id="63513-104">A microservices architecture consists of a collection of small, autonomous services.</span></span> <span data-ttu-id="63513-105">Los servicios son independientes entre sí y cada uno debe implementar una funcionalidad de negocio individual.</span><span class="sxs-lookup"><span data-stu-id="63513-105">Each service is self-contained and should implement a single business capability.</span></span> 

![](./images/microservices-logical.svg)
 
<span data-ttu-id="63513-106">En cierto modo, los microservicios son la evolución natural de las arquitecturas orientadas a servicios, pero hay diferencias entre los microservicios y estas arquitecturas.</span><span class="sxs-lookup"><span data-stu-id="63513-106">In some ways, microservices are the natural evolution of service oriented architectures (SOA), but there are differences between microservices and SOA.</span></span> <span data-ttu-id="63513-107">Estas son algunas de las características que definen un microservicio:</span><span class="sxs-lookup"><span data-stu-id="63513-107">Here are some defining characteristics of a microservice:</span></span>

- <span data-ttu-id="63513-108">En una arquitectura de microservicios, los servicios son pequeños e independientes y están acoplados de forma flexible.</span><span class="sxs-lookup"><span data-stu-id="63513-108">In a microservices architecture, services are small, independent, and loosely coupled.</span></span>

- <span data-ttu-id="63513-109">Cada servicio es un código base independiente, que puede administrarse por un equipo de desarrollo pequeño.</span><span class="sxs-lookup"><span data-stu-id="63513-109">Each service is a separate codebase, which can be managed by a small development team.</span></span>

- <span data-ttu-id="63513-110">Los servicios pueden implementarse de manera independiente.</span><span class="sxs-lookup"><span data-stu-id="63513-110">Services can be deployed independently.</span></span> <span data-ttu-id="63513-111">Un equipo puede actualizar un servicio existente sin tener que volver a generar e implementar toda la aplicación.</span><span class="sxs-lookup"><span data-stu-id="63513-111">A team can update an existing service without rebuilding and redeploying the entire application.</span></span>

- <span data-ttu-id="63513-112">Los servicios son los responsables de conservar sus propios datos o estado externo.</span><span class="sxs-lookup"><span data-stu-id="63513-112">Services are responsible for persisting their own data or external state.</span></span> <span data-ttu-id="63513-113">Esto difiere del modelo tradicional, donde una capa de datos independiente controla la persistencia de los datos.</span><span class="sxs-lookup"><span data-stu-id="63513-113">This differs from the traditional model, where a separate data layer handles data persistence.</span></span>

- <span data-ttu-id="63513-114">Los servicios se comunican entre sí mediante API bien definidas.</span><span class="sxs-lookup"><span data-stu-id="63513-114">Services communicate with each other by using well-defined APIs.</span></span> <span data-ttu-id="63513-115">Los detalles de la implementación interna de cada servicio se ocultan frente a otros servicios.</span><span class="sxs-lookup"><span data-stu-id="63513-115">Internal implementation details of each service are hidden from other services.</span></span>

- <span data-ttu-id="63513-116">No es necesario que los servicios compartan la misma pila de tecnología, las bibliotecas o los marcos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="63513-116">Services don't need to share the same technology stack, libraries, or frameworks.</span></span>

<span data-ttu-id="63513-117">Además de los propios servicios, hay otros componentes que aparecen en una arquitectura típica de microservicios:</span><span class="sxs-lookup"><span data-stu-id="63513-117">Besides for the services themselves, some other components appear in a typical microservices architecture:</span></span>

<span data-ttu-id="63513-118">**Administración**.</span><span class="sxs-lookup"><span data-stu-id="63513-118">**Management**.</span></span> <span data-ttu-id="63513-119">El componente de administración es responsable de la colocación de servicios en los nodos, la identificación de errores, el reequilibrio de servicios entre nodos, etc.</span><span class="sxs-lookup"><span data-stu-id="63513-119">The management component is responsible for placing services on nodes, identifying failures, rebalancing services across nodes, and so forth.</span></span>  

<span data-ttu-id="63513-120">**Detección de servicios**.</span><span class="sxs-lookup"><span data-stu-id="63513-120">**Service Discovery**.</span></span>  <span data-ttu-id="63513-121">Mantiene una lista de servicios y los nodos en que se encuentran.</span><span class="sxs-lookup"><span data-stu-id="63513-121">Maintains a list of services and which nodes they are located on.</span></span> <span data-ttu-id="63513-122">Permite la búsqueda de servicios para localizar el punto de conexión de un servicio.</span><span class="sxs-lookup"><span data-stu-id="63513-122">Enables service lookup to find the endpoint for a service.</span></span> 

<span data-ttu-id="63513-123">**Puerta de enlace de API**</span><span class="sxs-lookup"><span data-stu-id="63513-123">**API Gateway**.</span></span> <span data-ttu-id="63513-124">La puerta de enlace de API es el punto de entrada para los clientes.</span><span class="sxs-lookup"><span data-stu-id="63513-124">The API gateway is the entry point for clients.</span></span> <span data-ttu-id="63513-125">Los clientes no llaman directamente a los servicios.</span><span class="sxs-lookup"><span data-stu-id="63513-125">Clients don't call services directly.</span></span> <span data-ttu-id="63513-126">En su lugar, llaman a la puerta de enlace de API, que reenvía la llamada a los servicios apropiados en el back-end.</span><span class="sxs-lookup"><span data-stu-id="63513-126">Instead, they call the API gateway, which forwards the call to the appropriate services on the back end.</span></span> <span data-ttu-id="63513-127">La puerta de enlace de API podría agregar las respuestas de varios servicios y devolver la respuesta agregada.</span><span class="sxs-lookup"><span data-stu-id="63513-127">The API gateway might aggregate the responses from several services and return the aggregated response.</span></span> 

<span data-ttu-id="63513-128">Entre las ventajas del uso de una puerta de enlace de API se encuentran las siguientes:</span><span class="sxs-lookup"><span data-stu-id="63513-128">The advantages of using an API gateway include:</span></span>

- <span data-ttu-id="63513-129">Desacoplan los clientes de los servicios.</span><span class="sxs-lookup"><span data-stu-id="63513-129">It decouples clients from services.</span></span> <span data-ttu-id="63513-130">Los servicios pueden cambiar de versión o refactorizarse sin necesidad de actualizar todos los clientes.</span><span class="sxs-lookup"><span data-stu-id="63513-130">Services can be versioned or refactored without needing to update all of the clients.</span></span>

-  <span data-ttu-id="63513-131">Los servicios pueden utilizar los protocolos de mensajería que no son fáciles de usar para un servicio web, como AMQP.</span><span class="sxs-lookup"><span data-stu-id="63513-131">Services can use messaging protocols that are not web friendly, such as AMQP.</span></span>

- <span data-ttu-id="63513-132">La puerta de enlace de API puede realizar otras funciones transversales como la autenticación, el registro, la terminación SSL y el equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="63513-132">The API Gateway can perform other cross-cutting functions such as authentication, logging, SSL termination, and load balancing.</span></span>

## <a name="when-to-use-this-architecture"></a><span data-ttu-id="63513-133">Cuándo utilizar esta arquitectura</span><span class="sxs-lookup"><span data-stu-id="63513-133">When to use this architecture</span></span>

<span data-ttu-id="63513-134">Considere este estilo de arquitectura para:</span><span class="sxs-lookup"><span data-stu-id="63513-134">Consider this architecture style for:</span></span>

- <span data-ttu-id="63513-135">Aplicaciones grandes que requieren una alta velocidad de publicación.</span><span class="sxs-lookup"><span data-stu-id="63513-135">Large applications that require a high release velocity.</span></span>

- <span data-ttu-id="63513-136">Aplicaciones complejas que necesitan gran escalabilidad.</span><span class="sxs-lookup"><span data-stu-id="63513-136">Complex applications that need to be highly scalable.</span></span>

- <span data-ttu-id="63513-137">Aplicaciones con dominios complejos o muchos subdominios.</span><span class="sxs-lookup"><span data-stu-id="63513-137">Applications with rich domains or many subdomains.</span></span>

- <span data-ttu-id="63513-138">Una organización que disponga de pequeños equipos de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="63513-138">An organization that consists of small development teams.</span></span>


## <a name="benefits"></a><span data-ttu-id="63513-139">Ventajas</span><span class="sxs-lookup"><span data-stu-id="63513-139">Benefits</span></span> 

- <span data-ttu-id="63513-140">**Implementaciones independientes**.</span><span class="sxs-lookup"><span data-stu-id="63513-140">**Independent deployments**.</span></span> <span data-ttu-id="63513-141">Puede actualizar un servicio sin volver a implementar toda la aplicación y revertir o poner al día una actualización si algo va mal.</span><span class="sxs-lookup"><span data-stu-id="63513-141">You can update a service without redeploying the entire application, and roll back or roll forward an update if something goes wrong.</span></span> <span data-ttu-id="63513-142">Las correcciones de errores y las publicaciones de características son más fáciles de administrar y entrañan menos riesgo.</span><span class="sxs-lookup"><span data-stu-id="63513-142">Bug fixes and feature releases are more manageable and less risky.</span></span>

- <span data-ttu-id="63513-143">**Desarrollo independiente**.</span><span class="sxs-lookup"><span data-stu-id="63513-143">**Independent development**.</span></span> <span data-ttu-id="63513-144">Un solo equipo de desarrollo puede compilar, probar e implementar un servicio.</span><span class="sxs-lookup"><span data-stu-id="63513-144">A single development team can build, test, and deploy a service.</span></span> <span data-ttu-id="63513-145">El resultado es la innovación continua y un ritmo más rápido de publicación.</span><span class="sxs-lookup"><span data-stu-id="63513-145">The result is continuous innovation and a faster release cadence.</span></span> 

- <span data-ttu-id="63513-146">**Equipos pequeños y centrados**.</span><span class="sxs-lookup"><span data-stu-id="63513-146">**Small, focused teams**.</span></span> <span data-ttu-id="63513-147">Los equipos pueden centrarse en un servicio.</span><span class="sxs-lookup"><span data-stu-id="63513-147">Teams can focus on one service.</span></span> <span data-ttu-id="63513-148">El menor ámbito de cada servicio hace que la base del código sea más fácil de entender, con lo que los nuevos miembros de los equipos pueden ponerse al día con mayor facilidad.</span><span class="sxs-lookup"><span data-stu-id="63513-148">The smaller scope of each service makes the code base easier to understand, and it's easier for new team members to ramp up.</span></span>

- <span data-ttu-id="63513-149">**Aislamiento de errores**.</span><span class="sxs-lookup"><span data-stu-id="63513-149">**Fault isolation**.</span></span> <span data-ttu-id="63513-150">Si un servicio deja de funcionar, no es necesario paralizar toda la aplicación.</span><span class="sxs-lookup"><span data-stu-id="63513-150">If a service goes down, it won't take out the entire application.</span></span> <span data-ttu-id="63513-151">Sin embargo, eso no significa que obtenga resistencia sin nada a cambio.</span><span class="sxs-lookup"><span data-stu-id="63513-151">However, that doesn't mean you get resiliency for free.</span></span> <span data-ttu-id="63513-152">Tendrá que seguir los procedimientos recomendados de resistencia y los patrones de diseño.</span><span class="sxs-lookup"><span data-stu-id="63513-152">You still need to follow resiliency best practices and design patterns.</span></span> <span data-ttu-id="63513-153">Vea [Diseño de aplicaciones resistentes de Azure][resiliency-overview].</span><span class="sxs-lookup"><span data-stu-id="63513-153">See [Designing resilient applications for Azure][resiliency-overview].</span></span>

- <span data-ttu-id="63513-154">**Pilas de tecnología mixta**.</span><span class="sxs-lookup"><span data-stu-id="63513-154">**Mixed technology stacks**.</span></span> <span data-ttu-id="63513-155">Los equipos pueden elegir la tecnología que mejor se adapte a su servicio.</span><span class="sxs-lookup"><span data-stu-id="63513-155">Teams can pick the technology that best fits their service.</span></span> 

- <span data-ttu-id="63513-156">**Escalado pormenorizado**.</span><span class="sxs-lookup"><span data-stu-id="63513-156">**Granular scaling**.</span></span> <span data-ttu-id="63513-157">Los servicios pueden escalarse de manera independiente.</span><span class="sxs-lookup"><span data-stu-id="63513-157">Services can be scaled independently.</span></span> <span data-ttu-id="63513-158">Al mismo tiempo, la mayor densidad de servicios por máquina virtual implica que los recursos de máquinas virtuales funcionan a máxima capacidad.</span><span class="sxs-lookup"><span data-stu-id="63513-158">At the same time, the higher density of services per VM means that VM resources are fully utilized.</span></span> <span data-ttu-id="63513-159">Con las restricciones de posición, un servicio puede asociarse con un perfil de VM (alta CPU, alta memoria, etc.).</span><span class="sxs-lookup"><span data-stu-id="63513-159">Using placement constraints, a services can be matched to a VM profile (high CPU, high memory, and so on).</span></span>

## <a name="challenges"></a><span data-ttu-id="63513-160">Desafíos</span><span class="sxs-lookup"><span data-stu-id="63513-160">Challenges</span></span>

- <span data-ttu-id="63513-161">**Complejidad**.</span><span class="sxs-lookup"><span data-stu-id="63513-161">**Complexity**.</span></span> <span data-ttu-id="63513-162">Una aplicación de microservicios tiene más partes en movimiento que la aplicación monolítica equivalente.</span><span class="sxs-lookup"><span data-stu-id="63513-162">A microservices application has more moving parts than the equivalent monolithic application.</span></span> <span data-ttu-id="63513-163">Cada servicio es más sencillo, pero el sistema como un todo es más complejo.</span><span class="sxs-lookup"><span data-stu-id="63513-163">Each service is simpler, but the entire system as a whole is more complex.</span></span>

- <span data-ttu-id="63513-164">**Desarrollo y pruebas**.</span><span class="sxs-lookup"><span data-stu-id="63513-164">**Development and test**.</span></span> <span data-ttu-id="63513-165">El desarrollo con dependencias de servicios requiere un enfoque diferente.</span><span class="sxs-lookup"><span data-stu-id="63513-165">Developing against service dependencies requires a different approach.</span></span> <span data-ttu-id="63513-166">Las herramientas existentes no están necesariamente diseñadas para trabajar con dependencias de servicios.</span><span class="sxs-lookup"><span data-stu-id="63513-166">Existing tools are not necessarily designed to work with service dependencies.</span></span> <span data-ttu-id="63513-167">La refactorización en los límites del servicio puede resultar difícil.</span><span class="sxs-lookup"><span data-stu-id="63513-167">Refactoring across service boundaries can be difficult.</span></span> <span data-ttu-id="63513-168">También supone un desafío probar las dependencias de los servicios, especialmente cuando la aplicación está evolucionando rápidamente.</span><span class="sxs-lookup"><span data-stu-id="63513-168">It is also challenging to test service dependencies, especially when the application is evolving quickly.</span></span>

- <span data-ttu-id="63513-169">**Falta de gobernanza**.</span><span class="sxs-lookup"><span data-stu-id="63513-169">**Lack of governance**.</span></span> <span data-ttu-id="63513-170">El enfoque descentralizado para la generación de microservicios tiene ventajas, pero también puede causar problemas.</span><span class="sxs-lookup"><span data-stu-id="63513-170">The decentralized approach to building microservices has advantages, but it can also lead to problems.</span></span> <span data-ttu-id="63513-171">Puede acabar con tantos lenguajes y marcos de trabajo diferentes que la aplicación puede ser difícil de mantener.</span><span class="sxs-lookup"><span data-stu-id="63513-171">You may end up with so many different languages and frameworks that the application becomes hard to maintain.</span></span> <span data-ttu-id="63513-172">Puede resultar útil establecer algunos estándares para todo el proyecto sin restringir excesivamente la flexibilidad de los equipos.</span><span class="sxs-lookup"><span data-stu-id="63513-172">It may be useful to put some project-wide standards in place, without overly restricting teams' flexibility.</span></span> <span data-ttu-id="63513-173">Esto se aplica especialmente a las funcionalidades transversales, como el registro.</span><span class="sxs-lookup"><span data-stu-id="63513-173">This especially applies to cross-cutting functionality such as logging.</span></span>

- <span data-ttu-id="63513-174">**Congestión y latencia de red**.</span><span class="sxs-lookup"><span data-stu-id="63513-174">**Network congestion and latency**.</span></span> <span data-ttu-id="63513-175">El uso de muchos servicios pequeños y detallados puede dar lugar a más comunicación interservicios.</span><span class="sxs-lookup"><span data-stu-id="63513-175">The use of many small, granular services can result in more interservice communication.</span></span> <span data-ttu-id="63513-176">Además, si la cadena de dependencias del servicio se hace demasiado larga (el servicio A llama a B, que llama a C...), la latencia adicional puede constituir un problema.</span><span class="sxs-lookup"><span data-stu-id="63513-176">Also, if the chain of service dependencies gets too long (service A calls B, which calls C...), the additional latency can become a problem.</span></span> <span data-ttu-id="63513-177">Tendrá que diseñar las API con atención.</span><span class="sxs-lookup"><span data-stu-id="63513-177">You will need to design APIs carefully.</span></span> <span data-ttu-id="63513-178">Evite que las API se comuniquen demasiado, piense en formatos de serialización y busque lugares para utilizar patrones de comunicación asincrónica.</span><span class="sxs-lookup"><span data-stu-id="63513-178">Avoid overly chatty APIs, think about serialization formats, and look for places to use asynchronous communication patterns.</span></span>

- <span data-ttu-id="63513-179">**Integridad de datos**.</span><span class="sxs-lookup"><span data-stu-id="63513-179">**Data integrity**.</span></span> <span data-ttu-id="63513-180">Cada microservicio es responsable de la conservación de sus propios datos.</span><span class="sxs-lookup"><span data-stu-id="63513-180">With each microservice responsible for its own data persistence.</span></span> <span data-ttu-id="63513-181">Como consecuencia, la coherencia de los datos puede suponer un problema.</span><span class="sxs-lookup"><span data-stu-id="63513-181">As a result, data consistency can be a challenge.</span></span> <span data-ttu-id="63513-182">Adopte una coherencia final cuando sea posible.</span><span class="sxs-lookup"><span data-stu-id="63513-182">Embrace eventual consistency where possible.</span></span>

- <span data-ttu-id="63513-183">**Administración**.</span><span class="sxs-lookup"><span data-stu-id="63513-183">**Management**.</span></span> <span data-ttu-id="63513-184">Para tener éxito con los microservicios se necesita una cultura de DevOps consolidada.</span><span class="sxs-lookup"><span data-stu-id="63513-184">To be successful with microservices requires a mature DevOps culture.</span></span> <span data-ttu-id="63513-185">El registro correlacionado entre servicios puede resultar un desafío.</span><span class="sxs-lookup"><span data-stu-id="63513-185">Correlated logging across services can be challenging.</span></span> <span data-ttu-id="63513-186">Normalmente, el registro debe correlacionar varias llamadas de servicio para una sola operación de usuario.</span><span class="sxs-lookup"><span data-stu-id="63513-186">Typically, logging must correlate multiple service calls for a single user operation.</span></span>

- <span data-ttu-id="63513-187">**Control de versiones**.</span><span class="sxs-lookup"><span data-stu-id="63513-187">**Versioning**.</span></span> <span data-ttu-id="63513-188">Las actualizaciones de un servicio no deben interrumpir servicios que dependen de él.</span><span class="sxs-lookup"><span data-stu-id="63513-188">Updates to a service must not break services that depend on it.</span></span> <span data-ttu-id="63513-189">Es posible que varios servicios se actualicen en cualquier momento; por lo tanto, sin un cuidadoso diseño, podrían surgir problemas con la compatibilidad con versiones anteriores o posteriores.</span><span class="sxs-lookup"><span data-stu-id="63513-189">Multiple services could be updated at any given time, so without careful design, you might have problems with backward or forward compatibility.</span></span>

- <span data-ttu-id="63513-190">**Conjunto de habilidades**.</span><span class="sxs-lookup"><span data-stu-id="63513-190">**Skillset**.</span></span> <span data-ttu-id="63513-191">Los microservicios son sistemas muy distribuidos.</span><span class="sxs-lookup"><span data-stu-id="63513-191">Microservices are highly distributed systems.</span></span> <span data-ttu-id="63513-192">Evalúe cuidadosamente si el equipo tiene los conocimientos y la experiencia para desenvolverse correctamente.</span><span class="sxs-lookup"><span data-stu-id="63513-192">Carefully evaluate whether the team has the skills and experience to be successful.</span></span>

## <a name="best-practices"></a><span data-ttu-id="63513-193">Prácticas recomendadas</span><span class="sxs-lookup"><span data-stu-id="63513-193">Best practices</span></span>

- <span data-ttu-id="63513-194">Adapte los servicios al dominio empresarial.</span><span class="sxs-lookup"><span data-stu-id="63513-194">Model services around the business domain.</span></span> 

- <span data-ttu-id="63513-195">Descentralice todo.</span><span class="sxs-lookup"><span data-stu-id="63513-195">Decentralize everything.</span></span> <span data-ttu-id="63513-196">Los equipos individuales son responsables de diseñar y compilar servicios.</span><span class="sxs-lookup"><span data-stu-id="63513-196">Individual teams are responsible for designing and building services.</span></span> <span data-ttu-id="63513-197">Evite el uso compartido de código o esquemas de datos.</span><span class="sxs-lookup"><span data-stu-id="63513-197">Avoid sharing code or data schemas.</span></span> 

- <span data-ttu-id="63513-198">El almacenamiento de datos debería ser privado para el servicio que posee los datos.</span><span class="sxs-lookup"><span data-stu-id="63513-198">Data storage should be private to the service that owns the data.</span></span> <span data-ttu-id="63513-199">Use el almacenamiento recomendado para cada tipo de servicio y de datos.</span><span class="sxs-lookup"><span data-stu-id="63513-199">Use the best storage for each service and data type.</span></span> 

- <span data-ttu-id="63513-200">Los servicios se comunican a través de API bien diseñadas.</span><span class="sxs-lookup"><span data-stu-id="63513-200">Services communicate through well-designed APIs.</span></span> <span data-ttu-id="63513-201">Evite la pérdida de detalles de la implementación.</span><span class="sxs-lookup"><span data-stu-id="63513-201">Avoid leaking implementation details.</span></span> <span data-ttu-id="63513-202">Las API deben modelar el dominio, no la implementación interna del servicio.</span><span class="sxs-lookup"><span data-stu-id="63513-202">APIs should model the domain, not the internal implementation of the service.</span></span>

- <span data-ttu-id="63513-203">Evite el acoplamiento entre servicios.</span><span class="sxs-lookup"><span data-stu-id="63513-203">Avoid coupling between services.</span></span> <span data-ttu-id="63513-204">Entre las causas de acoplamiento se encuentran los protocolos de comunicación rígidos y los esquemas de bases de datos compartidos.</span><span class="sxs-lookup"><span data-stu-id="63513-204">Causes of coupling include shared database schemas and rigid communication protocols.</span></span>

- <span data-ttu-id="63513-205">Descargue a la puerta de enlace de cuestiones transversales, como la autenticación y la terminación SSL.</span><span class="sxs-lookup"><span data-stu-id="63513-205">Offload cross-cutting concerns, such as authentication and SSL termination, to the gateway.</span></span>

- <span data-ttu-id="63513-206">Conserve el conocimiento del dominio fuera de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="63513-206">Keep domain knowledge out of the gateway.</span></span> <span data-ttu-id="63513-207">La puerta de enlace debe controlar y enrutar las solicitudes de cliente sin ningún conocimiento de las reglas de negocios o la lógica de dominio.</span><span class="sxs-lookup"><span data-stu-id="63513-207">The gateway should handle and route client requests without any knowledge of the business rules or domain logic.</span></span> <span data-ttu-id="63513-208">En caso contrario, la puerta de enlace se convierte en una dependencia y puede provocar el acoplamiento entre servicios.</span><span class="sxs-lookup"><span data-stu-id="63513-208">Otherwise, the gateway becomes a dependency and can cause coupling between services.</span></span>

- <span data-ttu-id="63513-209">Los servicios deben tener un acoplamiento flexible y una alta cohesión funcional.</span><span class="sxs-lookup"><span data-stu-id="63513-209">Services should have loose coupling and high functional cohesion.</span></span> <span data-ttu-id="63513-210">Las funciones que es probable que cambien juntas se deben empaquetar e implementar en conjunto.</span><span class="sxs-lookup"><span data-stu-id="63513-210">Functions that are likely to change together should be packaged and deployed together.</span></span> <span data-ttu-id="63513-211">Si residen en distintos servicios, estos terminan estrechamente acoplados, porque un cambio en un servicio requerirá la actualización del otro servicio.</span><span class="sxs-lookup"><span data-stu-id="63513-211">If they reside in separate services, those services end up being tightly coupled, because a change in one service will require updating the other service.</span></span> <span data-ttu-id="63513-212">La comunicación demasiado intensa entre dos servicios puede ser un síntoma de un acoplamiento estrecho y una cohesión baja.</span><span class="sxs-lookup"><span data-stu-id="63513-212">Overly chatty communication between two services may be a symptom of tight coupling and low cohesion.</span></span> 

- <span data-ttu-id="63513-213">Aísle los errores.</span><span class="sxs-lookup"><span data-stu-id="63513-213">Isolate failures.</span></span> <span data-ttu-id="63513-214">Utilice estrategias de resistencia para impedir que los errores dentro de un servicio se reproduzcan en cascada.</span><span class="sxs-lookup"><span data-stu-id="63513-214">Use resiliency strategies to prevent failures within a service from cascading.</span></span> <span data-ttu-id="63513-215">Vea [Resiliency patterns][resiliency-patterns] (Patrones de resistencia) y [Diseño de aplicaciones resistentes de Azure][resiliency-overview].</span><span class="sxs-lookup"><span data-stu-id="63513-215">See [Resiliency patterns][resiliency-patterns] and [Designing resilient applications][resiliency-overview].</span></span>

## <a name="microservices-using-azure-container-service"></a><span data-ttu-id="63513-216">Microservicios que utilizan Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="63513-216">Microservices using Azure Container Service</span></span> 

<span data-ttu-id="63513-217">Puede usar Azure Container Service para configurar y aprovisionar un clúster de Docker.</span><span class="sxs-lookup"><span data-stu-id="63513-217">You can use Azure Container Service to configure and provision a Docker cluster.</span></span> <span data-ttu-id="63513-218">Azure Container Service admite diferentes orquestadores de contenedores populares, como Kubernetes, DC/OS y Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="63513-218">Azure Container Services supports several popular container orchestrators, including Kubernetes, DC/OS, and Docker Swarm.</span></span>

![](./images/microservices-acs.png)
 
<span data-ttu-id="63513-219">**Nodos públicos**.</span><span class="sxs-lookup"><span data-stu-id="63513-219">**Public nodes**.</span></span> <span data-ttu-id="63513-220">Estos nodos son accesibles a través de un equilibrador de carga orientado al público.</span><span class="sxs-lookup"><span data-stu-id="63513-220">These nodes are reachable through a public-facing load balancer.</span></span> <span data-ttu-id="63513-221">La puerta de enlace de API se hospeda en esos nodos.</span><span class="sxs-lookup"><span data-stu-id="63513-221">The API gateway is hosted on these nodes.</span></span>

<span data-ttu-id="63513-222">**Nodos de back-end**.</span><span class="sxs-lookup"><span data-stu-id="63513-222">**Backend nodes**.</span></span> <span data-ttu-id="63513-223">Estos nodos ejecutan servicios a los que acceden los clientes a través de la puerta de enlace de API.</span><span class="sxs-lookup"><span data-stu-id="63513-223">These nodes run services that clients reach via the API gateway.</span></span> <span data-ttu-id="63513-224">Estos nodos no reciben el tráfico de Internet directamente.</span><span class="sxs-lookup"><span data-stu-id="63513-224">These nodes don't receive Internet traffic directly.</span></span> <span data-ttu-id="63513-225">Los nodos de back-end pueden incluir más de un grupo de máquinas virtuales, cada uno con un perfil de hardware diferente.</span><span class="sxs-lookup"><span data-stu-id="63513-225">The backend nodes might include more than one pool of VMs, each with a different hardware profile.</span></span> <span data-ttu-id="63513-226">Por ejemplo, podría crear grupos diferentes para cargas de trabajo de proceso generales, cargas de trabajo de CPU elevadas y cargas de trabajo de memoria elevadas.</span><span class="sxs-lookup"><span data-stu-id="63513-226">For example, you could create separate pools for general compute workloads, high CPU workloads, and high memory workloads.</span></span> 

<span data-ttu-id="63513-227">**Máquinas virtuales de administración**</span><span class="sxs-lookup"><span data-stu-id="63513-227">**Management VMs**.</span></span> <span data-ttu-id="63513-228">Estas máquinas virtuales ejecutan los nodos principales para el orquestador de contenedores.</span><span class="sxs-lookup"><span data-stu-id="63513-228">These VMs run the master nodes for the container orchestrator.</span></span> 

<span data-ttu-id="63513-229">**Redes**.</span><span class="sxs-lookup"><span data-stu-id="63513-229">**Networking**.</span></span> <span data-ttu-id="63513-230">Los nodos públicos, los nodos de back-end y las máquinas virtuales de administración se colocan en subredes diferentes dentro de la misma red virtual (VNet).</span><span class="sxs-lookup"><span data-stu-id="63513-230">The public nodes, backend nodes, and management VMs are placed in separate subnets within the same virtual network (VNet).</span></span> 

<span data-ttu-id="63513-231">**Equilibradores de carga.**</span><span class="sxs-lookup"><span data-stu-id="63513-231">**Load balancers**.</span></span>  <span data-ttu-id="63513-232">Un equilibrador de carga con orientación externa se coloca delante de los nodos públicos.</span><span class="sxs-lookup"><span data-stu-id="63513-232">An externally facing load balancer sits in front of the public nodes.</span></span> <span data-ttu-id="63513-233">Distribuye las solicitudes de Internet a los nodos públicos.</span><span class="sxs-lookup"><span data-stu-id="63513-233">It distributes internet requests to the public nodes.</span></span> <span data-ttu-id="63513-234">Otro equilibrador de carga se coloca delante de las máquinas virtuales de administración para permitir el tráfico de Secure Shell (ssh) a las máquinas virtuales de administración mediante las reglas NAT.</span><span class="sxs-lookup"><span data-stu-id="63513-234">Another load balancer is placed in front of the management VMs, to allow secure shell (ssh) traffic to the management VMs, using NAT rules.</span></span>

<span data-ttu-id="63513-235">Por motivos de confiabilidad y escalabilidad, cada servicio se replica a través de varias máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="63513-235">For reliability and scalability, each service is replicated across multiple VMs.</span></span> <span data-ttu-id="63513-236">Sin embargo, como los servicios son relativamente ligeros (en comparación con una aplicación monolítica), varios servicios normalmente se empaquetan en una sola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="63513-236">However, because services are also relatively lightweight (compared with a monolithic application), multiple services are usually packed into a single VM.</span></span> <span data-ttu-id="63513-237">Una mayor densidad permite una mejor utilización de recursos.</span><span class="sxs-lookup"><span data-stu-id="63513-237">Higher density allows better resource utilization.</span></span> <span data-ttu-id="63513-238">Si un servicio determinado no usa una gran cantidad de recursos, no es necesario dedicar una máquina virtual completa a la ejecución de ese servicio.</span><span class="sxs-lookup"><span data-stu-id="63513-238">If a particular service doesn't use a lot of resources, you don't need to dedicate an entire VM to running that service.</span></span>

<span data-ttu-id="63513-239">El siguiente diagrama muestra tres nodos que ejecutan cuatro servicios diferentes (indicados mediante distintas formas).</span><span class="sxs-lookup"><span data-stu-id="63513-239">The following diagram shows three nodes running four different services (indicated by different shapes).</span></span> <span data-ttu-id="63513-240">Observe que cada servicio tiene al menos dos instancias.</span><span class="sxs-lookup"><span data-stu-id="63513-240">Notice that each service has at least two instances.</span></span> 
 
![](./images/microservices-node-density.png)

## <a name="microservices-using-azure-service-fabric"></a><span data-ttu-id="63513-241">Microservicios que utilizan Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="63513-241">Microservices using Azure Service Fabric</span></span>

<span data-ttu-id="63513-242">El siguiente diagrama muestra una arquitectura de microservicios que utiliza Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="63513-242">The following diagram shows a microservices architecture using Azure Service Fabric.</span></span>

![](./images/service-fabric.png)

<span data-ttu-id="63513-243">El clúster de Service Fabric se implementa en uno o varios conjuntos de escalado de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="63513-243">The Service Fabric Cluster is deployed to one or more VM scale sets.</span></span> <span data-ttu-id="63513-244">Puede que tenga más de un conjunto de escalado de máquina virtual en el clúster, con el fin de tener una combinación de tipos de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="63513-244">You might have more than one VM scale set in the cluster, in order to have a mix of VM types.</span></span> <span data-ttu-id="63513-245">Una puerta de enlace de API se coloca delante del clúster de Service Fabric, con un equilibrador de carga externo para recibir las solicitudes de cliente.</span><span class="sxs-lookup"><span data-stu-id="63513-245">An API Gateway is placed in front of the Service Fabric cluster, with an external load balancer to receive client requests.</span></span>

<span data-ttu-id="63513-246">El tiempo de ejecución de Service Fabric se ocupa de la administración del clúster; esto es, la selección de ubicación de los servicios, la conmutación por error de los nodos y el seguimiento de los estados, entre otros.</span><span class="sxs-lookup"><span data-stu-id="63513-246">The Service Fabric runtime performs cluster management, including service placement, node failover, and health monitoring.</span></span> <span data-ttu-id="63513-247">El tiempo de ejecución se implementa en los propios nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="63513-247">The runtime is deployed on the cluster nodes themselves.</span></span> <span data-ttu-id="63513-248">No hay un conjunto independiente de máquinas virtuales de administración del clúster.</span><span class="sxs-lookup"><span data-stu-id="63513-248">There isn't a separate set of cluster management VMs.</span></span>

<span data-ttu-id="63513-249">Los servicios se comunican entre sí mediante el proxy inverso que está integrado en Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="63513-249">Services communicate with each other using the reverse proxy that is built into Service Fabric.</span></span> <span data-ttu-id="63513-250">Service Fabric proporciona un servicio de detección que puede resolver el punto de conexión para un servicio con nombre.</span><span class="sxs-lookup"><span data-stu-id="63513-250">Service Fabric provides a discovery service that can resolve the endpoint for a named service.</span></span>


<!-- links -->

[resiliency-overview]: ../../resiliency/index.md
[resiliency-patterns]: ../../patterns/category/resiliency.md


