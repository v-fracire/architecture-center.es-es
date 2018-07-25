---
title: Protección de aplicaciones web de Windows para sectores regulados
description: Escenario de eficacia probada a la hora de compilar una aplicación web segura, de varios niveles, con Windows Server en Azure que use conjuntos de escalado, Application Gateway y equilibradores de carga.
author: iainfoulds
ms.date: 07/11/2018
ms.openlocfilehash: aba714fc1955341645d0faa400768bc09fb8e50b
ms.sourcegitcommit: 71cbef121c40ef36e2d6e3a088cb85c4260599b9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/14/2018
ms.locfileid: "39060996"
---
# <a name="secure-windows-web-application-for-regulated-industries"></a><span data-ttu-id="38c08-103">Protección de aplicaciones web de Windows para sectores regulados</span><span class="sxs-lookup"><span data-stu-id="38c08-103">Secure Windows web application for regulated industries</span></span>

<span data-ttu-id="38c08-104">Este escenario de ejemplo es aplicable a sectores regulados que necesitan proteger las aplicaciones de varios niveles.</span><span class="sxs-lookup"><span data-stu-id="38c08-104">This sample scenario is applicable to regulated industries that have a need to secure multi-tier applications.</span></span> <span data-ttu-id="38c08-105">En este escenario, una aplicación front-end de ASP.NET se conecta de forma segura a un clúster back-end protegido de Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="38c08-105">In this scenario, a front-end ASP.NET application securely connects to a protected back-end Microsoft SQL Server cluster.</span></span>

<span data-ttu-id="38c08-106">Entre los escenarios de aplicación se incluyen aplicaciones para quirófanos, citas de pacientes y conservación de historiales o renovación y pedido de recetas.</span><span class="sxs-lookup"><span data-stu-id="38c08-106">Example application scenarios include running operating room applications, patient appointments and records keeping, or prescription refills and ordering.</span></span> <span data-ttu-id="38c08-107">Tradicionalmente, las organizaciones usaban aplicaciones y servicios locales heredados para estos escenarios.</span><span class="sxs-lookup"><span data-stu-id="38c08-107">Traditionally, organizations had to maintain legacy on-premises applications and services for these scenarios.</span></span> <span data-ttu-id="38c08-108">Con una forma segura y escalable de implementar estas aplicaciones de Windows Server en Azure, las organizaciones pueden modernizar sus implementaciones y reducir los costos operativos locales y la sobrecarga de administración.</span><span class="sxs-lookup"><span data-stu-id="38c08-108">With a secure way and scalable way to deploy these Windows Server applications in Azure, organizations can modernize their deployments are reduce their on-premises operating costs and management overhead.</span></span>

## <a name="related-use-cases"></a><span data-ttu-id="38c08-109">Casos de uso relacionados</span><span class="sxs-lookup"><span data-stu-id="38c08-109">Related use cases</span></span>

<span data-ttu-id="38c08-110">Tenga en cuenta este escenario para los casos de uso siguientes:</span><span class="sxs-lookup"><span data-stu-id="38c08-110">Consider this scenario for the following use cases:</span></span>

* <span data-ttu-id="38c08-111">Modernización de implementaciones de aplicaciones en un entorno seguro en la nube.</span><span class="sxs-lookup"><span data-stu-id="38c08-111">Modernizing application deployments in a secure cloud environment.</span></span>
* <span data-ttu-id="38c08-112">Reducción de la administración de aplicaciones y servicios locales heredados.</span><span class="sxs-lookup"><span data-stu-id="38c08-112">Reducing legacy on-premises application and service management.</span></span>
* <span data-ttu-id="38c08-113">Mejora de la asistencia sanitaria al paciente y experimentación con nuevas plataformas de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="38c08-113">Improving patient healthcare and experience with new application platforms.</span></span>

## <a name="architecture"></a><span data-ttu-id="38c08-114">Arquitectura</span><span class="sxs-lookup"><span data-stu-id="38c08-114">Architecture</span></span>

![Introducción a la arquitectura de los componentes de Azure implicados en aplicaciones de Windows Server de varios niveles para sectores regulados][architecture]

<span data-ttu-id="38c08-116">Este escenario incluye una aplicación de varios niveles para sectores regulados que usa ASP.NET y Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="38c08-116">This scenario covers a multi-tier regulated industries application that uses ASP.NET and Microsoft SQL Server.</span></span> <span data-ttu-id="38c08-117">Los datos fluyen por el escenario de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="38c08-117">The data flows through the scenario as follows:</span></span>

1. <span data-ttu-id="38c08-118">Los usuarios acceden a la aplicación front-end de ASP.NET para sectores regulados a través de una instancia de Azure Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="38c08-118">Users access the front-end ASP.NET regulated industries application through an Azure Application Gateway.</span></span>
2. <span data-ttu-id="38c08-119">Application Gateway distribuye el tráfico a las instancias de máquinas virtuales de un conjunto de escalado de máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="38c08-119">The Application Gateway distributes traffic to VM instances within an Azure virtual machine scale set.</span></span>
3. <span data-ttu-id="38c08-120">La aplicación ASP.NET se conecta al clúster de Microsoft SQL Server en un nivel de back-end a través de un equilibrador de carga de Azure.</span><span class="sxs-lookup"><span data-stu-id="38c08-120">The ASP.NET application connects to Microsoft SQL Server cluster in a back-end tier via an Azure load balancer.</span></span> <span data-ttu-id="38c08-121">Estas instancias de back-end de SQL Server están en una red virtual de Azure independiente, protegidas mediante reglas de grupo de seguridad de red que limitan el flujo de tráfico.</span><span class="sxs-lookup"><span data-stu-id="38c08-121">These backend SQL Server instances are in a separate Azure virtual network, secured by network security group rules that limit traffic flow.</span></span>
4. <span data-ttu-id="38c08-122">El equilibrador de carga distribuye el tráfico de SQL Server en instancias de máquinas virtuales de otro conjunto de escalado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="38c08-122">The load balancer distributes SQL Server traffic to VM instances in another virtual machine scale set.</span></span>
5. <span data-ttu-id="38c08-123">Azure Blob Storage actúa como un testigo en la nube para el clúster de SQL Server en el nivel de back-end.</span><span class="sxs-lookup"><span data-stu-id="38c08-123">Azure Blob Storage acts as a Cloud Witness for the SQL Server cluster in the backend tier.</span></span>  <span data-ttu-id="38c08-124">La conexión desde dentro de la red virtual se habilita con un punto de conexión de servicio de red virtual para Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="38c08-124">The connection from within the VNet is enabled with a VNet Service Endpoint for Azure Storage.</span></span>

### <a name="components"></a><span data-ttu-id="38c08-125">Componentes</span><span class="sxs-lookup"><span data-stu-id="38c08-125">Components</span></span>

* <span data-ttu-id="38c08-126">[Azure Application Gateway][appgateway-docs] es un equilibrador de carga de tráfico web de capa 7 que es compatible con aplicaciones y puede distribuir el tráfico según reglas de enrutamiento específicas.</span><span class="sxs-lookup"><span data-stu-id="38c08-126">[Azure Application Gateway][appgateway-docs] is a layer 7 web traffic load balancer that is application-aware and can distribute traffic based on specific routing rules.</span></span> <span data-ttu-id="38c08-127">App Gateway puede también controlar la descarga de SSL para obtener un rendimiento de servidor web mejorado.</span><span class="sxs-lookup"><span data-stu-id="38c08-127">App Gateway can also handle SSL offloading for improved web server performance.</span></span>
* <span data-ttu-id="38c08-128">[Azure Virtual Network][vnet-docs] permite que varios recursos como, por ejemplo, máquinas virtuales, se puedan comunicar de forma segura entre ellos, con Internet y con redes locales.</span><span class="sxs-lookup"><span data-stu-id="38c08-128">[Azure Virtual Network][vnet-docs] allows resources such as VMs to securely communicate with each other, the Internet, and on-premises networks.</span></span> <span data-ttu-id="38c08-129">Las redes virtuales proporcionan aislamiento y segmentación, filtrado y enrutamiento de tráfico, y permiten la conexión entre ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="38c08-129">Virtual networks provide isolation and segmentation, filter and route traffic, and allow connection between locations.</span></span> <span data-ttu-id="38c08-130">Se usan dos redes virtuales combinadas con los grupos de seguridad de red adecuados en este escenario para proporcionar una [red perimetral][dmz] (DMZ) y aislamiento para los componentes de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="38c08-130">Two virtual networks combined with the appropriate NSGs are used in this scenario to provide a [demilitarized zone][dmz] (DMZ) and isolation of the application components.</span></span> <span data-ttu-id="38c08-131">El emparejamiento de redes virtuales conecta las dos redes entre sí.</span><span class="sxs-lookup"><span data-stu-id="38c08-131">Virtual network peering connects the two networks together.</span></span>
* <span data-ttu-id="38c08-132">El [conjunto de escalado de máquinas virtuales de Azure][scaleset-docs] permite crear y administrar un grupo de máquinas virtuales idénticas con equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="38c08-132">[Azure virtual machine scale set][scaleset-docs] let you create and manager a group of identical, load balanced, VMs.</span></span> <span data-ttu-id="38c08-133">El número de instancias de máquina virtual puede aumentar o disminuir automáticamente según la demanda, o de acuerdo a una programación definida.</span><span class="sxs-lookup"><span data-stu-id="38c08-133">The number of VM instances can automatically increase or decrease in response to demand or a defined schedule.</span></span> <span data-ttu-id="38c08-134">Se usan dos conjuntos de escalado de máquinas virtuales en este escenario, uno para las instancias de la aplicación ASP.NET de front-end y otro para las instancias de máquinas virtuales de clústeres de SQL Server de back-end.</span><span class="sxs-lookup"><span data-stu-id="38c08-134">Two separate virtual machine scale sets are used in this scenario - one for the frontend ASP.NET application instances, and one for the backend SQL Server cluster VM instances.</span></span> <span data-ttu-id="38c08-135">Se puede usar Desired State Configuration (DSC) de PowerShell o la extensión de script personalizada de Azure para aprovisionar las instancias de máquinas virtuales con el software y los valores de configuración requeridos.</span><span class="sxs-lookup"><span data-stu-id="38c08-135">PowerShell desired state configuration (DSC) or the Azure custom script extension can be used to provision the VM instances with the required software and configuration settings.</span></span>
* <span data-ttu-id="38c08-136">Los [grupos de seguridad de red de Azure][nsg-docs] contienen una lista de reglas de seguridad que permiten o deniegan el tráfico entrante o saliente en función de las direcciones IP de origen o destino, el puerto y el protocolo.</span><span class="sxs-lookup"><span data-stu-id="38c08-136">[Azure network security groups][nsg-docs] contains a list of security rules that allow or deny inbound or outbound network traffic based on source or destination IP address, port, and protocol.</span></span> <span data-ttu-id="38c08-137">Las redes virtuales de este escenario se protegen con reglas de grupo de seguridad de red que restringen el flujo de tráfico entre los componentes de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="38c08-137">The virtual networks in this scenario are secured with network security group rules that restrict the flow of traffic between the application components.</span></span>
* <span data-ttu-id="38c08-138">[Azure Load Balancer][loadbalancer-docs] distribuye el tráfico entrante según reglas y sondeos de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="38c08-138">[Azure load balancer][loadbalancer-docs] distributes inbound traffic according to rules and health probes.</span></span> <span data-ttu-id="38c08-139">Una instancia de Load Balancer proporciona baja latencia y alto rendimiento, y puede escalar hasta millones de flujos para todas las aplicaciones TCP y UDP.</span><span class="sxs-lookup"><span data-stu-id="38c08-139">A load balancer provides low latency and high throughput, and scales up to millions of flows for all TCP and UDP applications.</span></span> <span data-ttu-id="38c08-140">Se usa un equilibrador de carga interno en este escenario para distribuir el tráfico desde la capa de aplicación front-end al clúster de SQL Server de back-end.</span><span class="sxs-lookup"><span data-stu-id="38c08-140">An internal load balancer is used in this scenario to distribute traffic from the frontend application tier to the backend SQL Server cluster.</span></span>
* <span data-ttu-id="38c08-141">[Azure Blob Storage][cloudwitness-docs] actúa como una ubicación de testigo en la nube para el clúster de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="38c08-141">[Azure Blob Storage][cloudwitness-docs] acts a Cloud Witness location for the SQL Server cluster.</span></span> <span data-ttu-id="38c08-142">Este testigo se usa para las operaciones del clúster y las decisiones que requieren un voto adicional para decidir el cuórum.</span><span class="sxs-lookup"><span data-stu-id="38c08-142">This witness is used for cluster operations and decisions that require an additional vote to decide quorum.</span></span> <span data-ttu-id="38c08-143">El uso de un testigo en la nube elimina la necesidad de una máquina virtual adicional para que actúe como un testigo de recurso compartido de archivos tradicional.</span><span class="sxs-lookup"><span data-stu-id="38c08-143">Using Cloud Witness removes the need for an additional VM to act as a traditional File Share Witness.</span></span>

### <a name="alternatives"></a><span data-ttu-id="38c08-144">Alternativas</span><span class="sxs-lookup"><span data-stu-id="38c08-144">Alternatives</span></span>

* <span data-ttu-id="38c08-145">\*nix, Windows se puede reemplazar fácilmente por otros sistemas operativos ya que nada en la infraestructura depende del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="38c08-145">\*nix, windows can easily be replaced by a variety of other OS's as nothing in the infrastructure depends on the OS.</span></span>

* <span data-ttu-id="38c08-146">[SQL Server para Linux][sql-linux] puede reemplazar el almacén de datos de back-end.</span><span class="sxs-lookup"><span data-stu-id="38c08-146">[SQL Server for Linux][sql-linux] can replace the back-end data store.</span></span>

* <span data-ttu-id="38c08-147">[COSMOS DB][cosmos] es otra alternativa para el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="38c08-147">[Cosmos DB][cosmos] is another another alternative for the data store.</span></span>

## <a name="considerations"></a><span data-ttu-id="38c08-148">Consideraciones</span><span class="sxs-lookup"><span data-stu-id="38c08-148">Considerations</span></span>

### <a name="availability"></a><span data-ttu-id="38c08-149">Disponibilidad</span><span class="sxs-lookup"><span data-stu-id="38c08-149">Availability</span></span>

<span data-ttu-id="38c08-150">Las instancias de máquinas virtuales en este escenario se implementan en zonas de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="38c08-150">The VM instances in this scenario are deployed across Availability Zones.</span></span> <span data-ttu-id="38c08-151">Cada zona de disponibilidad consta de uno o varios centros de datos equipados con alimentación, refrigeración y redes independientes.</span><span class="sxs-lookup"><span data-stu-id="38c08-151">Each zone is made up of one or more datacenters equipped with independent power, cooling, and networking.</span></span> <span data-ttu-id="38c08-152">Hay un mínimo de tres zonas disponibles en todas las regiones habilitadas.</span><span class="sxs-lookup"><span data-stu-id="38c08-152">A minimum of three zones are available in all enabled regions.</span></span> <span data-ttu-id="38c08-153">Esta distribución de instancias de máquinas virtuales en varias zonas proporciona alta disponibilidad para las capas de aplicación.</span><span class="sxs-lookup"><span data-stu-id="38c08-153">This distribution of VM instances across zones provides high availability to the application tiers.</span></span> <span data-ttu-id="38c08-154">Para más información, consulte [¿Qué son las zonas de disponibilidad en Azure?][azureaz-docs]</span><span class="sxs-lookup"><span data-stu-id="38c08-154">For more information, see [what are Availability Zones in Azure?][azureaz-docs]</span></span>

<span data-ttu-id="38c08-155">El nivel de base de datos se puede configurar para usar grupos de disponibilidad Always On.</span><span class="sxs-lookup"><span data-stu-id="38c08-155">The database tier can be configured to use Always On availability groups.</span></span> <span data-ttu-id="38c08-156">Con esta configuración de SQL Server, se configura una base de datos principal dentro de un clúster con un máximo de ocho bases de datos secundarias.</span><span class="sxs-lookup"><span data-stu-id="38c08-156">With this SQL Server configuration, one primary database within a cluster is configured with up to eight secondary databases.</span></span> <span data-ttu-id="38c08-157">Si se produce un problema con la base de datos principal, el clúster conmuta por error a una de las bases de datos secundarias, lo cual permite que la aplicación siga estando disponible.</span><span class="sxs-lookup"><span data-stu-id="38c08-157">If an issue occurs with the primary database, the cluster fails over to one of the secondary databases, which allows the application to continue to be available.</span></span> <span data-ttu-id="38c08-158">Para más información, consulte [Información general de los grupos de disponibilidad AlwaysOn (SQL Server)][sqlalwayson-docs].</span><span class="sxs-lookup"><span data-stu-id="38c08-158">For more information, see [Overview of Always On availability groups for SQL Server][sqlalwayson-docs].</span></span>

<span data-ttu-id="38c08-159">Para ver otros temas de disponibilidad, consulte la [lista de comprobación de disponibilidad][availability] que encontrará en Azure Architecture Center.</span><span class="sxs-lookup"><span data-stu-id="38c08-159">For other availability topics, see the [availability checklist][availability] in the Azure Architecure Center.</span></span>

### <a name="scalability"></a><span data-ttu-id="38c08-160">Escalabilidad</span><span class="sxs-lookup"><span data-stu-id="38c08-160">Scalability</span></span>

<span data-ttu-id="38c08-161">Este escenario utiliza conjuntos de escalado de máquinas virtuales para los componentes de front-end y de back-end.</span><span class="sxs-lookup"><span data-stu-id="38c08-161">This scenario uses virtual machine scale sets for the frontend and backend components.</span></span> <span data-ttu-id="38c08-162">Con los conjuntos de escalado, el número de instancias de máquina virtual que se ejecutan en la capa de aplicación de front-end se puede reducir horizontalmente de forma automática en respuesta a la demanda del cliente, o según una programación definida.</span><span class="sxs-lookup"><span data-stu-id="38c08-162">With scale sets, the number of VM instances that run the frontend application tier can automatically scale in response to customer demand, or based on a defined schedule.</span></span> <span data-ttu-id="38c08-163">Para más información, consulte [Introducción al escalado automático con conjuntos de escalado de máquinas virtuales][vmssautoscale-docs].</span><span class="sxs-lookup"><span data-stu-id="38c08-163">For more information, see [Overview of autoscale with virtual machine scale sets][vmssautoscale-docs].</span></span>

<span data-ttu-id="38c08-164">Para ver otros temas de escalabilidad, consulte la [lista de comprobación de escalabilidad][scalability] que encontrará en Azure Architecture Center.</span><span class="sxs-lookup"><span data-stu-id="38c08-164">For other scalability topics, see the [scalability checklist][scalability] in the Azure Architecure Center.</span></span>

### <a name="security"></a><span data-ttu-id="38c08-165">Seguridad</span><span class="sxs-lookup"><span data-stu-id="38c08-165">Security</span></span>

<span data-ttu-id="38c08-166">Los grupos de seguridad de red protegen todo el tráfico de la red virtual hacia la capa de aplicación de front-end.</span><span class="sxs-lookup"><span data-stu-id="38c08-166">All the virtual network traffic into the frontend application tier and protected by network security groups.</span></span> <span data-ttu-id="38c08-167">Las reglas limitan el flujo de tráfico de forma que solo las instancias de máquinas virtuales de la capa de aplicación de front-end pueden acceder al nivel de la base de datos de back-end.</span><span class="sxs-lookup"><span data-stu-id="38c08-167">Rules limit the flow of traffic so that only the frontend application tier VM instances can access the backend database tier.</span></span> <span data-ttu-id="38c08-168">No se permite ningún tráfico de Internet saliente procedente del nivel de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="38c08-168">No outbound Internet traffic is allowed from the database tier.</span></span> <span data-ttu-id="38c08-169">Para reducir la superficie de ataque, no hay ningún puerto de administración remota directa abierto.</span><span class="sxs-lookup"><span data-stu-id="38c08-169">To reduce the attack footprint, no direct remote management ports are open.</span></span> <span data-ttu-id="38c08-170">Para más información, consulte [Grupos de seguridad de red de Azure][nsg-docs].</span><span class="sxs-lookup"><span data-stu-id="38c08-170">For more information, see [Azure network security groups][nsg-docs].</span></span>

<span data-ttu-id="38c08-171">Para ver instrucciones sobre la implementación de Payment Card Industry Data Security Standard (PCI DSS 3.2), consulte [infraestructura compatible][pci-dss].</span><span class="sxs-lookup"><span data-stu-id="38c08-171">To view guidance on deploying Payment Card Industry Data Security Standards (PCI DSS 3.2) [compliant infrastructure][pci-dss].</span></span> <span data-ttu-id="38c08-172">Para obtener instrucciones generales sobre el diseño de escenarios seguros, consulte la [documentación de seguridad de Azure][security].</span><span class="sxs-lookup"><span data-stu-id="38c08-172">For general guidance on designing secure scenarios, see the [Azure Security Documentation][security].</span></span>

### <a name="resiliency"></a><span data-ttu-id="38c08-173">Resistencia</span><span class="sxs-lookup"><span data-stu-id="38c08-173">Resiliency</span></span>

<span data-ttu-id="38c08-174">En combinación con el uso de zonas de disponibilidad y conjuntos de escalado de máquinas virtuales, este escenario utiliza una instancia de Azure Application Gateway y un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="38c08-174">In combination with the use of Availability Zones and virtual machine scale sets, this scenario uses Azure Application Gateway and load balancer.</span></span> <span data-ttu-id="38c08-175">Estos dos componentes de redes distribuyen el tráfico a las instancias de máquinas virtuales conectadas e incluyen sondeos de estado que garantizan que el tráfico solo se distribuye a las máquinas virtuales correctas.</span><span class="sxs-lookup"><span data-stu-id="38c08-175">These two networking components distribute traffic to the connected VM instances, and include health probes that ensure traffic is only distributed to healthy VMs.</span></span> <span data-ttu-id="38c08-176">Se configuran dos instancias de Application Gateway en una configuración activa/pasiva, y se usa un equilibrador de carga con redundancia de zona.</span><span class="sxs-lookup"><span data-stu-id="38c08-176">Two Application Gateway instances are configured in an active-passive configuration, and a zone-redundant load balancer is used.</span></span> <span data-ttu-id="38c08-177">Esta configuración hace que los recursos y aplicaciones de red sean resistentes frente a problemas que, de lo contrario, interrumpirían el tráfico y afectarían al acceso de los usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="38c08-177">This configuration makes the networking resources and application resilient to issues that would otherwise disrupt traffic and impact end-user access.</span></span>

<span data-ttu-id="38c08-178">Para obtener instrucciones generales sobre el diseño de escenarios resistentes, consulte [Diseño de aplicaciones resistentes de Azure][resiliency].</span><span class="sxs-lookup"><span data-stu-id="38c08-178">For general guidance on designing resilient scenarios, see [Designing resilient applications for Azure][resiliency].</span></span>

## <a name="deploy-the-scenario"></a><span data-ttu-id="38c08-179">Implementación del escenario</span><span class="sxs-lookup"><span data-stu-id="38c08-179">Deploy the scenario</span></span>

<span data-ttu-id="38c08-180">**Requisitos previos**</span><span class="sxs-lookup"><span data-stu-id="38c08-180">**Prerequisites.**</span></span>

* <span data-ttu-id="38c08-181">Debe tener una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="38c08-181">You must have an existing Azure account.</span></span> <span data-ttu-id="38c08-182">Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="38c08-182">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>
* <span data-ttu-id="38c08-183">Para implementar un clúster de SQL Server en el conjunto de escalado de back-end necesita una instancia de Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="38c08-183">To deploy a SQL Server cluster into the backend scale set, you would need an Active Directory Directory Services domain.</span></span>

<span data-ttu-id="38c08-184">Para implementar la infraestructura principal de este escenario con una plantilla de Azure Resource Manager, realice los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="38c08-184">To deploy the core infrastructure for this scenario with an Azure Resource Manager template, perform the following steps.</span></span>

1. <span data-ttu-id="38c08-185">Seleccione el botón **Implementar en Azure**:</span><span class="sxs-lookup"><span data-stu-id="38c08-185">Select the **Deploy to Azure** button:</span></span><br><a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmspnp%2Fsolution-architectures%2Fmaster%2Finfrastructure%2Fregulated-multitier-app%2Fazuredeploy.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a>
2. <span data-ttu-id="38c08-186">Espere a que la implementación de plantilla se abra en Azure Portal y complete los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="38c08-186">Wait for the template deployment to open in the Azure portal, then complete the following steps:</span></span>
   * <span data-ttu-id="38c08-187">Elija **Crear nuevo** para el grupo de recursos y proporcione un nombre como, por ejemplo, *myWindowsscenario*, en el cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="38c08-187">Choose to **Create new** resource group, then provide a name such as *myWindowsscenario* in the text box.</span></span>
   * <span data-ttu-id="38c08-188">Seleccione una región en el cuadro de lista desplegable **Ubicación**.</span><span class="sxs-lookup"><span data-stu-id="38c08-188">Select a region from the **Location** drop-down box.</span></span>
   * <span data-ttu-id="38c08-189">Indique un nombre de usuario y una contraseña segura para las instancias de conjuntos de escalado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="38c08-189">Provide a username and secure password for the virtual machine scale set instances.</span></span>
   * <span data-ttu-id="38c08-190">Revise los términos y condiciones, y seleccione **Acepto los términos y condiciones indicados anteriormente**.</span><span class="sxs-lookup"><span data-stu-id="38c08-190">Review the terms and conditions, then check **I agree to the terms and conditions stated above**.</span></span>
   * <span data-ttu-id="38c08-191">Seleccione el botón **Comprar**.</span><span class="sxs-lookup"><span data-stu-id="38c08-191">Select the **Purchase** button.</span></span>

<span data-ttu-id="38c08-192">La implementación puede tardar unos 15-20 minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="38c08-192">It can take 15-20 minutes for the deployment to complete.</span></span>

## <a name="pricing"></a><span data-ttu-id="38c08-193">Precios</span><span class="sxs-lookup"><span data-stu-id="38c08-193">Pricing</span></span>

<span data-ttu-id="38c08-194">Para explorar el costo de ejecutar este escenario, todos los servicios están preconfigurados en la calculadora de costos.</span><span class="sxs-lookup"><span data-stu-id="38c08-194">To explore the cost of running this scenario, all of the services are pre-configured in the cost calculator.</span></span>  <span data-ttu-id="38c08-195">Para ver cómo cambiarían los precios en su caso concreto, cambie las variables pertinentes para que coincidan con el tráfico esperado.</span><span class="sxs-lookup"><span data-stu-id="38c08-195">To see how the pricing would change for your particular use case, change the appropriate variables to match your expected traffic.</span></span>

<span data-ttu-id="38c08-196">Hemos incluido tres perfiles de costos de ejemplo basados en el número de instancias de conjuntos de escalado de máquinas virtuales que ejecutan las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="38c08-196">We have provided three sample cost profiles based on the number of scale set VM instances that run your applications.</span></span>

* <span data-ttu-id="38c08-197">[Pequeño][small-pricing]: este perfil correlaciona dos instancias de máquina virtual de front-end y dos de back-end.</span><span class="sxs-lookup"><span data-stu-id="38c08-197">[Small][small-pricing]: this correlates to two frontend and two backend VM instances.</span></span>
* <span data-ttu-id="38c08-198">[Mediano][medium-pricing]: este perfil correlaciona 20 instancias de máquina virtual de front-end y 5 de back-end.</span><span class="sxs-lookup"><span data-stu-id="38c08-198">[Medium][medium-pricing]: this correlates to 20 frontend and 5 backend VM instances.</span></span>
* <span data-ttu-id="38c08-199">[Grande][large-pricing]: este perfil correlaciona 100 instancias de máquina virtual de front-end y 10 de back-end.</span><span class="sxs-lookup"><span data-stu-id="38c08-199">[Large][large-pricing]: this correlates to 100 frontend and 10 backend VM instances.</span></span>

## <a name="related-resources"></a><span data-ttu-id="38c08-200">Recursos relacionados</span><span class="sxs-lookup"><span data-stu-id="38c08-200">Related Resources</span></span>

<span data-ttu-id="38c08-201">Este escenario usa un conjunto de escalado de máquinas virtuales de back-end que ejecuta un clúster de Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="38c08-201">This scenario used a backend virtual machine scale set that runs a Microsoft SQL Server cluster.</span></span> <span data-ttu-id="38c08-202">También se puede usar Azure Cosmos DB como un nivel de base de datos escalable y seguro para los datos de aplicación.</span><span class="sxs-lookup"><span data-stu-id="38c08-202">Azure Cosmos DB could also be used as a scalable and secure database tier for the application data.</span></span> <span data-ttu-id="38c08-203">Un [punto de conexión de servicio de red virtual de Azure][vnetendpoint-docs] le permite proteger los recursos de los servicios de Azure fundamentales solo para las redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="38c08-203">An [Azure virtual network service endpoint][vnetendpoint-docs] allow you to secure your critical Azure service resources to only your virtual networks.</span></span> <span data-ttu-id="38c08-204">En este escenario, los puntos de conexión le permiten proteger el tráfico entre la capa de aplicación de front-end y Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="38c08-204">In this scenario, VNet endpoints allow you to secure traffic between the frontend application tier and Cosmos DB.</span></span> <span data-ttu-id="38c08-205">Para más información sobre Cosmos DB, consulte [Introducción a Azure Cosmos DB][azurecosmosdb-docs].</span><span class="sxs-lookup"><span data-stu-id="38c08-205">For more information on Cosmos DB, see [Azure Cosmos DB overview][azurecosmosdb-docs].</span></span>

<span data-ttu-id="38c08-206">También puede ver una completa [arquitectura de referencia para una aplicación de n niveles genérica con SQL Server][ntiersql-ra].</span><span class="sxs-lookup"><span data-stu-id="38c08-206">You also view a thorough [reference architecture for a generic N-tier application with SQL Server][ntiersql-ra].</span></span>

<!-- links -->
[appgateway-docs]: /azure/application-gateway/overview
[architecture]: ./media/regulated-multitier-app/architecture-regulated-multitier-app.png
[autoscaling]: /azure/architecture/best-practices/auto-scaling
[availability]: /architecture/checklist/availability
[azureaz-docs]: /azure/availability-zones/az-overview
[azurecosmosdb-docs]: /azure/cosmos-db/introduction
[cloudwitness-docs]: /windows-server/failover-clustering/deploy-cloud-witness
[loadbalancer-docs]: /azure/load-balancer/load-balancer-overview
[nsg-docs]: /azure/virtual-network/security-overview
[ntiersql-ra]: /azure/architecture/reference-architectures/n-tier/n-tier-sql-server
[resiliency]: /azure/architecture/resiliency/ 
[security]: /azure/security/
[scalability]: /azure/architecture/checklist/scalability 
[scaleset-docs]: /azure/virtual-machine-scale-sets/overview
[sqlalwayson-docs]: /sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server
[vmssautoscale-docs]: /azure/virtual-machine-scale-sets/virtual-machine-scale-sets-autoscale-overview
[vnet-docs]: /azure/virtual-network/virtual-networks-overview
[vnetendpoint-docs]: /azure/virtual-network/virtual-network-service-endpoints-overview
[pci-dss]: /azure/security/blueprints/pcidss-iaaswa-overview
[dmz]: /azure/virtual-network/virtual-networks-dmz-nsg
[cosmos]: /azure/cosmos-db/
[sql-linux]: /sql/linux/sql-server-linux-overview?view=sql-server-linux-2017

[small-pricing]: https://azure.com/e/711bbfcbbc884ef8aa91cdf0f2caff72
[medium-pricing]: https://azure.com/e/b622d82d79b34b8398c4bce35477856f
[large-pricing]: https://azure.com/e/1d99d8b92f90496787abecffa1473a93