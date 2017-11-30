---
title: "Aplicación web escalable"
description: "Mejora de la escalabilidad en una aplicación web que se ejecuta en Microsoft Azure"
author: MikeWasson
pnp.series.title: Azure App Service
pnp.series.prev: basic-web-app
pnp.series.next: multi-region-web-app
ms.date: 11/23/2016
cardTitle: Improve scalability
ms.openlocfilehash: b875b89b87edd5636d90da8b7f8211f965b39937
ms.sourcegitcommit: b0482d49aab0526be386837702e7724c61232c60
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/14/2017
---
# <a name="improve-scalability-in-a-web-application"></a><span data-ttu-id="ed69f-103">Mejora de la escalabilidad en una aplicación web</span><span class="sxs-lookup"><span data-stu-id="ed69f-103">Improve scalability in a web application</span></span>

<span data-ttu-id="ed69f-104">Esta arquitectura de referencia muestra procedimientos de demostrada eficacia para mejorar la escalabilidad y el rendimiento en una aplicación web de Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="ed69f-104">This reference architecture shows proven practices for improving scalability and performance in an Azure App Service web application.</span></span>

<span data-ttu-id="ed69f-105">![[0]][0]</span><span class="sxs-lookup"><span data-stu-id="ed69f-105">![[0]][0]</span></span>

<span data-ttu-id="ed69f-106">*Descargue un [archivo Visio][visio-download] de esta arquitectura.*</span><span class="sxs-lookup"><span data-stu-id="ed69f-106">*Download a [Visio file][visio-download] of this architecture.*</span></span>

## <a name="architecture"></a><span data-ttu-id="ed69f-107">Arquitectura</span><span class="sxs-lookup"><span data-stu-id="ed69f-107">Architecture</span></span>  

<span data-ttu-id="ed69f-108">Esta arquitectura se basa en la que se muestra en [Aplicación web básica][basic-web-app].</span><span class="sxs-lookup"><span data-stu-id="ed69f-108">This architecture builds on the one shown in [Basic web application][basic-web-app].</span></span> <span data-ttu-id="ed69f-109">Incluye los siguientes componentes:</span><span class="sxs-lookup"><span data-stu-id="ed69f-109">It includes the following components:</span></span>

* <span data-ttu-id="ed69f-110">**Grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="ed69f-110">**Resource group**.</span></span> <span data-ttu-id="ed69f-111">Un [grupo de recursos][resource-group] es un contenedor lógico de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="ed69f-111">A [resource group][resource-group] is a logical container for Azure resources.</span></span>
* <span data-ttu-id="ed69f-112">**[Aplicación web][app-service-web-app]** y **[aplicación de API][app-service-api-app]**.</span><span class="sxs-lookup"><span data-stu-id="ed69f-112">**[Web app][app-service-web-app]** and **[API app][app-service-api-app]**.</span></span> <span data-ttu-id="ed69f-113">Una aplicación moderna típica podría incluir un sitio web y una o varias web API web de RESTful.</span><span class="sxs-lookup"><span data-stu-id="ed69f-113">A typical modern application might include both a website and one or more RESTful web APIs.</span></span> <span data-ttu-id="ed69f-114">Los clientes del explorador podrían consumir una API web mediante AJAX, y también las aplicaciones nativas o las aplicaciones del lado servidor podrían consumirla.</span><span class="sxs-lookup"><span data-stu-id="ed69f-114">A web API might be consumed by browser clients through AJAX, by native client applications, or by server-side applications.</span></span> <span data-ttu-id="ed69f-115">Para conocer las consideraciones sobre el diseño de las API web, consulte la [guía de diseño de API][api-guidance].</span><span class="sxs-lookup"><span data-stu-id="ed69f-115">For considerations on designing web APIs, see [API design guidance][api-guidance].</span></span>    
* <span data-ttu-id="ed69f-116">**WebJob**.</span><span class="sxs-lookup"><span data-stu-id="ed69f-116">**WebJob**.</span></span> <span data-ttu-id="ed69f-117">Use [Azure WebJobs][webjobs] para ejecutar tareas de ejecución prolongada en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="ed69f-117">Use [Azure WebJobs][webjobs] to run long-running tasks in the background.</span></span> <span data-ttu-id="ed69f-118">Los trabajos web se pueden ejecutar de forma programada, continuamente o en respuesta a un desencadenador, como poner un mensaje en una cola.</span><span class="sxs-lookup"><span data-stu-id="ed69f-118">WebJobs can run on a schedule, continously, or in response to a trigger, such as putting a message on a queue.</span></span> <span data-ttu-id="ed69f-119">Un trabajo web se ejecuta como un proceso en segundo plano en el contexto de una aplicación de App Service.</span><span class="sxs-lookup"><span data-stu-id="ed69f-119">A WebJob runs as a background process in the context of an App Service app.</span></span>
* <span data-ttu-id="ed69f-120">**Cola**.</span><span class="sxs-lookup"><span data-stu-id="ed69f-120">**Queue**.</span></span> <span data-ttu-id="ed69f-121">En la arquitectura que se muestra aquí, la aplicación pone en cola las tareas en segundo plano mediante la colocación de un mensaje en una cola de [Azure Queue Storage][queue-storage].</span><span class="sxs-lookup"><span data-stu-id="ed69f-121">In the architecture shown here, the application queues background tasks by putting a message onto an [Azure Queue storage][queue-storage] queue.</span></span> <span data-ttu-id="ed69f-122">El mensaje desencadena una función en el trabajo web.</span><span class="sxs-lookup"><span data-stu-id="ed69f-122">The message triggers a function in the WebJob.</span></span> <span data-ttu-id="ed69f-123">Como alternativa, puede usar colas de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="ed69f-123">Alternatively, you can use Service Bus queues.</span></span> <span data-ttu-id="ed69f-124">Para ver una comparación, consulte [Colas de Storage y de Service Bus: comparación y diferencias][queues-compared].</span><span class="sxs-lookup"><span data-stu-id="ed69f-124">For a comparison, see [Azure Queues and Service Bus queues - compared and contrasted][queues-compared].</span></span>
* <span data-ttu-id="ed69f-125">**Caché**.</span><span class="sxs-lookup"><span data-stu-id="ed69f-125">**Cache**.</span></span> <span data-ttu-id="ed69f-126">Almacene datos parcialmente estáticos en [Azure Redis Cache][azure-redis].</span><span class="sxs-lookup"><span data-stu-id="ed69f-126">Store semi-static data in [Azure Redis Cache][azure-redis].</span></span>  
* <span data-ttu-id="ed69f-127">**CDN**.</span><span class="sxs-lookup"><span data-stu-id="ed69f-127">**CDN**.</span></span> <span data-ttu-id="ed69f-128">Use [Azure Content Delivery Network][ azure-cdn] (CDN) para almacenar en caché el contenido disponible públicamente y así reducir latencia y acelerar la entrega de contenido.</span><span class="sxs-lookup"><span data-stu-id="ed69f-128">Use [Azure Content Delivery Network][azure-cdn] (CDN) to cache publicly available content for lower latency and faster delivery of content.</span></span>
* <span data-ttu-id="ed69f-129">**Almacenamiento de datos**.</span><span class="sxs-lookup"><span data-stu-id="ed69f-129">**Data storage**.</span></span> <span data-ttu-id="ed69f-130">Use [Azure SQL Database][sql-db] con datos relacionales.</span><span class="sxs-lookup"><span data-stu-id="ed69f-130">Use [Azure SQL Database][sql-db] for relational data.</span></span> <span data-ttu-id="ed69f-131">Con datos no relacionales, podría usar un almacén NoSQL, como [Cosmos DB][documentdb].</span><span class="sxs-lookup"><span data-stu-id="ed69f-131">For non-relational data, consider a NoSQL store, such as [Cosmos DB][documentdb].</span></span>
* <span data-ttu-id="ed69f-132">**Azure Search**.</span><span class="sxs-lookup"><span data-stu-id="ed69f-132">**Azure Search**.</span></span> <span data-ttu-id="ed69f-133">Use [Azure Search][azure-search] para agregar funcionalidad de búsqueda, como sugerencias de búsqueda, búsqueda aproximada y búsqueda específica del idioma.</span><span class="sxs-lookup"><span data-stu-id="ed69f-133">Use [Azure Search][azure-search] to add search functionality such as search suggestions, fuzzy search, and language-specific search.</span></span> <span data-ttu-id="ed69f-134">Azure Search se usa normalmente en combinación con otro almacén de datos, en especial si el almacén de datos principal requiere una coherencia estricta.</span><span class="sxs-lookup"><span data-stu-id="ed69f-134">Azure Search is typically used in conjunction with another data store, especially if the primary data store requires strict consistency.</span></span> <span data-ttu-id="ed69f-135">En este enfoque, almacene los datos acreditado en el otro almacén de datos y el índice de búsqueda en Azure Search.</span><span class="sxs-lookup"><span data-stu-id="ed69f-135">In this approach, store authoritative data in the other data store and the search index in Azure Search.</span></span> <span data-ttu-id="ed69f-136">Azure Search también se puede usar para consolidar un índice de búsqueda sencillo desde varios almacenes de datos.</span><span class="sxs-lookup"><span data-stu-id="ed69f-136">Azure Search can also be used to consolidate a single search index from multiple data stores.</span></span>  
* <span data-ttu-id="ed69f-137">**Correo electrónico/SMS**.</span><span class="sxs-lookup"><span data-stu-id="ed69f-137">**Email/SMS**.</span></span> <span data-ttu-id="ed69f-138">Use un servicio de terceros como SendGrid o Twilio para enviar correo electrónico o mensajes SMS en lugar de generar esta funcionalidad directamente en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ed69f-138">Use a third-party service such as SendGrid or Twilio to send email or SMS messages instead of building this functionality directly into the application.</span></span>

## <a name="recommendations"></a><span data-ttu-id="ed69f-139">Recomendaciones</span><span class="sxs-lookup"><span data-stu-id="ed69f-139">Recommendations</span></span>

<span data-ttu-id="ed69f-140">Los requisitos pueden diferir de los de la arquitectura que se describe aquí.</span><span class="sxs-lookup"><span data-stu-id="ed69f-140">Your requirements might differ from the architecture described here.</span></span> <span data-ttu-id="ed69f-141">Use las recomendaciones de esta sección como punto de partida.</span><span class="sxs-lookup"><span data-stu-id="ed69f-141">Use the recommendations in this section as a starting point.</span></span>

### <a name="app-service-apps"></a><span data-ttu-id="ed69f-142">Aplicaciones de App Service</span><span class="sxs-lookup"><span data-stu-id="ed69f-142">App Service apps</span></span>
<span data-ttu-id="ed69f-143">Se recomienda crear la aplicación web y la API web como aplicaciones de App Service independientes.</span><span class="sxs-lookup"><span data-stu-id="ed69f-143">We recommend creating the web application and the web API as separate App Service apps.</span></span> <span data-ttu-id="ed69f-144">Este diseño permite ejecutarlas en planes de App Service diferentes, por lo que se pueden escalar de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="ed69f-144">This design lets you run them in separate App Service plans so they can be scaled independently.</span></span> <span data-ttu-id="ed69f-145">Si inicialmente no necesita ese nivel de escalabilidad, puede implementar las aplicaciones en el mismo plan y moverlas más tarde a planes diferentes si es necesario.</span><span class="sxs-lookup"><span data-stu-id="ed69f-145">If you don't need that level of scalability initially, you can deploy the apps into the same plan and move them into separate plans later if necessary.</span></span>

> [!NOTE]
> <span data-ttu-id="ed69f-146">Los planes Básico, Estándar y Premium se facturan por las instancias de máquina virtual, no por aplicación.</span><span class="sxs-lookup"><span data-stu-id="ed69f-146">For the Basic, Standard, and Premium plans, you are billed for the VM instances in the plan, not per app.</span></span> <span data-ttu-id="ed69f-147">Consulte [Precios de App Service][app-service-pricing].</span><span class="sxs-lookup"><span data-stu-id="ed69f-147">See [App Service Pricing][app-service-pricing]</span></span>
> 
> 

<span data-ttu-id="ed69f-148">Si tiene pensado usar las características *Tablas fáciles* o *API fáciles* de App Service Mobile Apps, cree una aplicación de App Service distinta para este fin.</span><span class="sxs-lookup"><span data-stu-id="ed69f-148">If you intend to use the *Easy Tables* or *Easy APIs* features of App Service Mobile Apps, create a separate App Service app for this purpose.</span></span>  <span data-ttu-id="ed69f-149">Estas características dependen de un marco de la aplicación específico para habilitarlas.</span><span class="sxs-lookup"><span data-stu-id="ed69f-149">These features rely on a specific application framework to enable them.</span></span>

### <a name="webjobs"></a><span data-ttu-id="ed69f-150">Trabajos web</span><span class="sxs-lookup"><span data-stu-id="ed69f-150">WebJobs</span></span>
<span data-ttu-id="ed69f-151">Considere la posibilidad de implementar trabajos web que consumen muchos recursos en una aplicación de App Service vacía dentro de un plan de App Service independiente.</span><span class="sxs-lookup"><span data-stu-id="ed69f-151">Consider deploying resource intensive WebJobs to an empty App Service app within a separate App Service plan.</span></span> <span data-ttu-id="ed69f-152">De esta manera, se dispone de instancias dedicados para el trabajo web.</span><span class="sxs-lookup"><span data-stu-id="ed69f-152">This provides dedicated instances for the WebJob.</span></span> <span data-ttu-id="ed69f-153">Consulte la [guía sobre los trabajos de segundo plano][webjobs-guidance].</span><span class="sxs-lookup"><span data-stu-id="ed69f-153">See [Background jobs guidance][webjobs-guidance].</span></span>  

### <a name="cache"></a><span data-ttu-id="ed69f-154">Memoria caché</span><span class="sxs-lookup"><span data-stu-id="ed69f-154">Cache</span></span>
<span data-ttu-id="ed69f-155">Puede mejorar el rendimiento y la escalabilidad mediante [Azure Redis Cache][azure-redis] para almacenar en caché algunos datos.</span><span class="sxs-lookup"><span data-stu-id="ed69f-155">You can improve performance and scalability by using [Azure Redis Cache][azure-redis] to cache some data.</span></span> <span data-ttu-id="ed69f-156">Considere el uso de Redis Cache para:</span><span class="sxs-lookup"><span data-stu-id="ed69f-156">Consider using Redis Cache for:</span></span>

* <span data-ttu-id="ed69f-157">Datos de transacción parcialmente estáticos</span><span class="sxs-lookup"><span data-stu-id="ed69f-157">Semi-static transaction data.</span></span>
* <span data-ttu-id="ed69f-158">Estado de sesión</span><span class="sxs-lookup"><span data-stu-id="ed69f-158">Session state.</span></span>
* <span data-ttu-id="ed69f-159">Salida HTML</span><span class="sxs-lookup"><span data-stu-id="ed69f-159">HTML output.</span></span> <span data-ttu-id="ed69f-160">Esto puede ser útil en aplicaciones que representan la salida HTML compleja.</span><span class="sxs-lookup"><span data-stu-id="ed69f-160">This can be useful in applications that render complex HTML output.</span></span>

<span data-ttu-id="ed69f-161">Para instrucciones detalladas sobre cómo diseñar una estrategia de almacenamiento en caché, consulte la [guía de almacenamiento en caché][caching-guidance].</span><span class="sxs-lookup"><span data-stu-id="ed69f-161">For more detailed guidance on designing a caching strategy, see [Caching guidance][caching-guidance].</span></span>

### <a name="cdn"></a><span data-ttu-id="ed69f-162">CDN</span><span class="sxs-lookup"><span data-stu-id="ed69f-162">CDN</span></span>
<span data-ttu-id="ed69f-163">Use [Azure CDN][azure-cdn] para almacenar en caché el contenido estático.</span><span class="sxs-lookup"><span data-stu-id="ed69f-163">Use [Azure CDN][azure-cdn] to cache static content.</span></span> <span data-ttu-id="ed69f-164">La principal ventaja de una red CDN es reducir la latencia de los usuarios, ya que el contenido se almacena en caché en un servidor perimetral que está geográficamente próximo al usuario.</span><span class="sxs-lookup"><span data-stu-id="ed69f-164">The main benefit of a CDN is to reduce latency for users, because content is cached at an edge server that is geographically close to the user.</span></span> <span data-ttu-id="ed69f-165">CDN también puede reducir la carga sobre la aplicación, ya que el la aplicación no administra el tráfico.</span><span class="sxs-lookup"><span data-stu-id="ed69f-165">CDN can also reduce load on the application, because that traffic is not being handled by the application.</span></span>

<span data-ttu-id="ed69f-166">Si la aplicación está compuesta mayormente por páginas estáticas, considere la posibilidad de usar [CDN para almacenar en caché la aplicación entera][cdn-app-service].</span><span class="sxs-lookup"><span data-stu-id="ed69f-166">If your app consists mostly of static pages, consider using [CDN to cache the entire app][cdn-app-service].</span></span> <span data-ttu-id="ed69f-167">Si no es así, coloque el contenido estático, como imágenes, CSS y archivos HTML, en [Azure Storage y use CDN para almacenar en caché esos archivos][cdn-storage-account].</span><span class="sxs-lookup"><span data-stu-id="ed69f-167">Otherwise, put static content such as images, CSS, and HTML files, into [Azure Storage and use CDN to cache those files][cdn-storage-account].</span></span>

> [!NOTE]
> <span data-ttu-id="ed69f-168">Azure CDN no puede servir contenido que requiera autenticación.</span><span class="sxs-lookup"><span data-stu-id="ed69f-168">Azure CDN cannot serve content that requires authentication.</span></span>
> 
> 

<span data-ttu-id="ed69f-169">Para obtener instrucciones más detalladas, consulte [guía de la red de entrega de contenido (CDN)][cdn-guidance].</span><span class="sxs-lookup"><span data-stu-id="ed69f-169">For more detailed guidance, see [Content Delivery Network (CDN) guidance][cdn-guidance].</span></span>

### <a name="storage"></a><span data-ttu-id="ed69f-170">Storage</span><span class="sxs-lookup"><span data-stu-id="ed69f-170">Storage</span></span>
<span data-ttu-id="ed69f-171">Las aplicaciones modernas suelen procesan grandes cantidades de datos.</span><span class="sxs-lookup"><span data-stu-id="ed69f-171">Modern applications often process large amounts of data.</span></span> <span data-ttu-id="ed69f-172">Para escalarlos a la nube, es importante elegir el tipo de almacenamiento correcto.</span><span class="sxs-lookup"><span data-stu-id="ed69f-172">In order to scale for the cloud, it's important to choose the right storage type.</span></span> <span data-ttu-id="ed69f-173">Estas son algunas recomendaciones básicas.</span><span class="sxs-lookup"><span data-stu-id="ed69f-173">Here are some baseline recommendations.</span></span> 

| <span data-ttu-id="ed69f-174">Qué desea almacenar</span><span class="sxs-lookup"><span data-stu-id="ed69f-174">What you want to store</span></span> | <span data-ttu-id="ed69f-175">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="ed69f-175">Example</span></span> | <span data-ttu-id="ed69f-176">Almacenamiento recomendado</span><span class="sxs-lookup"><span data-stu-id="ed69f-176">Recommended storage</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed69f-177">Archivos</span><span class="sxs-lookup"><span data-stu-id="ed69f-177">Files</span></span> |<span data-ttu-id="ed69f-178">Imágenes, documentos, archivos PDF</span><span class="sxs-lookup"><span data-stu-id="ed69f-178">Images, documents, PDFs</span></span> |<span data-ttu-id="ed69f-179">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="ed69f-179">Azure Blob Storage</span></span> |
| <span data-ttu-id="ed69f-180">Pares clave-valor</span><span class="sxs-lookup"><span data-stu-id="ed69f-180">Key/Value pairs</span></span> |<span data-ttu-id="ed69f-181">Datos de perfil de usuario consultados por identificador de usuario</span><span class="sxs-lookup"><span data-stu-id="ed69f-181">User profile data looked up by user ID</span></span> |<span data-ttu-id="ed69f-182">Almacenamiento de tablas de Azure</span><span class="sxs-lookup"><span data-stu-id="ed69f-182">Azure Table storage</span></span> |
| <span data-ttu-id="ed69f-183">Mensajes cortos diseñados para desencadenar procesamiento adicional</span><span class="sxs-lookup"><span data-stu-id="ed69f-183">Short messages intended to trigger further processing</span></span> |<span data-ttu-id="ed69f-184">Solicitudes de pedido</span><span class="sxs-lookup"><span data-stu-id="ed69f-184">Order requests</span></span> |<span data-ttu-id="ed69f-185">Azure Queue Storage, cola de Service Bus o tema de Service Bus</span><span class="sxs-lookup"><span data-stu-id="ed69f-185">Azure Queue storage, Service Bus queue, or Service Bus topic</span></span> |
| <span data-ttu-id="ed69f-186">Datos no relacionales con un esquema flexible que requiere consulta básica</span><span class="sxs-lookup"><span data-stu-id="ed69f-186">Non-relational data with a flexible schema requiring basic querying</span></span> |<span data-ttu-id="ed69f-187">Catálogo de productos</span><span class="sxs-lookup"><span data-stu-id="ed69f-187">Product catalog</span></span> |<span data-ttu-id="ed69f-188">Base de datos de documentos, como Azure Cosmos DB, MongoDB o Apache CouchDB</span><span class="sxs-lookup"><span data-stu-id="ed69f-188">Document database, such as Azure Cosmos DB, MongoDB, or Apache CouchDB</span></span> |
| <span data-ttu-id="ed69f-189">Datos relacionales que requieren compatibilidad más completa con consultas, un esquemas estricto o fuerte coherencia</span><span class="sxs-lookup"><span data-stu-id="ed69f-189">Relational data requiring richer query support, strict schema, and/or strong consistency</span></span> |<span data-ttu-id="ed69f-190">Inventario de productos</span><span class="sxs-lookup"><span data-stu-id="ed69f-190">Product inventory</span></span> |<span data-ttu-id="ed69f-191">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="ed69f-191">Azure SQL Database</span></span> |

## <a name="scalability-considerations"></a><span data-ttu-id="ed69f-192">Consideraciones sobre escalabilidad</span><span class="sxs-lookup"><span data-stu-id="ed69f-192">Scalability considerations</span></span>

<span data-ttu-id="ed69f-193">Una de las ventajas principales de Azure App Service es la posibilidad de escalar la aplicación en función de la carga.</span><span class="sxs-lookup"><span data-stu-id="ed69f-193">A major benefit of Azure App Service is the ability to scale your application based on load.</span></span> <span data-ttu-id="ed69f-194">Estas son algunas consideraciones que se deben tener en cuenta al planear el escalado de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ed69f-194">Here are some considerations to keep in mind when planning to scale your application.</span></span>

### <a name="app-service-app"></a><span data-ttu-id="ed69f-195">Aplicación de App Service</span><span class="sxs-lookup"><span data-stu-id="ed69f-195">App Service app</span></span>
<span data-ttu-id="ed69f-196">Si la solución incluye varias aplicaciones de App Service, podría implementarlas en planes de App Service diferentes.</span><span class="sxs-lookup"><span data-stu-id="ed69f-196">If your solution includes several App Service apps, consider deploying them to separate App Service plans.</span></span> <span data-ttu-id="ed69f-197">Este enfoque permite escalarlas por separado porque se ejecutan en instancias independientes.</span><span class="sxs-lookup"><span data-stu-id="ed69f-197">This approach enables you to scale them independently because they run on separate instances.</span></span> 

<span data-ttu-id="ed69f-198">De igual forma, considere la posibilidad de colocar un trabajo web en su propio plan de modo que las tareas en segundo plano no se ejecuten en las mismas instancias que administran las solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="ed69f-198">Similarly, consider putting a WebJob into its own plan so that background tasks don't run on the same instances that handle HTTP requests.</span></span>  

### <a name="sql-database"></a><span data-ttu-id="ed69f-199">SQL Database</span><span class="sxs-lookup"><span data-stu-id="ed69f-199">SQL Database</span></span>
<span data-ttu-id="ed69f-200">Aumente la escalabilidad de una base de datos SQL mediante el *particionamiento* de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="ed69f-200">Increase scalability of a SQL database by *sharding* the database.</span></span> <span data-ttu-id="ed69f-201">El particionamiento hace referencia a la creación de particiones de la base de datos de manera horizontal.</span><span class="sxs-lookup"><span data-stu-id="ed69f-201">Sharding refers to partitioning the database horizontally.</span></span> <span data-ttu-id="ed69f-202">El particionamiento permite escalar la base de datos horizontalmente mediante [herramientas Elastic Database][sql-elastic].</span><span class="sxs-lookup"><span data-stu-id="ed69f-202">Sharding allows you to scale out the database horizontally using [Elastic Database tools][sql-elastic].</span></span> <span data-ttu-id="ed69f-203">Entre las posibles ventajas del particionamiento se incluyen:</span><span class="sxs-lookup"><span data-stu-id="ed69f-203">Potential benefits of sharding include:</span></span>

- <span data-ttu-id="ed69f-204">Mejor rendimiento de las transacciones.</span><span class="sxs-lookup"><span data-stu-id="ed69f-204">Better transaction throughput.</span></span>
- <span data-ttu-id="ed69f-205">Las consultas pueden ejecutarse con mayor rapidez sobre un subconjunto de los datos.</span><span class="sxs-lookup"><span data-stu-id="ed69f-205">Queries can run faster over a subset of the data.</span></span>

### <a name="azure-search"></a><span data-ttu-id="ed69f-206">Azure Search</span><span class="sxs-lookup"><span data-stu-id="ed69f-206">Azure Search</span></span>
<span data-ttu-id="ed69f-207">Azure Search quita la sobrecarga que supone realizar búsquedas de datos complejos desde el almacén de datos principal, y puede escalarse para administrar la carga.</span><span class="sxs-lookup"><span data-stu-id="ed69f-207">Azure Search removes the overhead of performing complex data searches from the primary data store, and it can scale to handle load.</span></span> <span data-ttu-id="ed69f-208">Consulte [Escalado de niveles de recursos para cargas de trabajo de indexación y consulta en Azure Search][azure-search-scaling].</span><span class="sxs-lookup"><span data-stu-id="ed69f-208">See [Scale resource levels for query and indexing workloads in Azure Search][azure-search-scaling].</span></span>

## <a name="security-considerations"></a><span data-ttu-id="ed69f-209">Consideraciones sobre la seguridad</span><span class="sxs-lookup"><span data-stu-id="ed69f-209">Security considerations</span></span>
<span data-ttu-id="ed69f-210">En esta sección se enumeran las consideraciones de seguridad que son específicas de los servicios de Azure descritos en este artículo.</span><span class="sxs-lookup"><span data-stu-id="ed69f-210">This section lists security considerations that are specific to the Azure services described in this article.</span></span> <span data-ttu-id="ed69f-211">No es una lista completa de procedimientos de seguridad recomendados.</span><span class="sxs-lookup"><span data-stu-id="ed69f-211">It's not a complete list of security best practices.</span></span> <span data-ttu-id="ed69f-212">Si desea conocer algunas otras consideraciones de seguridad, consulte [Protección de una aplicación en Azure App Service][app-service-security].</span><span class="sxs-lookup"><span data-stu-id="ed69f-212">For some additional security considerations, see [Secure an app in Azure App Service][app-service-security].</span></span>

### <a name="cross-origin-resource-sharing-cors"></a><span data-ttu-id="ed69f-213">Uso compartido de recursos entre orígenes</span><span class="sxs-lookup"><span data-stu-id="ed69f-213">Cross-Origin Resource Sharing (CORS)</span></span>
<span data-ttu-id="ed69f-214">Si crea un sitio web y una API web como aplicaciones independientes, el sitio web no podrá realizar llamadas AJAX a la API en el lado cliente a menos que habilite CORS.</span><span class="sxs-lookup"><span data-stu-id="ed69f-214">If you create a website and web API as separate apps, the website cannot make client-side AJAX calls to the API unless you enable CORS.</span></span>

> [!NOTE]
> <span data-ttu-id="ed69f-215">La seguridad del explorador impide que una página web realice solicitudes AJAX a otro dominio.</span><span class="sxs-lookup"><span data-stu-id="ed69f-215">Browser security prevents a web page from making AJAX requests to another domain.</span></span> <span data-ttu-id="ed69f-216">Esta restricción se conoce como directiva de mismo origen y evita que un sitio malintencionado lea datos confidenciales de otro sitio.</span><span class="sxs-lookup"><span data-stu-id="ed69f-216">This restriction is called the same-origin policy, and prevents a malicious site from reading sentitive data from another site.</span></span> <span data-ttu-id="ed69f-217">CORS es una norma de W3C que permite que un servidor "se relaje" con la directiva del mismo origen de forma que permite algunas solicitudes entre orígenes y rechaza otras.</span><span class="sxs-lookup"><span data-stu-id="ed69f-217">CORS is a W3C standard that allows a server to relax the same-origin policy and allow some cross-origin requests while rejecting others.</span></span>
> 
> 

<span data-ttu-id="ed69f-218">App Services tiene compatibilidad integrada con CORS, sin necesidad de escribir ningún código de aplicación.</span><span class="sxs-lookup"><span data-stu-id="ed69f-218">App Services has built-in support for CORS, without needing to write any application code.</span></span> <span data-ttu-id="ed69f-219">Consulte [Consume an API app from JavaScript using CORS][cors] (Consumo de una aplicación de API desde JavaScript con CORS).</span><span class="sxs-lookup"><span data-stu-id="ed69f-219">See [Consume an API app from JavaScript using CORS][cors].</span></span> <span data-ttu-id="ed69f-220">Agregue el sitio web a la lista de orígenes permitidos para la API.</span><span class="sxs-lookup"><span data-stu-id="ed69f-220">Add the website to the list of allowed origins for the API.</span></span>

### <a name="sql-database-encryption"></a><span data-ttu-id="ed69f-221">Cifrado de SQL Database</span><span class="sxs-lookup"><span data-stu-id="ed69f-221">SQL Database encryption</span></span>
<span data-ttu-id="ed69f-222">Use [Cifrado de datos transparente][sql-encryption] si necesita cifrar los datos en reposo en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="ed69f-222">Use [Transparent Data Encryption][sql-encryption] if you need to encrypt data at rest in the database.</span></span> <span data-ttu-id="ed69f-223">Esta característica realiza el cifrado y el descifrado en tiempo real de una base de datos completa (incluidas las copias de seguridad y los archivos de registros de transacciones) y no requiere realizar ningún cambio en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ed69f-223">This feature performs real-time encryption and decryption of an entire database (including backups and transaction log files) and requires no changes to the application.</span></span> <span data-ttu-id="ed69f-224">El cifrado agrega alguna latencia, así que es conveniente separar los datos que deben estar protegidos en su propia base de datos y habilitar el cifrado únicamente para esa base de datos.</span><span class="sxs-lookup"><span data-stu-id="ed69f-224">Encryption does add some latency, so it's a good practice to separate the data that must be secure into its own database and enable encryption only for that database.</span></span>  
  

<!-- links -->

[api-guidance]: ../../best-practices/api-design.md
[app-service-security]: /azure/app-service-web/web-sites-security
[app-service-web-app]: /azure/app-service-web/app-service-web-overview
[app-service-api-app]: /azure/app-service-api/app-service-api-apps-why-best-platform
[app-service-pricing]: https://azure.microsoft.com/pricing/details/app-service/
[azure-cdn]: https://azure.microsoft.com/services/cdn/
[azure-redis]: https://azure.microsoft.com/services/cache/
[azure-search]: https://azure.microsoft.com/documentation/services/search/
[azure-search-scaling]: /azure/search/search-capacity-planning
[background-jobs]: ../../best-practices/background-jobs.md
[basic-web-app]: basic-web-app.md
[basic-web-app-scalability]: basic-web-app.md#scalability-considerations
[caching-guidance]: ../../best-practices/caching.md
[cdn-app-service]: /azure/app-service-web/cdn-websites-with-cdn
[cdn-storage-account]: /azure/cdn/cdn-create-a-storage-account-with-cdn
[cdn-guidance]: ../../best-practices/cdn.md
[cors]: /azure/app-service-api/app-service-api-cors-consume-javascript
[documentdb]: https://azure.microsoft.com/documentation/services/documentdb/
[queue-storage]: /azure/storage/storage-dotnet-how-to-use-queues
[queues-compared]: /azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted
[resource-group]: /azure/azure-resource-manager/resource-group-overview#resource-groups
[sql-db]: https://azure.microsoft.com/documentation/services/sql-database/
[sql-elastic]: /azure/sql-database/sql-database-elastic-scale-introduction
[sql-encryption]: https://msdn.microsoft.com/library/dn948096.aspx
[tm]: https://azure.microsoft.com/services/traffic-manager/
[visio-download]: https://archcenter.azureedge.net/cdn/app-service-reference-architectures.vsdx
[web-app-multi-region]: ./multi-region.md
[webjobs-guidance]: ../../best-practices/background-jobs.md
[webjobs]: /azure/app-service/app-service-webjobs-readme
[0]: ./images/scalable-web-app.png "Aplicación web en Azure con escalabilidad mejorada"