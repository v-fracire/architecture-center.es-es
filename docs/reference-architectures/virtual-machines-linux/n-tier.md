---
title: "Ejecución de máquinas virtuales Linux para una aplicación de n niveles en Azure"
description: "Cómo ejecutar máquinas virtuales Linux para una arquitectura de n niveles en Microsoft Azure."
author: MikeWasson
ms.date: 11/22/2016
pnp.series.title: Linux VM workloads
pnp.series.next: multi-region-application
pnp.series.prev: multi-vm
ms.openlocfilehash: 673e090e306ffc421603371658c8273b10b980d4
ms.sourcegitcommit: b0482d49aab0526be386837702e7724c61232c60
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/14/2017
---
# <a name="run-linux-vms-for-an-n-tier-application"></a><span data-ttu-id="336ca-103">Ejecución de máquinas virtuales Linux para una aplicación de n niveles</span><span class="sxs-lookup"><span data-stu-id="336ca-103">Run Linux VMs for an N-tier application</span></span>

<span data-ttu-id="336ca-104">En esta arquitectura de referencia se muestra un conjunto de prácticas demostradas para ejecutar máquinas virtuales Linux para una aplicación de n niveles.</span><span class="sxs-lookup"><span data-stu-id="336ca-104">This reference architecture shows a set of proven practices for running Linux virtual machines (VMs) for an N-tier application.</span></span> [<span data-ttu-id="336ca-105">**Implemente esta solución**.</span><span class="sxs-lookup"><span data-stu-id="336ca-105">**Deploy this solution**.</span></span>](#deploy-the-solution)  

<span data-ttu-id="336ca-106">![[0]][0]</span><span class="sxs-lookup"><span data-stu-id="336ca-106">![[0]][0]</span></span>

<span data-ttu-id="336ca-107">*Descargue un [archivo Visio][visio-download] de esta arquitectura.*</span><span class="sxs-lookup"><span data-stu-id="336ca-107">*Download a [Visio file][visio-download] of this architecture.*</span></span>

## <a name="architecture"></a><span data-ttu-id="336ca-108">Arquitectura</span><span class="sxs-lookup"><span data-stu-id="336ca-108">Architecture</span></span>

<span data-ttu-id="336ca-109">Hay muchas maneras de implementar una arquitectura de n niveles.</span><span class="sxs-lookup"><span data-stu-id="336ca-109">There are many ways to implement an N-tier architecture.</span></span> <span data-ttu-id="336ca-110">En el diagrama se muestra una aplicación web típica de tres niveles.</span><span class="sxs-lookup"><span data-stu-id="336ca-110">The diagram shows a typical 3-tier web application.</span></span> <span data-ttu-id="336ca-111">Esta arquitectura se basa en [Ejecución de máquinas virtuales de carga equilibrada para escalabilidad y disponibilidad][multi-vm].</span><span class="sxs-lookup"><span data-stu-id="336ca-111">This architecture builds on [Run load-balanced VMs for scalability and availability][multi-vm].</span></span> <span data-ttu-id="336ca-112">Los niveles Web y Business usan máquinas virtuales de carga equilibrada.</span><span class="sxs-lookup"><span data-stu-id="336ca-112">The web and business tiers use load-balanced VMs.</span></span>

* <span data-ttu-id="336ca-113">**Conjuntos de disponibilidad**.</span><span class="sxs-lookup"><span data-stu-id="336ca-113">**Availability sets.**</span></span> <span data-ttu-id="336ca-114">Cree un [conjunto de disponibilidad][azure-availability-sets] para cada nivel y aprovisione al menos dos máquinas virtuales en cada nivel.</span><span class="sxs-lookup"><span data-stu-id="336ca-114">Create an [availability set][azure-availability-sets] for each tier, and provision at least two VMs in each tier.</span></span>  <span data-ttu-id="336ca-115">Esto hace que las máquinas virtuales sean aptas para un [Acuerdo de Nivel de Servicio (SLA)][vm-sla] mayor.</span><span class="sxs-lookup"><span data-stu-id="336ca-115">This makes the VMs eligible for a higher [service level agreement (SLA)][vm-sla] for VMs.</span></span>
* <span data-ttu-id="336ca-116">**Subredes**.</span><span class="sxs-lookup"><span data-stu-id="336ca-116">**Subnets.**</span></span> <span data-ttu-id="336ca-117">Cree una subred independiente para cada nivel.</span><span class="sxs-lookup"><span data-stu-id="336ca-117">Create a separate subnet for each tier.</span></span> <span data-ttu-id="336ca-118">Especifique el intervalo de direcciones y la máscara de subred con la notación [CIDR].</span><span class="sxs-lookup"><span data-stu-id="336ca-118">Specify the address range and subnet mask using [CIDR] notation.</span></span> 
* <span data-ttu-id="336ca-119">**Equilibradores de carga.**</span><span class="sxs-lookup"><span data-stu-id="336ca-119">**Load balancers.**</span></span> <span data-ttu-id="336ca-120">Use un [equilibrador de carga con conexión a Internet][load-balancer-external] para distribuir el tráfico entrante de Internet al nivel Web y un [equilibrador de carga interno][load-balancer-internal] para distribuir el tráfico de red del nivel Web al nivel Business.</span><span class="sxs-lookup"><span data-stu-id="336ca-120">Use an [Internet-facing load balancer][load-balancer-external] to distribute incoming Internet traffic to the web tier, and an [internal load balancer][load-balancer-internal] to distribute network traffic from the web tier to the business tier.</span></span>
* <span data-ttu-id="336ca-121">**JumpBox.**</span><span class="sxs-lookup"><span data-stu-id="336ca-121">**Jumpbox.**</span></span> <span data-ttu-id="336ca-122">También se denomina [host bastión].</span><span class="sxs-lookup"><span data-stu-id="336ca-122">Also called a [bastion host].</span></span> <span data-ttu-id="336ca-123">Se trata de una máquina virtual segura en la red que usan los administradores para conectarse al resto de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="336ca-123">A secure VM on the network that administrators use to connect to the other VMs.</span></span> <span data-ttu-id="336ca-124">El JumpBox tiene un NSG que solo permite el tráfico remoto que procede de direcciones IP públicas de una lista segura.</span><span class="sxs-lookup"><span data-stu-id="336ca-124">The jumpbox has an NSG that allows remote traffic only from public IP addresses on a safe list.</span></span> <span data-ttu-id="336ca-125">El NSG debe permitir el tráfico a través de Secure Shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="336ca-125">The NSG should permit secure shell (SSH) traffic.</span></span>
* <span data-ttu-id="336ca-126">**Supervisión.**</span><span class="sxs-lookup"><span data-stu-id="336ca-126">**Monitoring.**</span></span> <span data-ttu-id="336ca-127">El software de supervisión, como [Nagios], [Zabbix] o [Icinga], puede ofrecerle información sobre el tiempo de respuesta, el tiempo de actividad de la máquina virtual y el estado general del sistema.</span><span class="sxs-lookup"><span data-stu-id="336ca-127">Monitoring software such as [Nagios], [Zabbix], or [Icinga] can give you insight into response time, VM uptime, and the overall health of your system.</span></span> <span data-ttu-id="336ca-128">Instale el software de supervisión en una máquina virtual que se encuentre en una subred de administración independiente.</span><span class="sxs-lookup"><span data-stu-id="336ca-128">Install the monitoring software on a VM that's placed in a separate management subnet.</span></span>
* <span data-ttu-id="336ca-129">**Grupos de seguridad de red.**</span><span class="sxs-lookup"><span data-stu-id="336ca-129">**NSGs.**</span></span> <span data-ttu-id="336ca-130">Use [grupos de seguridad de red][nsg] (NSG) para restringir el tráfico de red dentro de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="336ca-130">Use [network security groups][nsg] (NSGs) to restrict network traffic within the VNet.</span></span> <span data-ttu-id="336ca-131">Por ejemplo, en la arquitectura de tres niveles que se muestra aquí, el nivel de base de datos no acepta el tráfico desde el front-end web, solo desde el nivel Business y la subred de administración.</span><span class="sxs-lookup"><span data-stu-id="336ca-131">For example, in the 3-tier architecture shown here, the database tier does not accept traffic from the web front end, only from the business tier and the management subnet.</span></span>
* <span data-ttu-id="336ca-132">**Base de datos Apache Cassandra**.</span><span class="sxs-lookup"><span data-stu-id="336ca-132">**Apache Cassandra database**.</span></span> <span data-ttu-id="336ca-133">Proporciona alta disponibilidad en el nivel de datos, al habilitar la replicación y la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="336ca-133">Provides high availability at the data tier, by enabling replication and failover.</span></span>

## <a name="recommendations"></a><span data-ttu-id="336ca-134">Recomendaciones</span><span class="sxs-lookup"><span data-stu-id="336ca-134">Recommendations</span></span>

<span data-ttu-id="336ca-135">Los requisitos pueden diferir de los de la arquitectura que se describe aquí.</span><span class="sxs-lookup"><span data-stu-id="336ca-135">Your requirements might differ from the architecture described here.</span></span> <span data-ttu-id="336ca-136">Use estas recomendaciones como punto inicial.</span><span class="sxs-lookup"><span data-stu-id="336ca-136">Use these recommendations as a starting point.</span></span> 

### <a name="vnet--subnets"></a><span data-ttu-id="336ca-137">Red virtual/subredes</span><span class="sxs-lookup"><span data-stu-id="336ca-137">VNet / Subnets</span></span>

<span data-ttu-id="336ca-138">Cuando cree la red virtual, determine cuántas direcciones IP requieren los recursos de cada subred.</span><span class="sxs-lookup"><span data-stu-id="336ca-138">When you create the VNet, determine how many IP addresses your resources in each subnet require.</span></span> <span data-ttu-id="336ca-139">Especifique una máscara de subred y un intervalo de direcciones de la red virtual lo suficientemente grande para la dirección IP requerida con el uso de la notación [CIDR].</span><span class="sxs-lookup"><span data-stu-id="336ca-139">Specify a subnet mask and a VNet address range large enough for the required IP addresses using [CIDR] notation.</span></span> <span data-ttu-id="336ca-140">Use un espacio de direcciones que se encuentre dentro de los [bloques de direcciones IP privados][private-ip-space] estándar, que son 10.0.0.0/8, 172.16.0.0/12 y 192.168.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="336ca-140">Use an address space that falls within the standard [private IP address blocks][private-ip-space], which are 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16.</span></span>

<span data-ttu-id="336ca-141">Elija un intervalo de direcciones que no se superponga con la red local, en caso de que necesite configurar una puerta de enlace entre la red virtual y la red local más adelante.</span><span class="sxs-lookup"><span data-stu-id="336ca-141">Choose an address range that does not overlap with your on-premises network, in case you need to set up a gateway between the VNet and your on-premises network later.</span></span> <span data-ttu-id="336ca-142">Una vez creada la red virtual, no se puede cambiar el intervalo de direcciones.</span><span class="sxs-lookup"><span data-stu-id="336ca-142">Once you create the VNet, you can't change the address range.</span></span>

<span data-ttu-id="336ca-143">Diseñe subredes teniendo en cuenta los requisitos de funcionalidad y seguridad.</span><span class="sxs-lookup"><span data-stu-id="336ca-143">Design subnets with functionality and security requirements in mind.</span></span> <span data-ttu-id="336ca-144">Todas las máquinas virtuales dentro del mismo nivel o rol deben incluirse en la misma subred, lo que puede servir como un límite de seguridad.</span><span class="sxs-lookup"><span data-stu-id="336ca-144">All VMs within the same tier or role should go into the same subnet, which can be a security boundary.</span></span> <span data-ttu-id="336ca-145">Para obtener más información sobre el diseño de redes virtuales y subredes, vea [Planeación y diseño de redes virtuales de Azure][plan-network].</span><span class="sxs-lookup"><span data-stu-id="336ca-145">For more information about designing VNets and subnets, see [Plan and design Azure Virtual Networks][plan-network].</span></span>

<span data-ttu-id="336ca-146">Para cada subred, especifique el espacio de direcciones de la subred en la notación CIDR.</span><span class="sxs-lookup"><span data-stu-id="336ca-146">For each subnet, specify the address space for the subnet in CIDR notation.</span></span> <span data-ttu-id="336ca-147">Por ejemplo, "10.0.0.0/24" crea un intervalo de doscientas cincuenta y seis direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="336ca-147">For example, '10.0.0.0/24' creates a range of 256 IP addresses.</span></span> <span data-ttu-id="336ca-148">Las máquinas virtuales pueden usar doscientas cincuenta y una; cinco están reservadas.</span><span class="sxs-lookup"><span data-stu-id="336ca-148">VMs can use 251 of these; five are reserved.</span></span> <span data-ttu-id="336ca-149">Asegúrese de que los intervalos de direcciones no se superponen entre las subredes.</span><span class="sxs-lookup"><span data-stu-id="336ca-149">Make sure the address ranges don't overlap across subnets.</span></span> <span data-ttu-id="336ca-150">Vea [Preguntas más frecuentes (P+F) acerca de Azure Virtual Network][vnet faq].</span><span class="sxs-lookup"><span data-stu-id="336ca-150">See the [Virtual Network FAQ][vnet faq].</span></span>

### <a name="network-security-groups"></a><span data-ttu-id="336ca-151">Grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="336ca-151">Network security groups</span></span>

<span data-ttu-id="336ca-152">Use reglas NSG para restringir el tráfico entre los niveles.</span><span class="sxs-lookup"><span data-stu-id="336ca-152">Use NSG rules to restrict traffic between tiers.</span></span> <span data-ttu-id="336ca-153">Por ejemplo, en la arquitectura de tres niveles mostrada anteriormente, el nivel Web no se comunica directamente con el nivel de base de datos.</span><span class="sxs-lookup"><span data-stu-id="336ca-153">For example, in the 3-tier architecture shown above, the web tier does not communicate directly with the database tier.</span></span> <span data-ttu-id="336ca-154">Para exigir esto, el nivel de base de datos debe bloquear el tráfico entrante desde la subred del nivel Web.</span><span class="sxs-lookup"><span data-stu-id="336ca-154">To enforce this, the database tier should block incoming traffic from the web tier subnet.</span></span>  

1. <span data-ttu-id="336ca-155">Cree un NSG y asócielo a la subred del nivel de base de datos.</span><span class="sxs-lookup"><span data-stu-id="336ca-155">Create an NSG and associate it to the database tier subnet.</span></span>
2. <span data-ttu-id="336ca-156">Agregue una regla que deniegue todo el tráfico entrante de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="336ca-156">Add a rule that denies all inbound traffic from the VNet.</span></span> <span data-ttu-id="336ca-157">(Use la etiqueta `VIRTUAL_NETWORK` de la regla).</span><span class="sxs-lookup"><span data-stu-id="336ca-157">(Use the `VIRTUAL_NETWORK` tag in the rule.)</span></span> 
3. <span data-ttu-id="336ca-158">Agregue una regla con mayor prioridad que permita el tráfico entrante de la subred del nivel Business.</span><span class="sxs-lookup"><span data-stu-id="336ca-158">Add a rule with a higher priority that allows inbound traffic from the business tier subnet.</span></span> <span data-ttu-id="336ca-159">Esta regla invalida la regla anterior y permite al nivel Business comunicarse con el nivel de base de datos.</span><span class="sxs-lookup"><span data-stu-id="336ca-159">This rule overrides the previous rule, and allows the business tier to talk to the database tier.</span></span>
4. <span data-ttu-id="336ca-160">Agregue una regla que permita el tráfico entrante desde dentro de la subred del nivel de base de datos.</span><span class="sxs-lookup"><span data-stu-id="336ca-160">Add a rule that allows inbound traffic from within the database tier subnet itself.</span></span> <span data-ttu-id="336ca-161">Esta regla permite la comunicación entre las máquinas virtuales en el nivel de base de datos, que es necesario para la replicación y la conmutación por error de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="336ca-161">This rule allows communication between VMs in the database tier, which is needed for database replication and failover.</span></span>
5. <span data-ttu-id="336ca-162">Agregue una regla que permita el tráfico SSH de la subred de JumpBox.</span><span class="sxs-lookup"><span data-stu-id="336ca-162">Add a rule that allows SSH traffic from the jumpbox subnet.</span></span> <span data-ttu-id="336ca-163">Esta regla permite a los administradores conectarse al nivel de base de datos desde JumpBox.</span><span class="sxs-lookup"><span data-stu-id="336ca-163">This rule lets administrators connect to the database tier from the jumpbox.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="336ca-164">Un NSG tiene [reglas predeterminadas][nsg-rules] que permiten todo el tráfico entrante desde dentro de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="336ca-164">An NSG has [default rules][nsg-rules] that allow any inbound traffic from within the VNet.</span></span> <span data-ttu-id="336ca-165">Estas reglas no se pueden eliminar, pero sí se pueden invalidar con la creación de reglas de mayor prioridad.</span><span class="sxs-lookup"><span data-stu-id="336ca-165">These rules can't be deleted, but you can override them by creating higher-priority rules.</span></span>
   > 
   > 

### <a name="load-balancers"></a><span data-ttu-id="336ca-166">Equilibradores de carga</span><span class="sxs-lookup"><span data-stu-id="336ca-166">Load balancers</span></span>

<span data-ttu-id="336ca-167">El equilibrador de carga externo distribuye el tráfico de Internet al nivel Web.</span><span class="sxs-lookup"><span data-stu-id="336ca-167">The external load balancer distributes Internet traffic to the web tier.</span></span> <span data-ttu-id="336ca-168">Cree una dirección IP pública para este equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="336ca-168">Create a public IP address for this load balancer.</span></span> <span data-ttu-id="336ca-169">Vea [Creación de un equilibrador de carga orientado a Internet mediante Azure Portal][lb-external-create].</span><span class="sxs-lookup"><span data-stu-id="336ca-169">See [Creating an Internet-facing load balancer][lb-external-create].</span></span>

<span data-ttu-id="336ca-170">El equilibrador de carga interno distribuye el tráfico de red del nivel Web al nivel Business.</span><span class="sxs-lookup"><span data-stu-id="336ca-170">The internal load balancer distributes network traffic from the web tier to the business tier.</span></span> <span data-ttu-id="336ca-171">Para asignar una dirección IP privada a este equilibrador de carga, cree una configuración de IP de front-end y asóciela a la subred para el nivel Business.</span><span class="sxs-lookup"><span data-stu-id="336ca-171">To give this load balancer a private IP address, create a frontend IP configuration and associate it with the subnet for the business tier.</span></span> <span data-ttu-id="336ca-172">Vea [Creación de un equilibrador de carga interno en Azure Portal][lb-internal-create].</span><span class="sxs-lookup"><span data-stu-id="336ca-172">See [Get started creating an Internal load balancer][lb-internal-create].</span></span>

### <a name="cassandra"></a><span data-ttu-id="336ca-173">Cassandra</span><span class="sxs-lookup"><span data-stu-id="336ca-173">Cassandra</span></span>

<span data-ttu-id="336ca-174">Se recomienda [DataStax Enterprise][datastax] para usos de producción, pero estas recomendaciones se aplican a cualquier edición de Cassandra.</span><span class="sxs-lookup"><span data-stu-id="336ca-174">We recommend [DataStax Enterprise][datastax] for production use, but these recommendations apply to any Cassandra edition.</span></span> <span data-ttu-id="336ca-175">Para más información sobre cómo ejecutar DataStax en Azure, consulte [DataStax Enterprise Deployment Guide for Azure][cassandra-in-azure] (Guía de implementación de DataStax Enterprise Deployment para Azure).</span><span class="sxs-lookup"><span data-stu-id="336ca-175">For more information on running DataStax in Azure, see [DataStax Enterprise Deployment Guide for Azure][cassandra-in-azure].</span></span> 

<span data-ttu-id="336ca-176">Coloque las máquinas virtuales de un clúster de Cassandra en un conjunto de disponibilidad para asegurarse de que las réplicas de Cassandra se distribuyen entre varios dominios de error y dominios de actualización.</span><span class="sxs-lookup"><span data-stu-id="336ca-176">Put the VMs for a Cassandra cluster in an availability set to ensure that the Cassandra replicas are distributed across multiple fault domains and upgrade domains.</span></span> <span data-ttu-id="336ca-177">Para obtener más información sobre los dominios de error y los dominios de actualización, vea [Administración de la disponibilidad de las máquinas virtuales][azure-availability-sets].</span><span class="sxs-lookup"><span data-stu-id="336ca-177">For more information about fault domains and upgrade domains, see [Manage the availability of virtual machines][azure-availability-sets].</span></span> 

<span data-ttu-id="336ca-178">Configure tres dominios de error como máximo por cada conjunto de disponibilidad y dieciocho dominios de actualización por cada conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="336ca-178">Configure three fault domains (the maximum) per availability set and 18 upgrade domains per availability set.</span></span> <span data-ttu-id="336ca-179">Esto proporciona el número máximo de dominios de actualización que todavía se pueden distribuir uniformemente entre los dominios de error.</span><span class="sxs-lookup"><span data-stu-id="336ca-179">This provides the maximum number of upgrade domains that can still be distributed evenly across the fault domains.</span></span>   

<span data-ttu-id="336ca-180">Configure los nodos en el modo de reconocimiento del bastidor.</span><span class="sxs-lookup"><span data-stu-id="336ca-180">Configure nodes in rack-aware mode.</span></span> <span data-ttu-id="336ca-181">Asigne los dominios de error a los bastidores en el archivo `cassandra-rackdc.properties`.</span><span class="sxs-lookup"><span data-stu-id="336ca-181">Map fault domains to racks in the `cassandra-rackdc.properties` file.</span></span>

<span data-ttu-id="336ca-182">No se necesita un equilibrador de carga delante del clúster.</span><span class="sxs-lookup"><span data-stu-id="336ca-182">You don't need a load balancer in front of the cluster.</span></span> <span data-ttu-id="336ca-183">El cliente se conecta directamente a un nodo del clúster.</span><span class="sxs-lookup"><span data-stu-id="336ca-183">The client connects directly to a node in the cluster.</span></span>

### <a name="jumpbox"></a><span data-ttu-id="336ca-184">JumpBox</span><span class="sxs-lookup"><span data-stu-id="336ca-184">Jumpbox</span></span>

<span data-ttu-id="336ca-185">JumpBox tendrá requisitos mínimos de rendimiento, por lo que se debe seleccionar un tamaño pequeño de máquina virtual para JumpBox, como Estándar A1.</span><span class="sxs-lookup"><span data-stu-id="336ca-185">The jumpbox will have minimal performance requirements, so select a small VM size for the jumpbox such as Standard A1.</span></span> 

<span data-ttu-id="336ca-186">Cree una [dirección IP pública] para JumpBox.</span><span class="sxs-lookup"><span data-stu-id="336ca-186">Create a [public IP address] for the jumpbox.</span></span> <span data-ttu-id="336ca-187">Coloque JumpBox en la misma red virtual que las demás máquinas virtuales, pero en una subred de administración independiente.</span><span class="sxs-lookup"><span data-stu-id="336ca-187">Place the jumpbox in the same VNet as the other VMs, but in a separate management subnet.</span></span>

<span data-ttu-id="336ca-188">No permita el acceso SSH desde la red pública de Internet a las máquinas virtuales que ejecutan la carga de trabajo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="336ca-188">Do not allow SSH access from the public Internet to the VMs that run the application workload.</span></span> <span data-ttu-id="336ca-189">En su lugar, todo el acceso SSH a estas máquinas virtuales debe realizarse a través de JumpBox.</span><span class="sxs-lookup"><span data-stu-id="336ca-189">Instead, all SSH access to these VMs must come through the jumpbox.</span></span> <span data-ttu-id="336ca-190">Un administrador inicia sesión en JumpBox y, después, en la otra máquina virtual desde JumpBox.</span><span class="sxs-lookup"><span data-stu-id="336ca-190">An administrator logs into the jumpbox, and then logs into the other VM from the jumpbox.</span></span> <span data-ttu-id="336ca-191">JumpBox permite el tráfico SSH desde Internet, pero solo desde direcciones IP conocidas y seguras.</span><span class="sxs-lookup"><span data-stu-id="336ca-191">The jumpbox allows SSH traffic from the Internet, but only from known, safe IP addresses.</span></span>

<span data-ttu-id="336ca-192">Para proteger JumpBox, cree un NSG y aplíquelo a la subred de JumpBox.</span><span class="sxs-lookup"><span data-stu-id="336ca-192">To secure the jumpbox, create an NSG and apply it to the jumpbox subnet.</span></span> <span data-ttu-id="336ca-193">Agregue una regla NSG que permita las conexiones SSH solo desde un conjunto seguro de direcciones IP públicas.</span><span class="sxs-lookup"><span data-stu-id="336ca-193">Add an NSG rule that allows SSH connections only from a safe set of public IP addresses.</span></span> <span data-ttu-id="336ca-194">El NSG puede adjuntarse a la subred o al NIC de JumpBox.</span><span class="sxs-lookup"><span data-stu-id="336ca-194">The NSG can be attached either to the subnet or to the jumpbox NIC.</span></span> <span data-ttu-id="336ca-195">En este caso, se recomienda asociarlo a la NIC, para que solo se permita el tráfico SSH a JumpBox, incluso si agrega otras máquinas virtuales a la misma subred.</span><span class="sxs-lookup"><span data-stu-id="336ca-195">In this case, we recommend attaching it to the NIC, so SSH traffic is permitted only to the jumpbox, even if you add other VMs to the same subnet.</span></span>

<span data-ttu-id="336ca-196">Configure el NSG para las demás subredes, a fin de permitir el tráfico SSH de la subred de administración.</span><span class="sxs-lookup"><span data-stu-id="336ca-196">Configure the NSGs for the other subnets to allow SSH traffic from the management subnet.</span></span>

## <a name="availability-considerations"></a><span data-ttu-id="336ca-197">Consideraciones sobre disponibilidad</span><span class="sxs-lookup"><span data-stu-id="336ca-197">Availability considerations</span></span>

<span data-ttu-id="336ca-198">Coloque cada nivel o rol de máquina virtual en un conjunto de disponibilidad independiente.</span><span class="sxs-lookup"><span data-stu-id="336ca-198">Put each tier or VM role into a separate availability set.</span></span> 

<span data-ttu-id="336ca-199">En el nivel de base de datos, tener varias máquinas virtuales no supone automáticamente disponer de una base de datos de alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="336ca-199">At the database tier, having multiple VMs does not automatically translate into a highly available database.</span></span> <span data-ttu-id="336ca-200">Para una base de datos relacional, normalmente deberá usar la replicación y la conmutación por error para lograr una alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="336ca-200">For a relational database, you will typically need to use replication and failover to achieve high availability.</span></span>  

<span data-ttu-id="336ca-201">Si necesita más disponibilidad de la que proporciona el [SLA de Azure para máquinas virtuales][vm-sla], replique la aplicación entre dos regiones y use Azure Traffic Manager para la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="336ca-201">If you need higher availability than the [Azure SLA for VMs][vm-sla] provides, replicate the application across two regions and use Azure Traffic Manager for failover.</span></span> <span data-ttu-id="336ca-202">Para más información, vea [Run Linux VMs in multiple regions for high availability][multi-dc] (Ejecución de máquinas virtuales Linux en varias regiones para alta disponibilidad).</span><span class="sxs-lookup"><span data-stu-id="336ca-202">For more information, see [Run Linux VMs in multiple regions for high availability][multi-dc].</span></span>  

## <a name="security-considerations"></a><span data-ttu-id="336ca-203">Consideraciones sobre la seguridad</span><span class="sxs-lookup"><span data-stu-id="336ca-203">Security considerations</span></span>

<span data-ttu-id="336ca-204">Considere la posibilidad de agregar una aplicación virtual de red (NVA) para crear una red perimetral entre la red pública de Internet y la red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="336ca-204">Consider adding a network virtual appliance (NVA) to create a DMZ between the public Internet and the Azure virtual network.</span></span> <span data-ttu-id="336ca-205">NVA es un término genérico para una aplicación virtual que puede realizar tareas relacionadas con la red, como firewall, inspección de paquetes, auditoría y enrutamiento personalizado.</span><span class="sxs-lookup"><span data-stu-id="336ca-205">NVA is a generic term for a virtual appliance that can perform network-related tasks such as firewall, packet inspection, auditing, and custom routing.</span></span> <span data-ttu-id="336ca-206">Para más información, vea [Implementación de una red perimetral entre Internet y Azure][dmz].</span><span class="sxs-lookup"><span data-stu-id="336ca-206">For more information, see [Implementing a DMZ between Azure and the Internet][dmz].</span></span>

## <a name="scalability-considerations"></a><span data-ttu-id="336ca-207">Consideraciones sobre escalabilidad</span><span class="sxs-lookup"><span data-stu-id="336ca-207">Scalability considerations</span></span>

<span data-ttu-id="336ca-208">Los equilibradores de carga distribuyen el tráfico de red a los niveles Web y Business.</span><span class="sxs-lookup"><span data-stu-id="336ca-208">The load balancers distribute network traffic to the web and business tiers.</span></span> <span data-ttu-id="336ca-209">Escale horizontalmente mediante la adición de instancias de máquina virtual nuevas.</span><span class="sxs-lookup"><span data-stu-id="336ca-209">Scale horizontally by adding new VM instances.</span></span> <span data-ttu-id="336ca-210">Tenga en cuenta que se pueden escalar los niveles Web y Business por separado, según la carga.</span><span class="sxs-lookup"><span data-stu-id="336ca-210">Note that you can scale the web and business tiers independently, based on load.</span></span> <span data-ttu-id="336ca-211">Para reducir las posibles complicaciones causadas por la necesidad de mantener la afinidad del cliente, las máquinas virtuales del nivel Web no deben tener ningún estado.</span><span class="sxs-lookup"><span data-stu-id="336ca-211">To reduce possible complications caused by the need to maintain client affinity, the VMs in the web tier should be stateless.</span></span> <span data-ttu-id="336ca-212">Las máquinas virtuales que hospedan la lógica de negocios tampoco deben tener ningún estado.</span><span class="sxs-lookup"><span data-stu-id="336ca-212">The VMs hosting the business logic should also be stateless.</span></span>

## <a name="manageability-considerations"></a><span data-ttu-id="336ca-213">Consideraciones sobre la manejabilidad</span><span class="sxs-lookup"><span data-stu-id="336ca-213">Manageability considerations</span></span>

<span data-ttu-id="336ca-214">Simplifique la administración de todo el sistema mediante las herramientas de administración centralizadas, como [Azure Automation][azure-administration], [Microsoft Operations Management Suite] [ operations-management-suite], [Chef][chef] o [Puppet][puppet].</span><span class="sxs-lookup"><span data-stu-id="336ca-214">Simplify management of the entire system by using centralized administration tools such as [Azure Automation][azure-administration], [Microsoft Operations Management Suite][operations-management-suite], [Chef][chef], or [Puppet][puppet].</span></span> <span data-ttu-id="336ca-215">Estas herramientas pueden consolidar la información de diagnóstico y mantenimiento capturada de varias máquinas virtuales para proporcionar una visión general del sistema.</span><span class="sxs-lookup"><span data-stu-id="336ca-215">These tools can consolidate diagnostic and health information captured from multiple VMs to provide an overall view of the system.</span></span>

## <a name="deploy-the-solution"></a><span data-ttu-id="336ca-216">Implementación de la solución</span><span class="sxs-lookup"><span data-stu-id="336ca-216">Deploy the solution</span></span>

<span data-ttu-id="336ca-217">Hay disponible una implementación de esta arquitectura en [GitHub][github-folder].</span><span class="sxs-lookup"><span data-stu-id="336ca-217">A deployment for this architecture is available on [GitHub][github-folder].</span></span> <span data-ttu-id="336ca-218">La arquitectura se implementa en tres fases.</span><span class="sxs-lookup"><span data-stu-id="336ca-218">The architecture is deployed in three stages.</span></span> <span data-ttu-id="336ca-219">Para implementar la arquitectura, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="336ca-219">To deploy the architecture, follow these steps:</span></span> 

1. <span data-ttu-id="336ca-220">Haga clic en el botón a continuación:</span><span class="sxs-lookup"><span data-stu-id="336ca-220">Click the button below:</span></span><br><a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmspnp%2Freference-architectures%2Fmaster%2Fvirtual-machines%2Fn-tier-linux%2Fazuredeploy.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a>
2. <span data-ttu-id="336ca-221">Una vez que el vínculo se abre en Azure Portal, escriba los valores siguientes:</span><span class="sxs-lookup"><span data-stu-id="336ca-221">Once the link has opened in the Azure portal, enter the follow values:</span></span> 
   * <span data-ttu-id="336ca-222">El nombre del **Grupo de recursos** ya está definido en el archivo de parámetros, así que seleccione **Crear nuevo** y escriba `ra-ntier-cassandra-rg` en el cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="336ca-222">The **Resource group** name is already defined in the parameter file, so select **Create New** and enter `ra-ntier-cassandra-rg` in the text box.</span></span>
   * <span data-ttu-id="336ca-223">Seleccione la región en el cuadro de lista desplegable **Ubicación**.</span><span class="sxs-lookup"><span data-stu-id="336ca-223">Select the region from the **Location** drop down box.</span></span>
   * <span data-ttu-id="336ca-224">No modifique los cuadros de texto **URI raíz de plantilla** o **URI raíz de parámetro**.</span><span class="sxs-lookup"><span data-stu-id="336ca-224">Do not edit the **Template Root Uri** or the **Parameter Root Uri** text boxes.</span></span>
   * <span data-ttu-id="336ca-225">Revise los términos y condiciones, y haga clic en la casilla **Acepto los términos y condiciones indicados anteriormente**.</span><span class="sxs-lookup"><span data-stu-id="336ca-225">Review the terms and conditions, then click the **I agree to the terms and conditions stated above** checkbox.</span></span>
   * <span data-ttu-id="336ca-226">Haga clic en el botón **Comprar**.</span><span class="sxs-lookup"><span data-stu-id="336ca-226">Click on the **Purchase** button.</span></span>
3. <span data-ttu-id="336ca-227">Busque una notificación en Azure Portal con un mensaje que indique que la implementación se ha completado.</span><span class="sxs-lookup"><span data-stu-id="336ca-227">Check Azure portal notification for a message the deployment is complete.</span></span>
4. <span data-ttu-id="336ca-228">Los archivos de parámetros incluyen nombres de usuario y contraseñas de administrador codificados de forma rígida, y es muy recomendable que cambie ambos inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="336ca-228">The parameter files include a hard-coded administrator user names and passwords, and it is strongly recommended that you immediately change both on all the VMs.</span></span> <span data-ttu-id="336ca-229">Haga clic en cada máquina virtual en Azure Portal y después en **Restablecer contraseña** en la hoja **Soporte técnico y solución de problemas**.</span><span class="sxs-lookup"><span data-stu-id="336ca-229">Click on each VM in the Azure portal then click on **Reset password** in the **Support + troubleshooting** blade.</span></span> <span data-ttu-id="336ca-230">Seleccione **Restablecer contraseña** en el cuadro de lista desplegable **Modo**, seleccione un **Nombre de usuario** y una **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="336ca-230">Select **Reset password** in the **Mode** dropdown box, then select a new **User name** and **Password**.</span></span> <span data-ttu-id="336ca-231">Haga clic en el botón **Actualizar** para conservar el nuevo nombre de usuario y contraseña.</span><span class="sxs-lookup"><span data-stu-id="336ca-231">Click the **Update** button to persist the new user name and password.</span></span>

<!-- links -->
[multi-dc]: multi-region-application.md
[dmz]: ../dmz/secure-vnet-dmz.md
[multi-vm]: ./multi-vm.md
[naming conventions]: /azure/guidance/guidance-naming-conventions

[azure-administration]: /azure/automation/automation-intro
[azure-availability-sets]: /azure/virtual-machines/virtual-machines-linux-manage-availability
[host bastión]: https://en.wikipedia.org/wiki/Bastion_host
[cassandra-in-azure]: https://docs.datastax.com/en/datastax_enterprise/4.5/datastax_enterprise/install/installAzure.html
[CIDR]: https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing
[chef]: https://www.chef.io/solutions/azure/
[datastax]: http://www.datastax.com/products/datastax-enterprise
[github-folder]: https://github.com/mspnp/reference-architectures/tree/master/virtual-machines/n-tier-linux
[lb-external-create]: /azure/load-balancer/load-balancer-get-started-internet-portal
[lb-internal-create]: /azure/load-balancer/load-balancer-get-started-ilb-arm-portal
[load-balancer-external]: /azure/load-balancer/load-balancer-internet-overview
[load-balancer-internal]: /azure/load-balancer/load-balancer-internal-overview
[nsg]: /azure/virtual-network/virtual-networks-nsg
[nsg-rules]: /azure/azure-resource-manager/best-practices-resource-manager-security#network-security-groups
[operations-management-suite]: https://www.microsoft.com/server-cloud/operations-management-suite/overview.aspx
[plan-network]: /azure/virtual-network/virtual-network-vnet-plan-design-arm
[private-ip-space]: https://en.wikipedia.org/wiki/Private_network#Private_IPv4_address_spaces
[dirección IP pública]: /azure/virtual-network/virtual-network-ip-addresses-overview-arm
[puppet]: https://puppetlabs.com/blog/managing-azure-virtual-machines-puppet
[vm-sla]: https://azure.microsoft.com/support/legal/sla/virtual-machines
[vnet faq]: /azure/virtual-network/virtual-networks-faq
[visio-download]: https://archcenter.azureedge.net/cdn/vm-reference-architectures.vsdx
[Nagios]: https://www.nagios.org/
[Zabbix]: http://www.zabbix.com/
[Icinga]: http://www.icinga.org/
[0]: ./images/n-tier-diagram.png "Arquitectura de n niveles con Microsoft Azure"
