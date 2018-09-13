---
title: 'Adopción de la nube empresarial: Diseño de gobierno para una carga de trabajo simple'
description: Instrucciones para configurar los controles de gobierno de Azure para que un usuario pueda implementar una carga de trabajo simple
author: petertaylor9999
ms.date: 09/10/2018
ms.openlocfilehash: 13c7c4b41df14151d28b9c685f01019af3ec63f2
ms.sourcegitcommit: c49aeef818d7dfe271bc4128b230cfc676f05230
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/11/2018
ms.locfileid: "44389254"
---
# <a name="enterprise-cloud-adoption-governance-design-for-a-simple-workload"></a>Adopción de la nube empresarial: Diseño de gobierno para una carga de trabajo simple

El objetivo de esta guía es ayudarle a obtener información sobre el proceso para diseñar un modelo de gobierno de recursos en Azure que admita un único equipo y una carga de trabajo simple.  Veremos un conjunto de requisitos de gobierno hipotéticos y, después, describiremos varias implementaciones de ejemplo que cumplen dichos requisitos. 

En la fase de adopción de fundación, nuestro objetivo es implementar una carga de trabajo simple en Azure. El resultado son los siguientes requisitos:
* Administración de identidades para un solo **propietario de cargas de trabajo**, que es responsable de implementar y mantener la carga de trabajo simple. El propietario de la carga de trabajo necesita permisos para crear, leer, actualizar y eliminar recursos, así como permisos para delegar estos derechos a otros usuarios en el sistema de administración de identidades.
* Administrar todos los recursos para la carga de trabajo simple como una unidad única de administración.

## <a name="licensing-azure"></a>Licencias de Azure

Antes de comenzar el diseño de nuestro modelo de gobierno, es importante comprender cómo se conceden las licencias de Azure. El motivo es que las cuentas administrativas asociadas con su licencia de Azure tienen el mayor nivel de acceso a todos los recursos de Azure. Estas cuentas administrativas forman la base de su modelo de gobierno.  

> [!NOTE]
> Si su organización ya tiene un [Contrato Enterprise de Microsoft](https://www.microsoft.com/en-us/licensing/licensing-programs/enterprise.aspx) que no incluye Azure, se puede agregar Azure mediante un compromiso monetario por adelantado. Consulte las [licencias de Azure para la empresa](https://azure.microsoft.com/pricing/enterprise-agreement/) para más información. 

Cuando Azure se agregó al contrato Enterprise de su organización, se solicitó a su organización la creación de una **cuenta de Azure**. Durante el proceso de creación de la cuenta, se crea un **propietario de la cuenta de Azure** y un inquilino de Azure Active Directory (Azure AD) con una cuenta de **administrador global**. Un inquilino de Azure AD es una construcción lógica que representa una instancia segura y dedicada de Azure AD.

![Cuenta de Azure con el Administrador de cuentas de Azure y el administrador global de Azure AD](../_images/governance-3-0.png)
*Figura 1. Cuenta de Azure con el Administrador de cuentas de Azure y el administrador global de Azure AD.*

## <a name="identity-management"></a>Administración de identidades

Azure solo confía en [Azure AD](/azure/active-directory) para autenticar usuarios y autorizar el acceso de los usuarios a los recursos, por lo que Azure AD es nuestro sistema de administración de identidades. El administrador global de Azure AD tiene el mayor nivel de permisos y puede realizar todas las acciones relacionadas con la identidad, incluida la creación de usuarios y asignación de permisos. 

Nuestro requisito es una administración de identidades para un solo **propietario de cargas de trabajo**, que es responsable de implementar y mantener la carga de trabajo simple. El propietario de la carga de trabajo necesita permisos para crear, leer, actualizar y eliminar recursos, así como permisos para delegar estos derechos a otros usuarios en el sistema de administración de identidades.

Nuestro administrador global de Azure AD creará la cuenta de **propietario de carga de trabajo** para el **propietario de la carga de trabajo**:

![El administrador global de Azure AD crea la cuenta del propietario de carga de trabajo](../_images/governance-1-2.png)
*Figura 2. El administrador global de Azure AD crea la cuenta de usuario del propietario de carga de trabajo.*

No podemos asignar permiso de acceso a los recursos hasta que este usuario se agregue a una **suscripción**, lo que haremos en las dos secciones siguientes. 

## <a name="resource-management-scope"></a>Ámbito de la administración de recursos

A medida que crece el número de los recursos implementados por la organización, aumenta también la complejidad del gobierno de estos recursos. Azure implementa una jerarquía de contenedores lógicos para que su organización pueda administrar los recursos en grupos con distintos niveles de granularidad, lo que también se conoce como **ámbito**. 

El nivel superior del ámbito de administración de recursos es el nivel de **suscripción**. El **propietario de la cuenta** de Azure crea una suscripción, que establece el compromiso financiero y es responsable del pago de todos los recursos de Azure asociados con la suscripción:

![El propietario de la cuenta de Azure crea una suscripción](../_images/governance-1-3.png)
*Figura 3. El propietario de la cuenta de Azure crea una suscripción.*

Cuando se crea la suscripción, el **propietario de la cuenta** de Azure asocia un inquilino de Azure AD con la suscripción, y este inquilino de Azure AD se usa para autenticar y autorizar a los usuarios:

![El propietario de la cuenta de Azure asocia el inquilino de Azure AD con la suscripción](../_images/governance-1-4.png)
*Figura 4. El propietario de la cuenta de Azure asocia el inquilino de Azure AD con la suscripción.*

Puede que haya observado que actualmente no hay ningún usuario asociado con la suscripción, lo que significa que nadie tiene permiso para administrar los recursos. En realidad, el **propietario de la cuenta** es el propietario de la suscripción y tiene permiso para realizar cualquier acción en un recurso en la suscripción. Sin embargo, en la práctica, es muy probable que el **propietario de la cuenta** sea una persona de finanzas de su organización y no el responsable de crear, leer, actualizar y eliminar los recursos. Esas tareas las realizará el **propietario de la carga de trabajo**. Por lo tanto, tenemos que agregar el **propietario de la carga de trabajo** a la suscripción y asignar los permisos.

El **propietario de la cuenta** es actualmente el único usuario con permiso para agregar el **propietario de la carga de trabajo** a la suscripción, por lo que agrega el **propietario de la carga de trabajo** a la suscripción:

![El propietario de la cuenta de Azure agrega el **propietario de la carga de trabajo** a la suscripción](../_images/governance-1-5.png)
*Figura 5. El propietario de la cuenta de Azure agrega el propietario de la carga de trabajo a la suscripción.*

El **propietario de la cuenta** de Azure concede permisos al **propietario de la carga de trabajo** y, para ello, lo asigna a un rol de [control de acceso basado en rol (RBAC)](/azure/role-based-access-control/). El rol de RBAC especifica el conjunto de permisos que el **propietario de la carga de trabajo** tiene para un tipo de recurso individual o para un conjunto de tipos de recursos.

Tenga en cuenta que, en este ejemplo, el **propietario de la cuenta** ha asignado el rol [integrado **propietario**](/azure/role-based-access-control/built-in-roles#owner): 

![Se asignó el rol integrado propietario al **propietario de la carga de trabajo**](../_images/governance-1-6.png)
*Figura 6. Se asignó el rol integrado propietario al propietario de la carga de trabajo.*

El rol integrado **propietario** concede todos los permisos al **propietario de la carga de trabajo** en el ámbito de la suscripción. 

> [!IMPORTANT]
> El **propietario de la cuenta** de Azure es responsable del compromiso financiero asociado con la suscripción, pero el **propietario de la carga de trabajo** tiene los mismos permisos. El **propietario de la cuenta** debe confiar en el **propietario de la carga de trabajo** para implementar los recursos que están dentro del presupuesto de suscripción.

El siguiente nivel del ámbito de administración es el nivel **grupo de recursos**. Un grupo de recursos es un contenedor lógico de recursos. Las operaciones que se aplican en el nivel de grupo de recursos se aplican a todos los recursos de un grupo. Además, es importante tener en cuenta que los permisos de cada usuario se heredan de los permisos del siguiente nivel superior, a menos que se cambien explícitamente en ese ámbito. 

Para ilustrar esto, veamos lo que sucede cuando el **propietario de la carga de trabajo** crea un grupo de recursos:

![El **propietario de la carga de trabajo** crea un grupo de recursos](../_images/governance-1-7.png)
*Figura 7. El propietario de la carga de trabajo crea un grupo de recursos y hereda el rol integrado propietario en el ámbito del grupo de recursos.*

De nuevo, el rol integrado **propietario** concede todos los permisos al **propietario de la carga de trabajo** en el ámbito del grupo de recursos. Como se explicó anteriormente, este rol se hereda del nivel de suscripción. Si se asigna un rol diferente a este usuario en este ámbito, se aplica solo a este ámbito.

El nivel del ámbito de administración más bajo es el nivel **recurso**. Las operaciones que se aplican en el nivel de recursos se aplican solo al recurso en sí. Y, de nuevo, los permisos del nivel de recurso se heredan del ámbito del grupo de recursos. Por ejemplo, veamos lo que sucede si el **propietario de la carga de trabajo** implementa una [red virtual](/azure/virtual-network/virtual-networks-overview) en el grupo de recursos:

![El **propietario de la carga de trabajo** crea un recurso](../_images/governance-1-8.png)
*Figura 8. El propietario de la carga de trabajo crea un recurso y hereda el rol integrado propietario en el ámbito del recurso.*

El **propietario de la carga de trabajo** hereda el rol de propietario en el ámbito del recurso, lo que significa que el propietario de la carga de trabajo tiene todos los permisos para la red virtual.

## <a name="implementing-the-basic-resource-access-management-model"></a>Implementación del modelo de administración de acceso a los recursos básico

Vamos a aprender a implementar el modelo de gobierno diseñado anteriormente. 

Para empezar, la organización necesita una cuenta de Azure. Si su organización ya tiene un [Contrato Enterprise de Microsoft](https://www.microsoft.com/licensing/licensing-programs/enterprise.aspx) que no incluye Azure, se puede agregar Azure mediante un compromiso monetario por adelantado. Consulte las [licencias de Azure para la empresa](https://azure.microsoft.com/pricing/enterprise-agreement/) para más información. 

Cuando cree la cuenta de Azure, especifique el usuario de su organización que será el **propietario de la cuenta** de Azure. Después, se crea un inquilino de Azure Active Directory (Azure AD) de forma predeterminada. El **propietario de la cuenta** de Azure debe [crear la cuenta de usuario](/azure/active-directory/add-users-azure-active-directory) para el usuario de la organización que sea el **propietario de cargas de trabajo**. 

A continuación, el **propietario de la cuenta** de Azure debe [crear una suscripción](https://docs.microsoft.com/partner-center/create-a-new-subscription) y [asociar el inquilino de Azure AD](/azure/active-directory/fundamentals/active-directory-how-subscriptions-associated-directory) a ella.

Por último, con la suscripción creada y el inquilino de Azure AD asociado a ella, puede [agregar el **propietario de cargas de trabajo** a la suscripción con el rol integrado **propietario**](/azure/billing/billing-add-change-azure-subscription-administrator#add-an-rbac-owner-for-a-subscription-in-azure-portal).

## <a name="next-steps"></a>Pasos siguientes
> [!div class="nextstepaction"]
> [Implementación de una carga de trabajo básica en Azure](../infrastructure/basic-workload.md)
> [!div class="nextstepaction"]
> [Obtenga información sobre el acceso a los recursos para varios equipos](governance-multiple-teams.md)
