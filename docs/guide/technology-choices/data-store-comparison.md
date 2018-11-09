---
title: Criterios para elegir un almacén de datos
description: Información general sobre las opciones de Azure Compute
author: MikeWasson
ms.date: 06/01/2018
ms.openlocfilehash: f8996cdeb937a28b3f3056da3921a3f89dd36b1a
ms.sourcegitcommit: dbbf914757b03cdee7a274204f9579fa63d7eed2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/02/2018
ms.locfileid: "50916437"
---
# <a name="criteria-for-choosing-a-data-store"></a><span data-ttu-id="54a81-103">Criterios para elegir un almacén de datos</span><span class="sxs-lookup"><span data-stu-id="54a81-103">Criteria for choosing a data store</span></span>

<span data-ttu-id="54a81-104">Azure admite muchos tipos de soluciones de almacenamiento de datos, cada una con funcionalidades y características diferentes.</span><span class="sxs-lookup"><span data-stu-id="54a81-104">Azure supports many types of data storage solutions, each providing different features and capabilities.</span></span> <span data-ttu-id="54a81-105">En este artículo se describen los criterios de comparación que se deben utilizar al evaluar un almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="54a81-105">This article describes the comparison criteria you should use when evaluating a data store.</span></span> <span data-ttu-id="54a81-106">El objetivo es ayudarle a determinar qué tipos de almacenamientos de datos pueden cumplir los requisitos de la solución.</span><span class="sxs-lookup"><span data-stu-id="54a81-106">The goal is to help you determine which data storage types can meet your solution's requirements.</span></span>

## <a name="general-considerations"></a><span data-ttu-id="54a81-107">Consideraciones generales</span><span class="sxs-lookup"><span data-stu-id="54a81-107">General Considerations</span></span>

<span data-ttu-id="54a81-108">Para iniciar la comparación, recopile la máxima información posible de lo que se indica a continuación sobre las necesidades de datos.</span><span class="sxs-lookup"><span data-stu-id="54a81-108">To start your comparison, gather as much of the following information as you can about your data needs.</span></span> <span data-ttu-id="54a81-109">Esta información le ayudará a determinar qué tipos de almacenamientos de datos se adaptará mejor a sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="54a81-109">This information will help you to determine which data storage types will meet your needs.</span></span>

### <a name="functional-requirements"></a><span data-ttu-id="54a81-110">Requisitos funcionales</span><span class="sxs-lookup"><span data-stu-id="54a81-110">Functional requirements</span></span>

- <span data-ttu-id="54a81-111">**Formato de datos**.</span><span class="sxs-lookup"><span data-stu-id="54a81-111">**Data format**.</span></span> <span data-ttu-id="54a81-112">¿Qué tipo de datos pretende almacenar?</span><span class="sxs-lookup"><span data-stu-id="54a81-112">What type of data are you intending to store?</span></span> <span data-ttu-id="54a81-113">Los tipos comunes son los datos transaccionales, objetos JSON, telemetría, índices de búsqueda o archivos sin formato.</span><span class="sxs-lookup"><span data-stu-id="54a81-113">Common types include transactional data, JSON objects, telemetry, search indexes, or flat files.</span></span>
- <span data-ttu-id="54a81-114">**Tamaño de los datos**.</span><span class="sxs-lookup"><span data-stu-id="54a81-114">**Data size**.</span></span> <span data-ttu-id="54a81-115">¿De qué tamaño son las entidades que necesita almacenar?</span><span class="sxs-lookup"><span data-stu-id="54a81-115">How large are the entities you need to store?</span></span> <span data-ttu-id="54a81-116">¿Estas entidades deben conservarse como un único documento o se pueden dividir entre varios documentos, tablas, colecciones, etc.?</span><span class="sxs-lookup"><span data-stu-id="54a81-116">Will these entities need to be maintained as a single document, or can they be split across multiple documents, tables, collections, and so forth?</span></span>
- <span data-ttu-id="54a81-117">**Escala y estructura**.</span><span class="sxs-lookup"><span data-stu-id="54a81-117">**Scale and structure**.</span></span> <span data-ttu-id="54a81-118">¿Qué cantidad total de capacidad de almacenamiento necesita?</span><span class="sxs-lookup"><span data-stu-id="54a81-118">What is the overall amount of storage capacity you need?</span></span> <span data-ttu-id="54a81-119">¿Prevé realizar particiones de los datos?</span><span class="sxs-lookup"><span data-stu-id="54a81-119">Do you anticipate partitioning your data?</span></span> 
- <span data-ttu-id="54a81-120">**Relaciones de los datos**.</span><span class="sxs-lookup"><span data-stu-id="54a81-120">**Data relationships**.</span></span> <span data-ttu-id="54a81-121">¿Los datos deben admitir relaciones de uno a varios o de muchos a muchos?</span><span class="sxs-lookup"><span data-stu-id="54a81-121">Will your data need to support one-to-many or many-to-many relationships?</span></span> <span data-ttu-id="54a81-122">¿Son las relaciones en sí una parte importante de los datos?</span><span class="sxs-lookup"><span data-stu-id="54a81-122">Are relationships themselves an important part of the data?</span></span> <span data-ttu-id="54a81-123">¿Necesita unir o combinar datos de otra forma desde dentro del mismo conjunto de datos o desde conjuntos de datos externos?</span><span class="sxs-lookup"><span data-stu-id="54a81-123">Will you need to join or otherwise combine data from within the same dataset, or from external datasets?</span></span> 
- <span data-ttu-id="54a81-124">**Modelo de coherencia**.</span><span class="sxs-lookup"><span data-stu-id="54a81-124">**Consistency model**.</span></span> <span data-ttu-id="54a81-125">¿Qué importancia tiene para que las actualizaciones realizada en un nodo aparezcan en otros nodos, antes de que se puedan realizar más cambios?</span><span class="sxs-lookup"><span data-stu-id="54a81-125">How important is it for updates made in one node to appear in other nodes, before further changes can be made?</span></span> <span data-ttu-id="54a81-126">¿Puede aceptar una coherencia definitiva?</span><span class="sxs-lookup"><span data-stu-id="54a81-126">Can you accept eventual consistency?</span></span> <span data-ttu-id="54a81-127">¿Necesita garantías ACID para las transacciones?</span><span class="sxs-lookup"><span data-stu-id="54a81-127">Do you need ACID guarantees for transactions?</span></span>
- <span data-ttu-id="54a81-128">**Flexibilidad de los esquemas**.</span><span class="sxs-lookup"><span data-stu-id="54a81-128">**Schema flexibility**.</span></span> <span data-ttu-id="54a81-129">¿Qué tipo de esquemas se aplicará a los datos?</span><span class="sxs-lookup"><span data-stu-id="54a81-129">What kind of schemas will you apply to your data?</span></span> <span data-ttu-id="54a81-130">¿Usará un esquema fijo, un enfoque de esquema basado en escritura o un enfoque de esquema basado en lectura?</span><span class="sxs-lookup"><span data-stu-id="54a81-130">Will you use a fixed schema, a schema-on-write approach, or a schema-on-read approach?</span></span>
- <span data-ttu-id="54a81-131">**Simultaneidad**.</span><span class="sxs-lookup"><span data-stu-id="54a81-131">**Concurrency**.</span></span> <span data-ttu-id="54a81-132">¿Qué tipo de mecanismo de simultaneidad desea usar al actualizar y sincronizar los datos?</span><span class="sxs-lookup"><span data-stu-id="54a81-132">What kind of concurrency mechanism do you want to use when updating and synchronizing data?</span></span> <span data-ttu-id="54a81-133">¿La aplicación realizará varias actualizaciones que puedan entrar en conflicto?</span><span class="sxs-lookup"><span data-stu-id="54a81-133">Will the application perform many updates that could potentially conflict.</span></span> <span data-ttu-id="54a81-134">Si es así, puede requerir el bloqueo de registros y el control de simultaneidad pesimista.</span><span class="sxs-lookup"><span data-stu-id="54a81-134">If so, you may require record locking and pessimistic concurrency control.</span></span> <span data-ttu-id="54a81-135">Como alternativa, ¿puede admitir controles de simultaneidad pesimista?</span><span class="sxs-lookup"><span data-stu-id="54a81-135">Alternatively, can you support optimistic concurrency controls?</span></span> <span data-ttu-id="54a81-136">En su caso, ¿basta con un control de simultaneidad sencillo basado en marcas de tiempo o necesita la funcionalidad agregada del control de simultaneidad de varias versiones?</span><span class="sxs-lookup"><span data-stu-id="54a81-136">If so, is simple timestamp-based concurrency control enough, or do you need the added functionality of multi-version concurrency control?</span></span>
- <span data-ttu-id="54a81-137">**Movimiento de datos**.</span><span class="sxs-lookup"><span data-stu-id="54a81-137">**Data movement**.</span></span> <span data-ttu-id="54a81-138">¿La solución deberá realizar las tareas ETL para mover datos a otros almacenes o almacenamientos de datos?</span><span class="sxs-lookup"><span data-stu-id="54a81-138">Will your solution need to perform ETL tasks to move data to other stores or data warehouses?</span></span>
- <span data-ttu-id="54a81-139">**Ciclo de vida de los datos**.</span><span class="sxs-lookup"><span data-stu-id="54a81-139">**Data lifecycle**.</span></span> <span data-ttu-id="54a81-140">¿Los datos son de solo una escritura o de varias lecturas?</span><span class="sxs-lookup"><span data-stu-id="54a81-140">Is the data write-once, read-many?</span></span> <span data-ttu-id="54a81-141">¿Pueden moverse a un almacenamiento de acceso esporádico o en frío?</span><span class="sxs-lookup"><span data-stu-id="54a81-141">Can it be moved into cool or cold storage?</span></span>
- <span data-ttu-id="54a81-142">**Otras características compatibles**.</span><span class="sxs-lookup"><span data-stu-id="54a81-142">**Other supported features**.</span></span> <span data-ttu-id="54a81-143">¿Necesita otras características específicas, como la validación del esquema, agregaciones, indexación, búsqueda de texto completo, MapReduce u otras funcionalidades de consulta?</span><span class="sxs-lookup"><span data-stu-id="54a81-143">Do you need any other specific features, such as schema validation, aggregation, indexing, full-text search, MapReduce, or other query capabilities?</span></span>

### <a name="non-functional-requirements"></a><span data-ttu-id="54a81-144">Requisitos no funcionales</span><span class="sxs-lookup"><span data-stu-id="54a81-144">Non-functional requirements</span></span>

- <span data-ttu-id="54a81-145">**Rendimiento y escalabilidad**.</span><span class="sxs-lookup"><span data-stu-id="54a81-145">**Performance and scalability**.</span></span> <span data-ttu-id="54a81-146">¿Cuáles son los requisitos de rendimiento de datos?</span><span class="sxs-lookup"><span data-stu-id="54a81-146">What are your data performance requirements?</span></span> <span data-ttu-id="54a81-147">¿Tiene requisitos específicos para la velocidad de ingesta de datos y la velocidad de procesamiento de datos?</span><span class="sxs-lookup"><span data-stu-id="54a81-147">Do you have specific requirements for data ingestion rates and data processing rates?</span></span> <span data-ttu-id="54a81-148">¿Cuáles son los tiempos de respuesta aceptables para realizar consultas y agregaciones de datos una vez ingeridos?</span><span class="sxs-lookup"><span data-stu-id="54a81-148">What are the acceptable response times for querying and aggregation of data once ingested?</span></span> <span data-ttu-id="54a81-149">¿Cuánto necesitará escalar verticalmente el tamaño del almacén de datos?</span><span class="sxs-lookup"><span data-stu-id="54a81-149">How large will you need the data store to scale up?</span></span> <span data-ttu-id="54a81-150">¿La carta de trabajo es más de lectura intensiva o de escritura intensiva?</span><span class="sxs-lookup"><span data-stu-id="54a81-150">Is your workload more read-heavy or write-heavy?</span></span>
- <span data-ttu-id="54a81-151">**Confiabilidad**.</span><span class="sxs-lookup"><span data-stu-id="54a81-151">**Reliability**.</span></span> <span data-ttu-id="54a81-152">¿Qué SLA general necesita admitir?</span><span class="sxs-lookup"><span data-stu-id="54a81-152">What overall SLA do you need to support?</span></span> <span data-ttu-id="54a81-153">¿Qué nivel de tolerancia a errores es necesario proporcionar para los consumidores de datos?</span><span class="sxs-lookup"><span data-stu-id="54a81-153">What level of fault-tolerance do you need to provide for data consumers?</span></span> <span data-ttu-id="54a81-154">¿Qué tipo de funcionalidades de copia de seguridad y restauración necesita?</span><span class="sxs-lookup"><span data-stu-id="54a81-154">What kind of backup and restore capabilities do you need?</span></span> 
- <span data-ttu-id="54a81-155">**Replicación**.</span><span class="sxs-lookup"><span data-stu-id="54a81-155">**Replication**.</span></span> <span data-ttu-id="54a81-156">¿Necesitará que los datos se distribuyan entre varias réplicas o regiones?</span><span class="sxs-lookup"><span data-stu-id="54a81-156">Will your data need to be distributed among multiple replicas or regions?</span></span> <span data-ttu-id="54a81-157">¿Qué tipo de funcionalidad de replicación de datos necesita?</span><span class="sxs-lookup"><span data-stu-id="54a81-157">What kind of data replication capabilities do you require?</span></span> 
- <span data-ttu-id="54a81-158">**Límites**.</span><span class="sxs-lookup"><span data-stu-id="54a81-158">**Limits**.</span></span> <span data-ttu-id="54a81-159">¿Los límites de un almacén de datos particular admiten los requisitos de escalado, el número de conexiones y el rendimiento?</span><span class="sxs-lookup"><span data-stu-id="54a81-159">Will the limits of a particular data store support your requirements for scale, number of connections, and throughput?</span></span> 

### <a name="management-and-cost"></a><span data-ttu-id="54a81-160">Administración y costo</span><span class="sxs-lookup"><span data-stu-id="54a81-160">Management and cost</span></span>

- <span data-ttu-id="54a81-161">**Servicio administrado**.</span><span class="sxs-lookup"><span data-stu-id="54a81-161">**Managed service**.</span></span> <span data-ttu-id="54a81-162">Cuando sea posible, utilice un servicio de datos administrado, a menos que necesite funcionalidades específicas que solo se puedan encontrar en un almacén de datos hospedado en IaaS.</span><span class="sxs-lookup"><span data-stu-id="54a81-162">When possible, use a managed data service, unless you require specific capabilities that can only be found in an IaaS-hosted data store.</span></span>
- <span data-ttu-id="54a81-163">**Disponibilidad en regiones**.</span><span class="sxs-lookup"><span data-stu-id="54a81-163">**Region availability**.</span></span> <span data-ttu-id="54a81-164">Si se trata de servicios administrados, ¿el servicio se encuentra disponible en todas las regiones de Azure?</span><span class="sxs-lookup"><span data-stu-id="54a81-164">For managed services, is the service available in all Azure regions?</span></span> <span data-ttu-id="54a81-165">¿La solución debe hospedarse en determinadas regiones de Azure?</span><span class="sxs-lookup"><span data-stu-id="54a81-165">Does your solution need to be hosted in certain Azure regions?</span></span>
- <span data-ttu-id="54a81-166">**Portabilidad**.</span><span class="sxs-lookup"><span data-stu-id="54a81-166">**Portability**.</span></span> <span data-ttu-id="54a81-167">¿Los datos deben migrarse a centros de datos externos locales o a otros entornos de hospedaje en la nube?</span><span class="sxs-lookup"><span data-stu-id="54a81-167">Will your data need to migrated to on-premises, external datacenters, or other cloud hosting environments?</span></span>
- <span data-ttu-id="54a81-168">**Licencias**.</span><span class="sxs-lookup"><span data-stu-id="54a81-168">**Licensing**.</span></span> <span data-ttu-id="54a81-169">¿Tiene preferencia por un propietario frente al tipo de licencia de OSS?</span><span class="sxs-lookup"><span data-stu-id="54a81-169">Do you have a preference of a proprietary versus OSS license type?</span></span> <span data-ttu-id="54a81-170">¿Existen otras restricciones externas del tipo de licencia que puede usar?</span><span class="sxs-lookup"><span data-stu-id="54a81-170">Are there any other external restrictions on what type of license you can use?</span></span>
- <span data-ttu-id="54a81-171">**Costo total**.</span><span class="sxs-lookup"><span data-stu-id="54a81-171">**Overall cost**.</span></span> <span data-ttu-id="54a81-172">¿Cuál es el costo total de usar el servicio en la solución?</span><span class="sxs-lookup"><span data-stu-id="54a81-172">What is the overall cost of using the service within your solution?</span></span> <span data-ttu-id="54a81-173">¿Cuántas instancias necesitará ejecutar para satisfacer los requisitos de tiempo de actividad y rendimiento?</span><span class="sxs-lookup"><span data-stu-id="54a81-173">How many instances will need to run, to support your uptime and throughput requirements?</span></span> <span data-ttu-id="54a81-174">Tenga en cuenta los costos de las operaciones en este cálculo.</span><span class="sxs-lookup"><span data-stu-id="54a81-174">Consider operations costs in this calculation.</span></span> <span data-ttu-id="54a81-175">Una razón para preferir servicios administrados es el menor costo operativo.</span><span class="sxs-lookup"><span data-stu-id="54a81-175">One reason to prefer managed services is the reduced operational cost.</span></span>
- <span data-ttu-id="54a81-176">**Rentabilidad**.</span><span class="sxs-lookup"><span data-stu-id="54a81-176">**Cost effectiveness**.</span></span> <span data-ttu-id="54a81-177">¿Puede crear una partición de los datos para almacenarlos con más rentabilidad?</span><span class="sxs-lookup"><span data-stu-id="54a81-177">Can you partition your data, to store it more cost effectively?</span></span> <span data-ttu-id="54a81-178">Por ejemplo, ¿puede mover objetos grandes de una base de datos relacional cara a un almacén de objetos?</span><span class="sxs-lookup"><span data-stu-id="54a81-178">For example, can you move large objects out of an expensive relational database into an object store?</span></span>

### <a name="security"></a><span data-ttu-id="54a81-179">Seguridad</span><span class="sxs-lookup"><span data-stu-id="54a81-179">Security</span></span>

- <span data-ttu-id="54a81-180">**Seguridad**.</span><span class="sxs-lookup"><span data-stu-id="54a81-180">**Security**.</span></span> <span data-ttu-id="54a81-181">¿Qué tipo de cifrado necesita?</span><span class="sxs-lookup"><span data-stu-id="54a81-181">What type of encryption do you require?</span></span> <span data-ttu-id="54a81-182">¿Necesita cifrado en reposo?</span><span class="sxs-lookup"><span data-stu-id="54a81-182">Do you need encryption at rest?</span></span> <span data-ttu-id="54a81-183">¿Qué mecanismo de autenticación desea usar para conectarse a los datos?</span><span class="sxs-lookup"><span data-stu-id="54a81-183">What authentication mechanism do you want to use to connect to your data?</span></span>
- <span data-ttu-id="54a81-184">**Auditoría**.</span><span class="sxs-lookup"><span data-stu-id="54a81-184">**Auditing**.</span></span> <span data-ttu-id="54a81-185">¿Qué tipo de registro de auditoría necesita generar?</span><span class="sxs-lookup"><span data-stu-id="54a81-185">What kind of audit log do you need to generate?</span></span>
- <span data-ttu-id="54a81-186">**Requisitos de red**.</span><span class="sxs-lookup"><span data-stu-id="54a81-186">**Networking requirements**.</span></span> <span data-ttu-id="54a81-187">¿Necesita restringir o administrar el acceso a los datos desde otros recursos de red?</span><span class="sxs-lookup"><span data-stu-id="54a81-187">Do you need to restrict or otherwise manage access to your data from other network resources?</span></span> <span data-ttu-id="54a81-188">¿Necesita que los datos solo sean accesibles desde dentro del entorno de Azure?</span><span class="sxs-lookup"><span data-stu-id="54a81-188">Does data need to be accessible only from inside the Azure environment?</span></span> <span data-ttu-id="54a81-189">¿Los datos deben ser accesibles desde subredes o direcciones IP específicas?</span><span class="sxs-lookup"><span data-stu-id="54a81-189">Does the data need to be accessible from specific IP addresses or subnets?</span></span> <span data-ttu-id="54a81-190">¿Deben ser accesibles desde aplicaciones o servicios hospedados en centros de datos locales o en otros centros de datos externos?</span><span class="sxs-lookup"><span data-stu-id="54a81-190">Does it need to be accessible from applications or services hosted on-premises or in other external datacenters?</span></span>

### <a name="devops"></a><span data-ttu-id="54a81-191">DevOps</span><span class="sxs-lookup"><span data-stu-id="54a81-191">DevOps</span></span>

- <span data-ttu-id="54a81-192">**Serie de aptitudes**.</span><span class="sxs-lookup"><span data-stu-id="54a81-192">**Skill set**.</span></span> <span data-ttu-id="54a81-193">¿Existen lenguajes de programación concretos, sistemas operativos u otra tecnología que el equipo esté especialmente acostumbrado a usar?</span><span class="sxs-lookup"><span data-stu-id="54a81-193">Are there particular programming languages, operating systems, or other technology that your team is particularly adept at using?</span></span> <span data-ttu-id="54a81-194">¿Hay otros con los que a su equipo le resultaría difícil trabajar?</span><span class="sxs-lookup"><span data-stu-id="54a81-194">Are there others that would be difficult for your team to work with?</span></span>
- <span data-ttu-id="54a81-195">**Clientes** ¿Existe una buena compatibilidad del cliente con los lenguajes de desarrollo?</span><span class="sxs-lookup"><span data-stu-id="54a81-195">**Clients** Is there good client support for your development languages?</span></span>

<span data-ttu-id="54a81-196">En las siguientes secciones se comparan varios modelos de almacén de datos según el perfil de carga de trabajo, los tipos de datos y los casos de uso de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="54a81-196">The following sections compare various data store models in terms of workload profile, data types, and example use cases.</span></span>

## <a name="relational-database-management-systems-rdbms"></a><span data-ttu-id="54a81-197">Sistemas de administración de bases de datos relacionales (RDBMS)</span><span class="sxs-lookup"><span data-stu-id="54a81-197">Relational database management systems (RDBMS)</span></span>

<table>
<tr><td><span data-ttu-id="54a81-198"><strong>Carga de trabajo</strong></span><span class="sxs-lookup"><span data-stu-id="54a81-198"><strong>Workload</strong></span></span></td>
    <td>
        <ul>
            <li><span data-ttu-id="54a81-199">La creación de registros nuevos y las actualizaciones de los datos existentes se producen con regularidad.</span><span class="sxs-lookup"><span data-stu-id="54a81-199">Both the creation of new records and updates to existing data happen regularly.</span></span></li>
            <li><span data-ttu-id="54a81-200">Se deben realizar varias operaciones en una sola transacción.</span><span class="sxs-lookup"><span data-stu-id="54a81-200">Multiple operations have to be completed in a single transaction.</span></span></li>
            <li><span data-ttu-id="54a81-201">Requiere que las funciones de agregación realicen la tabulación cruzada.</span><span class="sxs-lookup"><span data-stu-id="54a81-201">Requires aggregation functions to perform cross-tabulation.</span></span></li>
            <li><span data-ttu-id="54a81-202">Se necesita una fuerte integración con herramientas de informes.</span><span class="sxs-lookup"><span data-stu-id="54a81-202">Strong integration with reporting tools is required.</span></span></li>
            <li><span data-ttu-id="54a81-203">Las relaciones se aplican mediante restricciones de base de datos.</span><span class="sxs-lookup"><span data-stu-id="54a81-203">Relationships are enforced using database constraints.</span></span></li>
            <li><span data-ttu-id="54a81-204">Se usan índices para optimizar el rendimiento de las consultas.</span><span class="sxs-lookup"><span data-stu-id="54a81-204">Indexes are used to optimize query performance.</span></span></li>
            <li><span data-ttu-id="54a81-205">Permite el acceso a subconjuntos específicos de datos.</span><span class="sxs-lookup"><span data-stu-id="54a81-205">Allows access to specific subsets of data.</span></span></li>
        </ul>
    </td>
</tr>
<tr><td><span data-ttu-id="54a81-206"><strong>Tipo de datos</strong></span><span class="sxs-lookup"><span data-stu-id="54a81-206"><strong>Data type</strong></span></span></td>
    <td>
        <ul>
            <li><span data-ttu-id="54a81-207">Los datos están muy normalizados.</span><span class="sxs-lookup"><span data-stu-id="54a81-207">Data is highly normalized.</span></span></li>
            <li><span data-ttu-id="54a81-208">Los esquemas de base de datos son necesarios y se aplican.</span><span class="sxs-lookup"><span data-stu-id="54a81-208">Database schemas are required and enforced.</span></span></li>
            <li><span data-ttu-id="54a81-209">Relaciones de muchos a muchos entre entidades de datos de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="54a81-209">Many-to-many relationships between data entities in the database.</span></span></li>
            <li><span data-ttu-id="54a81-210">Las restricciones se definen en el esquema y se imponen en todos los datos de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="54a81-210">Constraints are defined in the schema and imposed on any data in the database.</span></span></li>
            <li><span data-ttu-id="54a81-211">Los datos necesitan una integridad elevada.</span><span class="sxs-lookup"><span data-stu-id="54a81-211">Data requires high integrity.</span></span> <span data-ttu-id="54a81-212">Los índices y las relaciones deben mantenerse con precisión.</span><span class="sxs-lookup"><span data-stu-id="54a81-212">Indexes and relationships need to be maintained accurately.</span></span></li>
            <li><span data-ttu-id="54a81-213">Los datos requieren una sólida coherencia.</span><span class="sxs-lookup"><span data-stu-id="54a81-213">Data requires strong consistency.</span></span> <span data-ttu-id="54a81-214">Las transacciones funcionan de forma que garantizan que todos los datos sean totalmente coherentes para todos los usuarios y procesos.</span><span class="sxs-lookup"><span data-stu-id="54a81-214">Transactions operate in a way that ensures all data are 100% consistent for all users and processes.</span></span></li>
            <li><span data-ttu-id="54a81-215">El tamaño de las entradas de datos individuales suele ser de pequeño a mediano.</span><span class="sxs-lookup"><span data-stu-id="54a81-215">Size of individual data entries is intended to be small to medium-sized.</span></span></li>
        </ul>
    </td>
</tr>
<tr><td><span data-ttu-id="54a81-216"><strong>Ejemplos</strong></span><span class="sxs-lookup"><span data-stu-id="54a81-216"><strong>Examples</strong></span></span></td>
    <td>
        <ul>
            <li><span data-ttu-id="54a81-217">Línea de negocio (administración del capital humano, administración de relaciones con clientes y planeamiento de recursos empresariales)</span><span class="sxs-lookup"><span data-stu-id="54a81-217">Line of business  (human capital management, customer relationship management, enterprise resource planning)</span></span></li>
            <li><span data-ttu-id="54a81-218">Administración de inventario</span><span class="sxs-lookup"><span data-stu-id="54a81-218">Inventory management</span></span></li>
            <li><span data-ttu-id="54a81-219">Informes de base de datos</span><span class="sxs-lookup"><span data-stu-id="54a81-219">Reporting database</span></span></li>
            <li><span data-ttu-id="54a81-220">Control</span><span class="sxs-lookup"><span data-stu-id="54a81-220">Accounting</span></span></li>
            <li><span data-ttu-id="54a81-221">Administración de recursos</span><span class="sxs-lookup"><span data-stu-id="54a81-221">Asset management</span></span></li>
            <li><span data-ttu-id="54a81-222">Administración de fondos</span><span class="sxs-lookup"><span data-stu-id="54a81-222">Fund management</span></span></li>
            <li><span data-ttu-id="54a81-223">Administración de pedidos</span><span class="sxs-lookup"><span data-stu-id="54a81-223">Order management</span></span></li>
        </ul>
    </td>
</tr>
</table>

## <a name="document-databases"></a><span data-ttu-id="54a81-224">Bases de datos de documentos</span><span class="sxs-lookup"><span data-stu-id="54a81-224">Document databases</span></span>

<table>
<tr><td><span data-ttu-id="54a81-225"><strong>Carga de trabajo</strong></span><span class="sxs-lookup"><span data-stu-id="54a81-225"><strong>Workload</strong></span></span></td>
    <td>
        <ul>
            <li><span data-ttu-id="54a81-226">Uso general.</span><span class="sxs-lookup"><span data-stu-id="54a81-226">General purpose.</span></span></li>
            <li><span data-ttu-id="54a81-227">Las operaciones de inserción y actualización son comunes.</span><span class="sxs-lookup"><span data-stu-id="54a81-227">Insert and update operations are common.</span></span> <span data-ttu-id="54a81-228">La creación de registros nuevos y las actualizaciones de los datos existentes se producen con regularidad.</span><span class="sxs-lookup"><span data-stu-id="54a81-228">Both the creation of new records and updates to existing data happen regularly.</span></span></li>
            <li><span data-ttu-id="54a81-229">No hay ningún error de coincidencia de impedancia relacional de objetos.</span><span class="sxs-lookup"><span data-stu-id="54a81-229">No object-relational impedance mismatch.</span></span> <span data-ttu-id="54a81-230">Los documentos pueden coincidir mejor con las estructuras de objetos usadas en el código de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="54a81-230">Documents can better match the object structures used in application code.</span></span></li>
            <li><span data-ttu-id="54a81-231">La simultaneidad optimista se usa con más frecuencia.</span><span class="sxs-lookup"><span data-stu-id="54a81-231">Optimistic concurrency is more commonly used.</span></span></li>
            <li><span data-ttu-id="54a81-232">La aplicación consumidora debe modificar y procesar los datos.</span><span class="sxs-lookup"><span data-stu-id="54a81-232">Data must be modified and processed by consuming application.</span></span></li>
            <li><span data-ttu-id="54a81-233">Los datos necesitan un índice en varios campos.</span><span class="sxs-lookup"><span data-stu-id="54a81-233">Data requires index on multiple fields.</span></span></li>
            <li><span data-ttu-id="54a81-234">Los documentos individuales se recuperan y escriben como un solo bloque.</span><span class="sxs-lookup"><span data-stu-id="54a81-234">Individual documents are retrieved and written as a single block.</span></span></li>
    </td>
</tr>
<tr><td><span data-ttu-id="54a81-235"><strong>Tipo de datos</strong></span><span class="sxs-lookup"><span data-stu-id="54a81-235"><strong>Data type</strong></span></span></td>
    <td>
        <ul>
            <li><span data-ttu-id="54a81-236">Los datos pueden administrarse de manera no normalizada.</span><span class="sxs-lookup"><span data-stu-id="54a81-236">Data can be managed in de-normalized way.</span></span></li>
            <li><span data-ttu-id="54a81-237">El tamaño de los datos de documentos individuales es relativamente pequeño.</span><span class="sxs-lookup"><span data-stu-id="54a81-237">Size of individual document data is relatively small.</span></span></li>
            <li><span data-ttu-id="54a81-238">Cada tipo de documento puede usar su propio esquema.</span><span class="sxs-lookup"><span data-stu-id="54a81-238">Each document type can use its own schema.</span></span></li>
            <li><span data-ttu-id="54a81-239">Los documentos pueden incluir campos opcionales.</span><span class="sxs-lookup"><span data-stu-id="54a81-239">Documents can include optional fields.</span></span></li>
            <li><span data-ttu-id="54a81-240">Los datos del documento son semiestructurados, lo que significa que los tipo de datos de cada campo no se definen estrictamente.</span><span class="sxs-lookup"><span data-stu-id="54a81-240">Document data is semi-structured, meaning that data types of each field are not strictly defined.</span></span></li>
            <li><span data-ttu-id="54a81-241">Se admite la agregación de datos.</span><span class="sxs-lookup"><span data-stu-id="54a81-241">Data aggregation is supported.</span></span></li>
        </ul>
    </td>
</tr>
<tr><td><span data-ttu-id="54a81-242"><strong>Ejemplos</strong></span><span class="sxs-lookup"><span data-stu-id="54a81-242"><strong>Examples</strong></span></span></td>
    <td>
        <ul>
            <li><span data-ttu-id="54a81-243">Catálogo de productos</span><span class="sxs-lookup"><span data-stu-id="54a81-243">Product catalog</span></span></li>
            <li><span data-ttu-id="54a81-244">Cuentas de usuario</span><span class="sxs-lookup"><span data-stu-id="54a81-244">User accounts</span></span></li>
            <li><span data-ttu-id="54a81-245">Lista de materiales</span><span class="sxs-lookup"><span data-stu-id="54a81-245">Bill of materials</span></span></li>
            <li><span data-ttu-id="54a81-246">Personalización</span><span class="sxs-lookup"><span data-stu-id="54a81-246">Personalization</span></span></li>
            <li><span data-ttu-id="54a81-247">Administración de contenido</span><span class="sxs-lookup"><span data-stu-id="54a81-247">Content management</span></span></li>
            <li><span data-ttu-id="54a81-248">Datos de operaciones</span><span class="sxs-lookup"><span data-stu-id="54a81-248">Operations data</span></span></li>
            <li><span data-ttu-id="54a81-249">Administración de inventario</span><span class="sxs-lookup"><span data-stu-id="54a81-249">Inventory management</span></span></li>
            <li><span data-ttu-id="54a81-250">Datos del historial de transacciones</span><span class="sxs-lookup"><span data-stu-id="54a81-250">Transaction history data</span></span></li>
            <li><span data-ttu-id="54a81-251">Vista materializada de otros almacenes NoSQL.</span><span class="sxs-lookup"><span data-stu-id="54a81-251">Materialized view of other NoSQL stores.</span></span> <span data-ttu-id="54a81-252">Reemplaza la indexación de archivos/BLOB.</span><span class="sxs-lookup"><span data-stu-id="54a81-252">Replaces file/BLOB indexing.</span></span></li>
        </ul>
    </td>
</tr>
</table>

## <a name="keyvalue-stores"></a><span data-ttu-id="54a81-253">Almacenes clave-valor</span><span class="sxs-lookup"><span data-stu-id="54a81-253">Key/value stores</span></span>

<table>
<tr><td><span data-ttu-id="54a81-254"><strong>Carga de trabajo</strong></span><span class="sxs-lookup"><span data-stu-id="54a81-254"><strong>Workload</strong></span></span></td>
    <td>
        <ul>
            <li><span data-ttu-id="54a81-255">Los datos se identifican y se accede a ellos con una clave de identificador única, como un diccionario.</span><span class="sxs-lookup"><span data-stu-id="54a81-255">Data is identified and accessed using a single ID key, like a dictionary.</span></span></li>
            <li><span data-ttu-id="54a81-256">Escalable a gran escala.</span><span class="sxs-lookup"><span data-stu-id="54a81-256">Massively scalable.</span></span></li>
            <li><span data-ttu-id="54a81-257">No se necesitan combinaciones, bloqueos ni uniones.</span><span class="sxs-lookup"><span data-stu-id="54a81-257">No joins, lock, or unions are required.</span></span></li>
            <li><span data-ttu-id="54a81-258">No se usa ningún mecanismo de agregación.</span><span class="sxs-lookup"><span data-stu-id="54a81-258">No aggregation mechanisms are used.</span></span></li>
            <li><span data-ttu-id="54a81-259">Los índices secundarios no se suelen usar.</span><span class="sxs-lookup"><span data-stu-id="54a81-259">Secondary indexes are generally not used.</span></span></li>
        </ul>
    </td>
</tr>
<tr><td><span data-ttu-id="54a81-260"><strong>Tipo de datos</strong></span><span class="sxs-lookup"><span data-stu-id="54a81-260"><strong>Data type</strong></span></span></td>
    <td>
        <ul>
            <li><span data-ttu-id="54a81-261">El tamaño de los datos tiende a ser grande.</span><span class="sxs-lookup"><span data-stu-id="54a81-261">Data size tends to be large.</span></span></li>
            <li><span data-ttu-id="54a81-262">Cada clave está asociada con un valor único, que es un BLOB de datos no administrado.</span><span class="sxs-lookup"><span data-stu-id="54a81-262">Each key is associated with a single value, which is an unmanaged data BLOB.</span></span></li>
            <li><span data-ttu-id="54a81-263">No hay ninguna aplicación del esquema.</span><span class="sxs-lookup"><span data-stu-id="54a81-263">There is no schema enforcement.</span></span></li>
            <li><span data-ttu-id="54a81-264">No existen relaciones entre entidades.</span><span class="sxs-lookup"><span data-stu-id="54a81-264">No relationships between entities.</span></span></li>
        </ul>
    </td>
</tr>
<tr><td><span data-ttu-id="54a81-265"><strong>Ejemplos</strong></span><span class="sxs-lookup"><span data-stu-id="54a81-265"><strong>Examples</strong></span></span></td>
    <td>
        <ul>
            <li><span data-ttu-id="54a81-266">Almacenamiento en caché de datos</span><span class="sxs-lookup"><span data-stu-id="54a81-266">Data caching</span></span></li>
            <li><span data-ttu-id="54a81-267">Administración de sesiones</span><span class="sxs-lookup"><span data-stu-id="54a81-267">Session management</span></span></li>
            <li><span data-ttu-id="54a81-268">Administración de perfiles y preferencias de usuario</span><span class="sxs-lookup"><span data-stu-id="54a81-268">User preference and profile management</span></span></li>
            <li><span data-ttu-id="54a81-269">Recomendación de producto y servicio</span><span class="sxs-lookup"><span data-stu-id="54a81-269">Product recommendation and ad serving</span></span></li>
            <li><span data-ttu-id="54a81-270">Diccionarios</span><span class="sxs-lookup"><span data-stu-id="54a81-270">Dictionaries</span></span></li>
        </ul>
    </td>
</tr>
</table>

## <a name="graph-databases"></a><span data-ttu-id="54a81-271">Bases de datos de gráficos</span><span class="sxs-lookup"><span data-stu-id="54a81-271">Graph databases</span></span>

<table>
<tr><td><span data-ttu-id="54a81-272"><strong>Carga de trabajo</strong></span><span class="sxs-lookup"><span data-stu-id="54a81-272"><strong>Workload</strong></span></span></td>
    <td>
        <ul>
            <li><span data-ttu-id="54a81-273">Las relaciones entre elementos de datos son muy complejas, y conllevan muchos saltos entre los elementos de datos relacionados.</span><span class="sxs-lookup"><span data-stu-id="54a81-273">The relationships between data items are very complex, involving many hops between related data items.</span></span></li>
            <li><span data-ttu-id="54a81-274">La relación entre elementos de datos es dinámica y cambia con el tiempo.</span><span class="sxs-lookup"><span data-stu-id="54a81-274">The relationship between data items are dynamic and change over time.</span></span></li>
            <li><span data-ttu-id="54a81-275">Las relaciones entre objetos son ciudadanos de primera clase, sin requerir claves externas ni combinaciones que recorrer.</span><span class="sxs-lookup"><span data-stu-id="54a81-275">Relationships between objects are first-class citizens, without requiring foreign-keys and joins to traverse.</span></span></li>
        </ul>
    </td>
</tr>
<tr><td><span data-ttu-id="54a81-276"><strong>Tipo de datos</strong></span><span class="sxs-lookup"><span data-stu-id="54a81-276"><strong>Data type</strong></span></span></td>
    <td>
        <ul>
            <li><span data-ttu-id="54a81-277">Los datos constan de nodos y relaciones.</span><span class="sxs-lookup"><span data-stu-id="54a81-277">Data is comprised of nodes and relationships.</span></span></li>
            <li><span data-ttu-id="54a81-278">Los nodos son similares a las filas de tabla o documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="54a81-278">Nodes are similar to table rows or JSON documents.</span></span></li>
            <li><span data-ttu-id="54a81-279">Las relaciones son tan importantes como los nodos y se exponen directamente en el lenguaje de consulta.</span><span class="sxs-lookup"><span data-stu-id="54a81-279">Relationships are just as important as nodes, and are exposed directly in the query language.</span></span></li>
            <li><span data-ttu-id="54a81-280">Los objetos compuestos, como una persona con varios números de teléfono, tienden a dividirse en nodos independientes más pequeños que se combinan con relaciones que se pueden recorrer</span><span class="sxs-lookup"><span data-stu-id="54a81-280">Composite objects, such as a person with multiple phone numbers, tend to be broken into separate, smaller nodes, combined with traversable relationships</span></span> </li>
        </ul>
    </td>
</tr>
<tr><td><span data-ttu-id="54a81-281"><strong>Ejemplos</strong></span><span class="sxs-lookup"><span data-stu-id="54a81-281"><strong>Examples</strong></span></span></td>
    <td>
        <ul>
            <li><span data-ttu-id="54a81-282">Organigramas</span><span class="sxs-lookup"><span data-stu-id="54a81-282">Organization charts</span></span></li>
            <li><span data-ttu-id="54a81-283">Gráficos sociales</span><span class="sxs-lookup"><span data-stu-id="54a81-283">Social graphs</span></span></li>
            <li><span data-ttu-id="54a81-284">Detección de fraudes</span><span class="sxs-lookup"><span data-stu-id="54a81-284">Fraud detection</span></span></li>
            <li><span data-ttu-id="54a81-285">Análisis</span><span class="sxs-lookup"><span data-stu-id="54a81-285">Analytics</span></span></li>
            <li><span data-ttu-id="54a81-286">Motores de recomendaciones</span><span class="sxs-lookup"><span data-stu-id="54a81-286">Recommendation engines</span></span></li>
        </ul>
    </td>
</tr>
</table>

## <a name="column-family-databases"></a><span data-ttu-id="54a81-287">Bases de datos de familia de columnas</span><span class="sxs-lookup"><span data-stu-id="54a81-287">Column-family databases</span></span>

<table>
<tr><td><span data-ttu-id="54a81-288"><strong>Carga de trabajo</strong></span><span class="sxs-lookup"><span data-stu-id="54a81-288"><strong>Workload</strong></span></span></td>
    <td>
        <ul>
            <li><span data-ttu-id="54a81-289">La mayoría de las bases de datos de familia de columnas realizan operaciones de escritura muy rápidamente.</span><span class="sxs-lookup"><span data-stu-id="54a81-289">Most column-family databases perform write operations extremely quickly.</span></span></li>
            <li><span data-ttu-id="54a81-290">Las operaciones de actualización y eliminación son poco habituales.</span><span class="sxs-lookup"><span data-stu-id="54a81-290">Update and delete operations are rare.</span></span></li>
            <li><span data-ttu-id="54a81-291">Diseñado para proporcionar acceso de baja latencia y alto rendimiento.</span><span class="sxs-lookup"><span data-stu-id="54a81-291">Designed to provide high throughput and low-latency access.</span></span></li>
            <li><span data-ttu-id="54a81-292">Admite el acceso de consulta sencillo a un conjunto determinado de campos dentro de un registro mucho más grande.</span><span class="sxs-lookup"><span data-stu-id="54a81-292">Supports easy query access to a particular set of fields within a much larger record.</span></span></li>
            <li><span data-ttu-id="54a81-293">Escalable a gran escala.</span><span class="sxs-lookup"><span data-stu-id="54a81-293">Massively scalable.</span></span></li>
        </ul>
    </td>
</tr>
<tr><td><span data-ttu-id="54a81-294"><strong>Tipo de datos</strong></span><span class="sxs-lookup"><span data-stu-id="54a81-294"><strong>Data type</strong></span></span></td>
    <td>
        <ul>
            <li><span data-ttu-id="54a81-295">Los datos se almacenan en tablas formadas por una columna de clave y una o varias familias de columnas.</span><span class="sxs-lookup"><span data-stu-id="54a81-295">Data is stored in tables consisting of a key column and one or more column families.</span></span></li>
            <li><span data-ttu-id="54a81-296">Las columnas específicas pueden variar en filas individuales.</span><span class="sxs-lookup"><span data-stu-id="54a81-296">Specific columns can vary by individual rows.</span></span></li>
            <li><span data-ttu-id="54a81-297">Se accede a las celdas individuales a través de los comandos GET y PUT.</span><span class="sxs-lookup"><span data-stu-id="54a81-297">Individual cells are accessed via get and put commands</span></span></li>
            <li><span data-ttu-id="54a81-298">Se devuelven varias filas utilizando un comando SCAN.</span><span class="sxs-lookup"><span data-stu-id="54a81-298">Multiple rows are returned using a scan command.</span></span></li>
        </ul>
    </td>
</tr>
<tr><td><span data-ttu-id="54a81-299"><strong>Ejemplos</strong></span><span class="sxs-lookup"><span data-stu-id="54a81-299"><strong>Examples</strong></span></span></td>
    <td>
        <ul>
            <li><span data-ttu-id="54a81-300">Recomendaciones</span><span class="sxs-lookup"><span data-stu-id="54a81-300">Recommendations</span></span></li>
            <li><span data-ttu-id="54a81-301">Personalización</span><span class="sxs-lookup"><span data-stu-id="54a81-301">Personalization</span></span></li>
            <li><span data-ttu-id="54a81-302">datos del sensor</span><span class="sxs-lookup"><span data-stu-id="54a81-302">Sensor data</span></span></li>
            <li><span data-ttu-id="54a81-303">Telemetría</span><span class="sxs-lookup"><span data-stu-id="54a81-303">Telemetry</span></span></li>
            <li><span data-ttu-id="54a81-304">Mensajería</span><span class="sxs-lookup"><span data-stu-id="54a81-304">Messaging</span></span></li>
            <li><span data-ttu-id="54a81-305">Análisis de redes sociales</span><span class="sxs-lookup"><span data-stu-id="54a81-305">Social media analytics</span></span></li>
            <li><span data-ttu-id="54a81-306">Análisis web</span><span class="sxs-lookup"><span data-stu-id="54a81-306">Web analytics</span></span></li>
            <li><span data-ttu-id="54a81-307">Supervisión de la actividad</span><span class="sxs-lookup"><span data-stu-id="54a81-307">Activity monitoring</span></span></li>
            <li><span data-ttu-id="54a81-308">El tiempo y otros datos de serie temporal</span><span class="sxs-lookup"><span data-stu-id="54a81-308">Weather and other time-series data</span></span></li>
        </ul>
    </td>
</tr>
</table>

## <a name="search-engine-databases"></a><span data-ttu-id="54a81-309">Bases de datos del motor de búsqueda</span><span class="sxs-lookup"><span data-stu-id="54a81-309">Search engine databases</span></span>

<table>
<tr><td><span data-ttu-id="54a81-310"><strong>Carga de trabajo</strong></span><span class="sxs-lookup"><span data-stu-id="54a81-310"><strong>Workload</strong></span></span></td>
    <td>
        <ul>
            <li><span data-ttu-id="54a81-311">Indexación de datos de varios orígenes y servicios.</span><span class="sxs-lookup"><span data-stu-id="54a81-311">Indexing data from multiple sources and services.</span></span></li>
            <li><span data-ttu-id="54a81-312">Las consultas son ad-hoc y pueden ser complejas.</span><span class="sxs-lookup"><span data-stu-id="54a81-312">Queries are ad-hoc and can be complex.</span></span></li>
            <li><span data-ttu-id="54a81-313">Se requiere agregación.</span><span class="sxs-lookup"><span data-stu-id="54a81-313">Requires aggregation.</span></span></li>
            <li><span data-ttu-id="54a81-314">Se requiere la búsqueda de texto completo.</span><span class="sxs-lookup"><span data-stu-id="54a81-314">Full text search is required.</span></span></li>
            <li><span data-ttu-id="54a81-315">Se necesita una consulta de autoservicio ad-hoc.</span><span class="sxs-lookup"><span data-stu-id="54a81-315">Ad hoc self-service query is required.</span></span></li>
            <li><span data-ttu-id="54a81-316">Se requiere un análisis de datos con el índice en todos los campos.</span><span class="sxs-lookup"><span data-stu-id="54a81-316">Data analysis with index on all fields is required.</span></span></li>
        </ul>
    </td>
</tr>
<tr><td><span data-ttu-id="54a81-317"><strong>Tipo de datos</strong></span><span class="sxs-lookup"><span data-stu-id="54a81-317"><strong>Data type</strong></span></span></td>
    <td>
        <ul>
            <li><span data-ttu-id="54a81-318">Datos semiestructurados o sin estructurar</span><span class="sxs-lookup"><span data-stu-id="54a81-318">Semi-structured or unstructured</span></span></li>
            <li><span data-ttu-id="54a81-319">Texto</span><span class="sxs-lookup"><span data-stu-id="54a81-319">Text</span></span></li>
            <li><span data-ttu-id="54a81-320">Texto con referencia a los datos estructurados</span><span class="sxs-lookup"><span data-stu-id="54a81-320">Text with reference to structured data</span></span></li>
        </ul>
    </td>
</tr>
<tr><td><span data-ttu-id="54a81-321"><strong>Ejemplos</strong></span><span class="sxs-lookup"><span data-stu-id="54a81-321"><strong>Examples</strong></span></span></td>
    <td>
        <ul>
            <li><span data-ttu-id="54a81-322">Catálogos de productos</span><span class="sxs-lookup"><span data-stu-id="54a81-322">Product catalogs</span></span></li>
            <li><span data-ttu-id="54a81-323">Búsqueda de sitio</span><span class="sxs-lookup"><span data-stu-id="54a81-323">Site search</span></span></li>
            <li><span data-ttu-id="54a81-324">Registro</span><span class="sxs-lookup"><span data-stu-id="54a81-324">Logging</span></span></li>
            <li><span data-ttu-id="54a81-325">Análisis</span><span class="sxs-lookup"><span data-stu-id="54a81-325">Analytics</span></span></li>
            <li><span data-ttu-id="54a81-326">Sitios de la compra</span><span class="sxs-lookup"><span data-stu-id="54a81-326">Shopping sites</span></span></li>
        </ul>
    </td>
</tr>
</table>

## <a name="data-warehouse"></a><span data-ttu-id="54a81-327">Almacenamiento de datos</span><span class="sxs-lookup"><span data-stu-id="54a81-327">Data warehouse</span></span>

<table>
<tr><td><span data-ttu-id="54a81-328"><strong>Carga de trabajo</strong></span><span class="sxs-lookup"><span data-stu-id="54a81-328"><strong>Workload</strong></span></span></td>
    <td>
        <ul>
            <li><span data-ttu-id="54a81-329">Análisis de datos</span><span class="sxs-lookup"><span data-stu-id="54a81-329">Data analytics</span></span></li>
            <li><span data-ttu-id="54a81-330">BI empresarial</span><span class="sxs-lookup"><span data-stu-id="54a81-330">Enterprise BI</span></span>   </li>
        </ul>
    </td>
</tr>
<tr><td><span data-ttu-id="54a81-331"><strong>Tipo de datos</strong></span><span class="sxs-lookup"><span data-stu-id="54a81-331"><strong>Data type</strong></span></span></td>
    <td>
        <ul>
            <li><span data-ttu-id="54a81-332">Datos históricos de varios orígenes.</span><span class="sxs-lookup"><span data-stu-id="54a81-332">Historical data from multiple sources.</span></span></li>
            <li><span data-ttu-id="54a81-333">Normalmente se desnormaliza en un esquema de &quot;estrella&quot; o &quot;copo de nieve&quot;, que consta de tablas de hechos y dimensiones.</span><span class="sxs-lookup"><span data-stu-id="54a81-333">Usually denormalized in a &quot;star&quot; or &quot;snowflake&quot; schema, consisting of fact and dimension tables.</span></span></li>
            <li><span data-ttu-id="54a81-334">Suele cargarse con datos nuevos de forma programada.</span><span class="sxs-lookup"><span data-stu-id="54a81-334">Usually loaded with new data on a scheduled basis.</span></span></li>
            <li><span data-ttu-id="54a81-335">Las tablas de dimensiones suelen incluir varias versiones históricas de una entidad, conocida como <em>dimensión de variación lenta</em>.</span><span class="sxs-lookup"><span data-stu-id="54a81-335">Dimension tables often include multiple historic versions of an entity, referred to as a <em>slowly changing dimension</em>.</span></span></li>
        </ul>
    </td>
</tr>
<tr><td><span data-ttu-id="54a81-336"><strong>Ejemplos</strong></span><span class="sxs-lookup"><span data-stu-id="54a81-336"><strong>Examples</strong></span></span></td>
    <td><span data-ttu-id="54a81-337">Un almacenamiento de datos empresarial que proporciona datos para modelos analíticos, informes y paneles.</span><span class="sxs-lookup"><span data-stu-id="54a81-337">An enterprise data warehouse that provides data for analytical models, reports, and dashboards.</span></span>
    </td>
</tr>
</table>


## <a name="time-series-databases"></a><span data-ttu-id="54a81-338">Bases de datos de series temporales</span><span class="sxs-lookup"><span data-stu-id="54a81-338">Time series databases</span></span>

<table>
<tr><td><span data-ttu-id="54a81-339"><strong>Carga de trabajo</strong></span><span class="sxs-lookup"><span data-stu-id="54a81-339"><strong>Workload</strong></span></span></td>
    <td>
        <ul>
            <li><span data-ttu-id="54a81-340">Una proporción de operaciones masiva (95-99 %) son las escrituras.</span><span class="sxs-lookup"><span data-stu-id="54a81-340">An overwhelming proportion of operations (95-99%) are writes.</span></span></li>
            <li><span data-ttu-id="54a81-341">Los registros suelen anexarse secuencialmente en orden cronológico.</span><span class="sxs-lookup"><span data-stu-id="54a81-341">Records are generally appended sequentially in time order.</span></span></li>
            <li><span data-ttu-id="54a81-342">Las actualizaciones son poco frecuentes.</span><span class="sxs-lookup"><span data-stu-id="54a81-342">Updates are rare.</span></span></li>
            <li><span data-ttu-id="54a81-343">Las eliminaciones se producen de forma masiva y se realizan en bloques contiguos o registros.</span><span class="sxs-lookup"><span data-stu-id="54a81-343">Deletes occur in bulk, and are made to contiguous blocks or records.</span></span></li>
            <li><span data-ttu-id="54a81-344">Las solicitudes de lectura pueden ser mayores que la memoria disponible.</span><span class="sxs-lookup"><span data-stu-id="54a81-344">Read requests can be larger than available memory.</span></span></li>
            <li><span data-ttu-id="54a81-345">Es habitual que se produzcan varias lecturas al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="54a81-345">It&#39;s common for multiple reads to occur simultaneously.</span></span></li>
            <li><span data-ttu-id="54a81-346">Los datos se leen secuencialmente en orden cronológico ascendente o descendente.</span><span class="sxs-lookup"><span data-stu-id="54a81-346">Data is read sequentially in either ascending or descending time order.</span></span></li>
        </ul>
    </td>
</tr>
<tr><td><span data-ttu-id="54a81-347"><strong>Tipo de datos</strong></span><span class="sxs-lookup"><span data-stu-id="54a81-347"><strong>Data type</strong></span></span></td>
    <td>
        <ul>
            <li><span data-ttu-id="54a81-348">Una marca de tiempo que se utiliza como la clave principal y el mecanismo de ordenación.</span><span class="sxs-lookup"><span data-stu-id="54a81-348">A time stamp that is used as the primary key and sorting mechanism.</span></span></li>
            <li><span data-ttu-id="54a81-349">Medidas de la entrada o descripciones de lo que la entrada representa.</span><span class="sxs-lookup"><span data-stu-id="54a81-349">Measurements from the entry or descriptions of what the entry represents.</span></span></li>
            <li><span data-ttu-id="54a81-350">Etiquetas que definen información adicional sobre el tipo, el origen y otra información sobre la entrada.</span><span class="sxs-lookup"><span data-stu-id="54a81-350">Tags that define additional information about the type, origin, and other information about the entry.</span></span></li>
        </ul>
    </td>
</tr>
<tr><td><span data-ttu-id="54a81-351"><strong>Ejemplos</strong></span><span class="sxs-lookup"><span data-stu-id="54a81-351"><strong>Examples</strong></span></span></td>
    <td>
        <ul>
            <li><span data-ttu-id="54a81-352">Supervisión y telemetría de eventos.</span><span class="sxs-lookup"><span data-stu-id="54a81-352">Monitoring and event telemetry.</span></span></li>
            <li><span data-ttu-id="54a81-353">Sensor u otros datos de IoT.</span><span class="sxs-lookup"><span data-stu-id="54a81-353">Sensor or other IoT data.</span></span></li>
        </ul>
    </td>
</tr>
</table>

## <a name="object-storage"></a><span data-ttu-id="54a81-354">Almacenamiento de objetos</span><span class="sxs-lookup"><span data-stu-id="54a81-354">Object storage</span></span>

<table>
<tr><td><span data-ttu-id="54a81-355"><strong>Carga de trabajo</strong></span><span class="sxs-lookup"><span data-stu-id="54a81-355"><strong>Workload</strong></span></span></td>
    <td>
        <ul>
            <li><span data-ttu-id="54a81-356">Identificado por clave.</span><span class="sxs-lookup"><span data-stu-id="54a81-356">Identified by key.</span></span></li>
            <li><span data-ttu-id="54a81-357">Los objetos pueden ser accesibles por vía pública o privada.</span><span class="sxs-lookup"><span data-stu-id="54a81-357">Objects may be publicly or privately accessible.</span></span></li>
            <li><span data-ttu-id="54a81-358">El contenido suele ser un recurso como una hoja de cálculo, una imagen o un archivo de vídeo.</span><span class="sxs-lookup"><span data-stu-id="54a81-358">Content is typically an asset such as a spreadsheet, image, or video file.</span></span></li>
            <li><span data-ttu-id="54a81-359">El contenido debe ser duradero (permanente) y externo a cualquier máquina virtual o capa de aplicación.</span><span class="sxs-lookup"><span data-stu-id="54a81-359">Content must be durable (persistent), and external to any application tier or virtual machine.</span></span></li>
        </ul>
    </td>
</tr>
<tr><td><span data-ttu-id="54a81-360"><strong>Tipo de datos</strong></span><span class="sxs-lookup"><span data-stu-id="54a81-360"><strong>Data type</strong></span></span></td>
    <td>
        <ul>
            <li><span data-ttu-id="54a81-361">El tamaño de los datos es grande.</span><span class="sxs-lookup"><span data-stu-id="54a81-361">Data size is large.</span></span></li>
            <li><span data-ttu-id="54a81-362">Datos de blob.</span><span class="sxs-lookup"><span data-stu-id="54a81-362">Blob data.</span></span></li>
            <li><span data-ttu-id="54a81-363">El valor es opaco.</span><span class="sxs-lookup"><span data-stu-id="54a81-363">Value is opaque.</span></span></li>
        </ul>
    </td>
</tr>
<tr><td><span data-ttu-id="54a81-364"><strong>Ejemplos</strong></span><span class="sxs-lookup"><span data-stu-id="54a81-364"><strong>Examples</strong></span></span></td>
    <td>
        <ul>
            <li><span data-ttu-id="54a81-365">Imágenes, vídeos, documentos de Office y archivos PDF</span><span class="sxs-lookup"><span data-stu-id="54a81-365">Images, videos, office documents, PDFs</span></span></li>
            <li><span data-ttu-id="54a81-366">CSS, scripts y CSV</span><span class="sxs-lookup"><span data-stu-id="54a81-366">CSS, Scripts, CSV</span></span></li>
            <li><span data-ttu-id="54a81-367">HTML estático, JSON</span><span class="sxs-lookup"><span data-stu-id="54a81-367">Static HTML, JSON</span></span></li>
            <li><span data-ttu-id="54a81-368">Archivos de registro y auditoría</span><span class="sxs-lookup"><span data-stu-id="54a81-368">Log and audit files</span></span></li>
            <li><span data-ttu-id="54a81-369">Copias de seguridad de bases de datos</span><span class="sxs-lookup"><span data-stu-id="54a81-369">Database backups</span></span></li>
        </ul>
    </td>
</tr>
</table>

## <a name="shared-files"></a><span data-ttu-id="54a81-370">Archivos compartidos</span><span class="sxs-lookup"><span data-stu-id="54a81-370">Shared files</span></span>

<table>
<tr><td><span data-ttu-id="54a81-371"><strong>Carga de trabajo</strong></span><span class="sxs-lookup"><span data-stu-id="54a81-371"><strong>Workload</strong></span></span></td>
    <td>
        <ul>
            <li><span data-ttu-id="54a81-372">Migración de las aplicaciones existentes que interactúan con el sistema de archivos.</span><span class="sxs-lookup"><span data-stu-id="54a81-372">Migration from existing apps that interact with the file system.</span></span></li>
            <li><span data-ttu-id="54a81-373">Requiere la interfaz SMB.</span><span class="sxs-lookup"><span data-stu-id="54a81-373">Requires SMB interface.</span></span></li>
        </ul>
    </td>
</tr>
<tr><td><span data-ttu-id="54a81-374"><strong>Tipo de datos</strong></span><span class="sxs-lookup"><span data-stu-id="54a81-374"><strong>Data type</strong></span></span></td>
    <td>
        <ul>
            <li><span data-ttu-id="54a81-375">Archivos en un conjunto jerárquico de carpetas.</span><span class="sxs-lookup"><span data-stu-id="54a81-375">Files in a hierarchical set of folders.</span></span></li>
            <li><span data-ttu-id="54a81-376">Se puede acceder con bibliotecas estándar de E/S.</span><span class="sxs-lookup"><span data-stu-id="54a81-376">Accessible with standard I/O libraries.</span></span></li>
        </ul>
    </td>
</tr>
<tr><td><span data-ttu-id="54a81-377"><strong>Ejemplos</strong></span><span class="sxs-lookup"><span data-stu-id="54a81-377"><strong>Examples</strong></span></span></td>
    <td>
        <ul>
            <li><span data-ttu-id="54a81-378">Archivos heredados</span><span class="sxs-lookup"><span data-stu-id="54a81-378">Legacy files</span></span></li>
            <li><span data-ttu-id="54a81-379">Contenido compartido accesible entre una serie de máquinas virtuales o instancias de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="54a81-379">Shared content accessible among a number of VMs or app instances</span></span></li>
        </ul>
    </td>
</tr>
</table>
