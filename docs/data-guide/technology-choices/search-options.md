---
title: Elección de un almacén de datos de búsqueda
description: ''
author: zoinerTejada
ms.date: 02/12/2018
ms.openlocfilehash: b5943cd1410777b974a8cefcd77c7c2f1f2bfe67
ms.sourcegitcommit: e7e0e0282fa93f0063da3b57128ade395a9c1ef9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2018
ms.locfileid: "52902338"
---
# <a name="choosing-a-search-data-store-in-azure"></a>Elección de un almacén de datos de búsqueda en Azure

Este artículo compara las opciones de tecnologías para almacenes de datos de búsqueda de Azure. Un almacén de datos de búsqueda se utiliza para crear y almacenar índices especializados para realizar búsquedas en texto sin formato. El texto que se indexa puede residir en un almacén de datos independiente, como el almacenamiento de blobs. Una aplicación envía una consulta al almacén de datos de búsqueda y el resultado es una lista de documentos coincidentes. Para más información acerca de este escenario, consulte [Procesamiento de texto de formato libre para búsquedas](../scenarios/search.md). 

## <a name="what-are-your-options-when-choosing-a-search-data-store"></a>¿Cuáles son las opciones al elegir un almacén de datos de búsqueda?
En Azure, todos los almacenes de datos siguientes cumplirán los requisitos principales para la búsqueda de datos de texto de formato libre proporcionando un índice de búsqueda:
- [Azure Search](/azure/search/search-what-is-azure-search)
- [Elasticsearch](https://azuremarketplace.microsoft.com/marketplace/apps/elastic.elasticsearch?tab=Overview)
- [HDInsight con Solr](/azure/hdinsight/hdinsight-hadoop-solr-install-linux)
- [Azure SQL Database con búsqueda de texto completo](/sql/relational-databases/search/full-text-search)


## <a name="key-selection-criteria"></a>Principales criterios de selección

En escenarios de búsqueda, puede comenzar por la selección del almacén de datos de búsqueda adecuado para sus necesidades respondiendo a estas preguntas:

- ¿Quiere un servicio administrado en lugar de administrar sus propios servidores?

- ¿Puede especificar el esquema del índice en tiempo de diseño? De lo contrario, elija una opción que admita esquemas actualizables.

- ¿Necesita un índice solo para la búsqueda de texto completo o también necesita agregación de datos numéricos rápida y otros análisis? Si necesita funcionalidad más allá de la búsqueda de texto completo, considere las opciones que admitan análisis adicionales.

- ¿Necesita un índice de búsqueda de análisis de registros, con compatibilidad con la recolección de registros, agregación y visualizaciones de datos indexados? Si es así, considere la posibilidad de Elasticsearch, que forma parte de una pila de análisis de registros.

- ¿Necesita indexar datos en formatos de documento comunes como PDF, Word, PowerPoint y Excel? En caso afirmativo, elija una opción que proporcione indexadores de documentos.

- ¿La base de datos tiene necesidades específicas de seguridad? En caso afirmativo, tenga en cuenta las siguientes características de seguridad.

## <a name="capability-matrix"></a>Matriz de funcionalidades

En las tablas siguientes se resumen las diferencias clave en cuanto a funcionalidades.

### <a name="general-capabilities"></a>Funcionalidades generales

| | Azure Search | Elasticsearch | HDInsight con Solr | SQL Database | 
| --- | --- | --- | --- | --- | 
| Es un servicio administrado | SÍ | Sin  | SÍ | SÍ |  
| API DE REST | SÍ | Sí | SÍ | Sin  |
| Capacidad de programación | .NET | Java | Java | T-SQL | 
| Indexadores de documentos para los tipos de archivo más comunes (PDF, DOCX, TXT y otros) | SÍ | Sin  | Sí | Sin  |

### <a name="manageability-capabilities"></a>Funcionalidades de administración

| | Azure Search | Elasticsearch | HDInsight con Solr | SQL Database | 
| --- | --- | --- | --- | --- |
| Esquema actualizable | Sin  | SÍ | Sí | SÍ |
| Admite el escalado horizontal  | SÍ | Sí | SÍ | Sin  |

### <a name="analytic-workload-capabilities"></a>Funcionalidades de cargas de trabajo de análisis

| | Azure Search | Elasticsearch | HDInsight con Solr | SQL Database | 
| --- | --- | --- | --- | --- | 
| Admite el análisis más allá de la búsqueda de texto completo | Sin  | SÍ | Sí | SÍ |
| Forma parte de una pila de análisis de registros | Sin  | Sí (ELK) |  Sin  | Sin  |
| Admite búsqueda semántica | Sí (solo búsqueda de documentos similares) | SÍ | Sí | SÍ | 

### <a name="security-capabilities"></a>Funcionalidades de seguridad

| | Azure Search | Elasticsearch | HDInsight con Solr | SQL Database | 
| --- | --- | --- | --- | --- | 
| Seguridad de nivel de fila | Parcial (requiere una consulta de la aplicación para filtrar por el identificador de grupo) | Parcial (requiere una consulta de la aplicación para filtrar por el identificador de grupo) | SÍ | SÍ | 
| Cifrado de datos transparente | Sin  | No | No | SÍ |  
| Restricción del acceso a determinadas direcciones IP | Sin  | SÍ | Sí | SÍ |   
| Restricción del acceso para permitir solo el acceso de la red virtual | Sin  | SÍ | Sí | SÍ |  
| Autenticación de Active Directory (autenticación integrada) | Sin  | No | No | SÍ | 

## <a name="see-also"></a>Otras referencias

[Procesamiento de texto de formato libre para búsquedas](../scenarios/search.md)
