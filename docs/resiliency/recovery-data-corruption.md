---
title: "Recuperación de daños o eliminación accidental de los datos"
description: "Artículo para entender cómo recuperarse ante datos dañados o eliminación accidental de datos y para diseñar aplicaciones resistentes, con alta disponibilidad y con tolerancia a errores, así como para planear la recuperación ante desastres"
author: adamglick
ms.date: 08/18/2016
ms.openlocfilehash: b75c774f85c42f64472167897f08a7302ab50a3f
ms.sourcegitcommit: b0482d49aab0526be386837702e7724c61232c60
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/14/2017
---
[!INCLUDE [header](../_includes/header.md)]
# <a name="azure-resiliency-technical-guidance-recovery-from-data-corruption-or-accidental-deletion"></a><span data-ttu-id="058af-103">Guía técnica sobre resistencia en Azure: recuperación de datos dañados o de eliminaciones accidentales</span><span class="sxs-lookup"><span data-stu-id="058af-103">Azure resiliency technical guidance: recovery from data corruption or accidental deletion</span></span>
<span data-ttu-id="058af-104">Una parte de un plan de continuidad empresarial sólido consiste en tener un plan por si los datos resultan dañados o se eliminan accidentalmente.</span><span class="sxs-lookup"><span data-stu-id="058af-104">Part of a robust business continuity plan is having a plan if your data gets corrupted or accidentally deleted.</span></span> <span data-ttu-id="058af-105">A continuación se proporciona información acerca de la recuperación en caso de datos dañados o eliminados accidentalmente debido a errores de la aplicación o a un error del operador.</span><span class="sxs-lookup"><span data-stu-id="058af-105">The following is information about recovery after data has been corrupted or accidentally deleted, due to application errors or operator error.</span></span>

## <a name="virtual-machines"></a><span data-ttu-id="058af-106">Máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="058af-106">Virtual Machines</span></span>
<span data-ttu-id="058af-107">Para proteger Azure Virtual Machines (que a veces se denominan máquinas virtuales de infraestructura como servicio) de errores de las aplicaciones o eliminaciones accidentales, use [Azure Backup](https://azure.microsoft.com/services/backup/).</span><span class="sxs-lookup"><span data-stu-id="058af-107">To protect your Azure Virtual Machines (sometimes called infrastructure-as-a-service VMs) from application errors or accidental deletion, use [Azure Backup](https://azure.microsoft.com/services/backup/).</span></span> <span data-ttu-id="058af-108">Azure Backup permite la creación de copias de seguridad consistentes en varios discos de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="058af-108">Azure Backup enables the creation of backups that are consistent across multiple VM disks.</span></span> <span data-ttu-id="058af-109">Además, el almacén de Backup se puede replicar entre varias regiones para proporcionar recuperación en caso de pérdida de la región.</span><span class="sxs-lookup"><span data-stu-id="058af-109">In addition, the Backup Vault can be replicated across regions to provide recovery from region loss.</span></span>

## <a name="storage"></a><span data-ttu-id="058af-110">Storage</span><span class="sxs-lookup"><span data-stu-id="058af-110">Storage</span></span>
<span data-ttu-id="058af-111">Tenga en cuenta que aunque Azure Storage ofrece resistencia de datos mediante réplicas automatizadas, esto no evita que se puedan dañar los datos del código de la aplicación (ni el de los desarrolladores y usuarios) a causa de una eliminación o actualización accidental o no intencionada.</span><span class="sxs-lookup"><span data-stu-id="058af-111">Note that while Azure Storage provides data resiliency through automated replicas, this does not prevent your application code (or developers/users) from corrupting data through accidental or unintended deletion, update, and so on.</span></span> <span data-ttu-id="058af-112">Mantener la fidelidad de los datos en caso de error de la aplicación o del usuario requiere técnicas más avanzadas, como copiar los datos en una ubicación de almacenamiento secundaria con un registro de auditoría.</span><span class="sxs-lookup"><span data-stu-id="058af-112">Maintaining data fidelity in the face of application or user error requires more advanced techniques, such as copying the data to a secondary storage location with an audit log.</span></span> <span data-ttu-id="058af-113">Los desarrolladores pueden sacar provecho de la [funcionalidad de instantánea](https://msdn.microsoft.com/library/azure/ee691971.aspx)de blobs, que permite crear instantáneas de solo lectura del contenido del blob en un momento dado.</span><span class="sxs-lookup"><span data-stu-id="058af-113">Developers can take advantage of the blob [snapshot capability](https://msdn.microsoft.com/library/azure/ee691971.aspx), which can create read-only point-in-time snapshots of blob contents.</span></span> <span data-ttu-id="058af-114">Esta funcionalidad puede utilizarse como base de una solución de fidelidad de datos para los blobs de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="058af-114">This can be used as the basis of a data-fidelity solution for Azure Storage blobs.</span></span>

### <a name="blob-and-table-storage-backup"></a><span data-ttu-id="058af-115">Copia de seguridad de Blob y Table Storage</span><span class="sxs-lookup"><span data-stu-id="058af-115">Blob and Table Storage Backup</span></span>
<span data-ttu-id="058af-116">Aunque el contenido de los blobs y las tablas es muy duradero, siempre representan el estado actual de los datos.</span><span class="sxs-lookup"><span data-stu-id="058af-116">While blobs and tables are highly durable, they always represent the current state of the data.</span></span> <span data-ttu-id="058af-117">La recuperación ante una modificación o eliminación no deseada puede necesitar la restauración de datos a un estado anterior.</span><span class="sxs-lookup"><span data-stu-id="058af-117">Recovery from unwanted modification or deletion of data may require restoring data to a previous state.</span></span> <span data-ttu-id="058af-118">Esto se puede conseguir aprovechando las funcionalidades proporcionadas por Azure para almacenar y mantener copias de un estado anterior.</span><span class="sxs-lookup"><span data-stu-id="058af-118">This can be achieved by taking advantage of the capabilities provided by Azure to store and retain point-in-time copies.</span></span>

<span data-ttu-id="058af-119">Para Blobs de Azure, puede realizar copias de seguridad de un estado anterior mediante la [característica de instantáneas de blob](https://msdn.microsoft.com/library/ee691971.aspx).</span><span class="sxs-lookup"><span data-stu-id="058af-119">For Azure Blobs, you can perform point-in-time backups using the [blob snapshot feature](https://msdn.microsoft.com/library/ee691971.aspx).</span></span> <span data-ttu-id="058af-120">Por cada instantánea, solo se le cobrará por el almacenamiento que necesite para almacenar las diferencias producidas en el blob desde el último estado de instantánea.</span><span class="sxs-lookup"><span data-stu-id="058af-120">For each snapshot, you are only charged for the storage required to store the differences within the blob since the last snapshot state.</span></span> <span data-ttu-id="058af-121">Las instantáneas dependen de la existencia del blob original en el que se basan, por lo que se recomienda realizar una operación de copia a otro blob, o incluso a otra cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="058af-121">The snapshots are dependent on the existence of the original blob they are based on, so a copy operation to another blob or even another storage account is advisable.</span></span> <span data-ttu-id="058af-122">Esto garantiza que los datos de copia de seguridad que los datos de la copia de seguridad estén protegidos correctamente contra la eliminación accidental.</span><span class="sxs-lookup"><span data-stu-id="058af-122">This ensures that backup data is properly protected against accidental deletion.</span></span> <span data-ttu-id="058af-123">Para las tablas de Azure, puede realizar copias de un estado anterior en una tabla diferente o en los Blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="058af-123">For Azure Tables, you can make point-in-time copies to a different table or to Azure Blobs.</span></span> <span data-ttu-id="058af-124">Puede consultar una guía más detallada y ejemplos de cómo realizar copias de seguridad de tablas y blobs en el nivel de aplicación, aquí:</span><span class="sxs-lookup"><span data-stu-id="058af-124">More detailed guidance and examples of performing application-level backups of tables and blobs can be found here:</span></span>

* [<span data-ttu-id="058af-125">Protecting Your Tables Against Application Errors</span><span class="sxs-lookup"><span data-stu-id="058af-125">Protecting Your Tables Against Application Errors</span></span>](https://blogs.msdn.microsoft.com/windowsazurestorage/2010/05/03/protecting-your-tables-against-application-errors/)
* [<span data-ttu-id="058af-126">Protecting Your Blobs Against Application Errors</span><span class="sxs-lookup"><span data-stu-id="058af-126">Protecting Your Blobs Against Application Errors</span></span>](https://blogs.msdn.microsoft.com/windowsazurestorage/2010/04/29/protecting-your-blobs-against-application-errors/)

## <a name="database"></a><span data-ttu-id="058af-127">Base de datos</span><span class="sxs-lookup"><span data-stu-id="058af-127">Database</span></span>
<span data-ttu-id="058af-128">Hay varias opciones de [continuidad empresarial](/azure/sql-database/sql-database-business-continuity/) (copia de seguridad, restauración) disponibles para Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="058af-128">There are several [business continuity](/azure/sql-database/sql-database-business-continuity/) (backup, restore) options available for Azure SQL Database.</span></span> <span data-ttu-id="058af-129">Las bases de datos se pueden copiar mediante la funcionalidad de [copia de base de datos](/azure/sql-database/sql-database-copy/) o mediante la [exportación](/azure/sql-database/sql-database-export/) e [importación](https://msdn.microsoft.com/library/hh710052.aspx) de un archivo bacpac de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="058af-129">Databases can be copied by using the [Database Copy](/azure/sql-database/sql-database-copy/) functionality, or by  [exporting](/azure/sql-database/sql-database-export/) and [importing](https://msdn.microsoft.com/library/hh710052.aspx) a SQL Server bacpac file.</span></span> <span data-ttu-id="058af-130">Esta funcionalidad proporciona resultados transaccionales coherentes, cosa que no sucede en el caso de un archivo bacpac (a través del servicio de importación y exportación).</span><span class="sxs-lookup"><span data-stu-id="058af-130">Database Copy provides transactionally consistent results, while a bacpac (through the import/export service) does not.</span></span> <span data-ttu-id="058af-131">Ambas opciones se ejecutan como servicios basados en cola en el centro de datos y no proporcionan actualmente un Acuerdo de Nivel de Servicio con tiempo de finalización.</span><span class="sxs-lookup"><span data-stu-id="058af-131">Both of these options run as queue-based services within the data center, and they do not currently provide a time-to-completion SLA.</span></span>

> [!NOTE]
> <span data-ttu-id="058af-132">Las opciones de copia de base de datos e importación y exportación colocan un nivel significativo de carga en la base de datos de origen,</span><span class="sxs-lookup"><span data-stu-id="058af-132">The database copy and import/export options place a significant degree of load on the source database.</span></span> <span data-ttu-id="058af-133">lo que puede desencadenar eventos de contención o limitación de recursos.</span><span class="sxs-lookup"><span data-stu-id="058af-133">They can trigger resource contention or throttling events.</span></span>
> 
> 

### <a name="sql-database-backup"></a><span data-ttu-id="058af-134">Copia de seguridad de SQL Database</span><span class="sxs-lookup"><span data-stu-id="058af-134">SQL Database Backup</span></span>
<span data-ttu-id="058af-135">Las copias de seguridad de un estado anterior de Microsoft Azure SQL Database se consiguen mediante [la copia de Azure SQL Database](/azure/sql-database/sql-database-copy/).</span><span class="sxs-lookup"><span data-stu-id="058af-135">Point-in-time backups for Microsoft Azure SQL Database are achieved by [copying your Azure SQL database](/azure/sql-database/sql-database-copy/).</span></span> <span data-ttu-id="058af-136">Este comando se puede usar para crear una copia transaccionalmente coherente de una base de datos en el mismo servidor de bases de datos lógicas o en otro.</span><span class="sxs-lookup"><span data-stu-id="058af-136">You can use this command to create a transactionally consistent copy of a database on the same logical database server or to a different server.</span></span> <span data-ttu-id="058af-137">En cualquier caso, la copia de la base de datos es totalmente funcional y completamente independiente de la base de datos de origen.</span><span class="sxs-lookup"><span data-stu-id="058af-137">In either case, the database copy is fully functional and completely independent of the source database.</span></span> <span data-ttu-id="058af-138">Cada copia que cree representa una opción de recuperación de un estado anterior.</span><span class="sxs-lookup"><span data-stu-id="058af-138">Each copy you create represents a point-in-time recovery option.</span></span> <span data-ttu-id="058af-139">Puede recuperar completamente el estado de la base de datos cambiando el nombre de la nueva base de datos con el nombre de la base de datos de origen.</span><span class="sxs-lookup"><span data-stu-id="058af-139">You can recover the database state completely by renaming the new database with the source database name.</span></span> <span data-ttu-id="058af-140">De forma alternativa, puede recuperar un subconjunto específico de datos de la nueva base de datos mediante consultas de Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="058af-140">Alternatively, you can recover a specific subset of data from the new database by using Transact-SQL queries.</span></span> <span data-ttu-id="058af-141">Para obtener más información sobre SQL Database, consulte [Introducción a la continuidad empresarial con Azure SQL Database](/azure/sql-database/sql-database-business-continuity/).</span><span class="sxs-lookup"><span data-stu-id="058af-141">For additional details about SQL Database, see [Overview of business continuity with Azure SQL Database](/azure/sql-database/sql-database-business-continuity/).</span></span>

### <a name="sql-server-on-virtual-machines-backup"></a><span data-ttu-id="058af-142">SQL Server en la copia de seguridad de Máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="058af-142">SQL Server on Virtual Machines Backup</span></span>
<span data-ttu-id="058af-143">En los casos en que SQL Server se utiliza con la infraestructura de Azure como máquinas virtuales de servicio (a menudo denominadas IaaS o máquinas virtuales de IaaS), hay dos opciones: las copias de seguridad tradicionales y el trasvase de registros.</span><span class="sxs-lookup"><span data-stu-id="058af-143">For SQL Server used with Azure infrastructure as a service virtual machines (often called IaaS or IaaS VMs), there are two options: traditional backups and log shipping.</span></span> <span data-ttu-id="058af-144">El uso de copias de seguridad tradicionales le permite restaurar a un estado anterior específico, pero el proceso de recuperación es lento.</span><span class="sxs-lookup"><span data-stu-id="058af-144">Using traditional backups enables you to restore to a specific point in time, but the recovery process is slow.</span></span> <span data-ttu-id="058af-145">La restauración de copias de seguridad tradicionales requiere empezar con una copia de seguridad completa inicial y, a continuación, aplicar las copias de seguridad realizadas después de ella.</span><span class="sxs-lookup"><span data-stu-id="058af-145">Restoring traditional backups requires starting with an initial full backup, and then applying any backups taken after that.</span></span> <span data-ttu-id="058af-146">La segunda opción es configurar una sesión de trasvase de registros para retrasar la restauración de las copias de seguridad del registro (por ejemplo, en dos horas).</span><span class="sxs-lookup"><span data-stu-id="058af-146">The second option is to configure a log shipping session to delay the restore of log backups (for example, by two hours).</span></span> <span data-ttu-id="058af-147">Esto proporciona un tiempo para recuperarse de los errores que se produzcan en el servidor principal.</span><span class="sxs-lookup"><span data-stu-id="058af-147">This provides a window to recover from errors made on the primary.</span></span>

## <a name="other-azure-platform-services"></a><span data-ttu-id="058af-148">Otros servicios de la plataforma de Azure</span><span class="sxs-lookup"><span data-stu-id="058af-148">Other Azure platform services</span></span>
<span data-ttu-id="058af-149">Algunos servicios de la plataforma de Azure almacenan información en una cuenta de almacenamiento controlada por el usuario o en Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="058af-149">Some Azure platform services store information in a user-controlled storage account or Azure SQL Database.</span></span> <span data-ttu-id="058af-150">Si el recurso de almacenamiento o la cuenta se eliminan o se dañan, esto podría provocar errores graves con el servicio.</span><span class="sxs-lookup"><span data-stu-id="058af-150">If the account or storage resource is deleted or corrupted, this could cause serious errors with the service.</span></span> <span data-ttu-id="058af-151">En estos casos, es importante mantener copias de seguridad que le permitan volver a crear los recursos si estos se han eliminado o dañado.</span><span class="sxs-lookup"><span data-stu-id="058af-151">In these cases, it is important to maintain backups that would enable you to re-create these resources if they were deleted or corrupted.</span></span>

<span data-ttu-id="058af-152">Para los Sitios web y Azure Mobile Services, debe realizar la copia de seguridad y mantener las bases de datos asociadas.</span><span class="sxs-lookup"><span data-stu-id="058af-152">For Azure Web Sites and Azure Mobile Services, you must backup and maintain the associated databases.</span></span> <span data-ttu-id="058af-153">Para los servicios multimedia y Azure Virtual Machines, debe mantener la cuenta de Azure Storage asociada y todos los recursos de esa cuenta.</span><span class="sxs-lookup"><span data-stu-id="058af-153">For Azure Media Service and Virtual Machines, you must maintain the associated Azure Storage account and all resources in that account.</span></span> <span data-ttu-id="058af-154">Por ejemplo, en el caso de Máquinas virtuales, debe realizar la copia de seguridad y administrar los discos de las máquinas virtuales en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="058af-154">For example, for Virtual Machines, you must back up and manage the VM disks in Azure blob storage.</span></span>

## <a name="checklists-for-data-corruption-or-accidental-deletion"></a><span data-ttu-id="058af-155">Listas de comprobación de datos dañados o eliminados accidentalmente</span><span class="sxs-lookup"><span data-stu-id="058af-155">Checklists for data corruption or accidental deletion</span></span>
## <a name="virtual-machines-checklist"></a><span data-ttu-id="058af-156">Lista de comprobación de Máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="058af-156">Virtual Machines checklist</span></span>
1. <span data-ttu-id="058af-157">Revise la sección Máquinas virtuales de este documento.</span><span class="sxs-lookup"><span data-stu-id="058af-157">Review the Virtual Machines section of this document.</span></span>
2. <span data-ttu-id="058af-158">Realice una copia de seguridad y mantenga los discos de las máquinas virtuales mediante Azure Backup (o a través de su propio sistema de copias de seguridad mediante Azure Blob Storage y las instantáneas de disco duro virtual).</span><span class="sxs-lookup"><span data-stu-id="058af-158">Back up and maintain the VM disks with Azure Backup (or your own backup system by using Azure blob storage and VHD snapshots).</span></span>

## <a name="storage-checklist"></a><span data-ttu-id="058af-159">Lista de comprobación de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="058af-159">Storage checklist</span></span>
1. <span data-ttu-id="058af-160">Revise la sección Almacenamiento de este documento.</span><span class="sxs-lookup"><span data-stu-id="058af-160">Review the Storage section of this document.</span></span>
2. <span data-ttu-id="058af-161">Realice copias de seguridad de recursos de almacenamiento críticos de forma regular.</span><span class="sxs-lookup"><span data-stu-id="058af-161">Regularly back up critical storage resources.</span></span>
3. <span data-ttu-id="058af-162">Considere el uso de la característica de instantáneas de blobs.</span><span class="sxs-lookup"><span data-stu-id="058af-162">Consider using the snapshot feature for blobs.</span></span>

## <a name="database-checklist"></a><span data-ttu-id="058af-163">Lista de comprobación de base de datos</span><span class="sxs-lookup"><span data-stu-id="058af-163">Database checklist</span></span>
1. <span data-ttu-id="058af-164">Revise la sección Base de datos de este documento.</span><span class="sxs-lookup"><span data-stu-id="058af-164">Review the Database section of this document.</span></span>
2. <span data-ttu-id="058af-165">Cree copias de seguridad en un momento dado mediante el comando Database Copy.</span><span class="sxs-lookup"><span data-stu-id="058af-165">Create point-in-time backups by using the Database Copy command.</span></span>

## <a name="sql-server-on-virtual-machines-backup-checklist"></a><span data-ttu-id="058af-166">Lista de comprobación de SQL Server en la copia de seguridad de Máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="058af-166">SQL Server on Virtual Machines Backup checklist</span></span>
1. <span data-ttu-id="058af-167">Consulte la sección SQL Server en la copia de seguridad de Máquinas virtuales de este documento.</span><span class="sxs-lookup"><span data-stu-id="058af-167">Review the SQL Server on Virtual Machines Backup section of this document.</span></span>
2. <span data-ttu-id="058af-168">Use técnicas tradicionales de copia de seguridad y restauración.</span><span class="sxs-lookup"><span data-stu-id="058af-168">Use traditional backup and restore techniques.</span></span>
3. <span data-ttu-id="058af-169">Cree una sesión de trasvase de registros con retraso.</span><span class="sxs-lookup"><span data-stu-id="058af-169">Create a delayed log shipping session.</span></span>

## <a name="web-apps-checklist"></a><span data-ttu-id="058af-170">Lista de comprobación de Web Apps</span><span class="sxs-lookup"><span data-stu-id="058af-170">Web Apps checklist</span></span>
1. <span data-ttu-id="058af-171">Realice una copia de seguridad y mantenga la base de datos asociada, si hay alguna.</span><span class="sxs-lookup"><span data-stu-id="058af-171">Back up and maintain the associated database, if any.</span></span>

## <a name="media-services-checklist"></a><span data-ttu-id="058af-172">Lista de comprobación de Media Services</span><span class="sxs-lookup"><span data-stu-id="058af-172">Media Services checklist</span></span>
1. <span data-ttu-id="058af-173">Realice una copia de seguridad y mantenga los recursos de almacenamiento asociados.</span><span class="sxs-lookup"><span data-stu-id="058af-173">Back up and maintain the associated storage resources.</span></span>

## <a name="more-information"></a><span data-ttu-id="058af-174">Más información</span><span class="sxs-lookup"><span data-stu-id="058af-174">More information</span></span>
<span data-ttu-id="058af-175">Para obtener más información acerca de las características de copia de seguridad y restauración de Azure, consulte [Copia de seguridad y archivado](https://azure.microsoft.com/documentation/scenarios/storage-backup-recovery/).</span><span class="sxs-lookup"><span data-stu-id="058af-175">For more information about backup and restore features in Azure, see [Storage, backup and recovery scenarios](https://azure.microsoft.com/documentation/scenarios/storage-backup-recovery/).</span></span>

