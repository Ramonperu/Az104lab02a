

# LAB 01 - Manage Azure Active Directory Identities

Enero 17 de 2023*, Ramón Peinado Ruiz

Este laboratorio requiere permisos para crear usuarios de Azure Active Directory (Azure AD), crear roles personalizados de Azure Role Based Access Control (RBAC) y asignar estos roles a usuarios de Azure AD.

**Objetivos:**

------

• Task 1: Implementar Grupos de Administracion

• Task 2: Crear roles customizados RBAC

• Task 3: Asignar roles RBAC

• Task 4: Eliminacion de recursos

**Diagrama:**

------

<img src="/img/6ºimagenn.png" alt="6ºimagenn" style="zoom:80%;" />

### TASK 1:

------

***Home>Buscar>Management Groups***

<img src="/img/1ºimagenn.png" alt="1ºimagenn" style="zoom:80%;" />

No podemos crear grupos todavia, hemos de activar los permisos dento del directiorio activo

***Azure AD>manage>propierties > acces management -> yes***

<img src="/img/2ºimagenn.png" alt="2ºimagenn" style="zoom:80%;" />

Depues de activar esta opcion creamo el grupo de administracion

| Settings                      | Value            |
| ----------------------------- | ---------------- |
| Management group ID           | **az104-02-mg1** |
| Management group display name | **az104-02-mg1** |

Una vez creado el grupo entramos y añadimos subscripcion

<img src="/img/3ºimagenn.png" alt="2ºimagenn" style="zoom:80%;" />



<img src="/img/7ºimagenn.png" alt="7ºimagenn" style="zoom:80%;" />

Hemos de guardar el id de subscripcion:

5097fbdf-333c-428b-821a-e6802b29f570



### TASK 2:

------



El profesor nos ha facilitado este archivo json

<img src="/img/8ºimagenn.png" alt="8ºimagenn" style="zoom:80%;" />Del cual hemos modificado el alcance poniendo el suscription ID al final de:



*"AssignableScopes": [*

​    *"/providers/Microsoft.Management/managementGroups/az104-02-mg1",*

​    *"/subscriptions/**5097fbdf-333c-428b-821a-e6802b29f570"***



**Opcionalmente podriamos cambiar el nombre a nuestro gusto.



Subimos nuestro archivo .json a azure via powershell

<img src="/img/9ºimagenn.png" alt="9ºimagenn" style="zoom:80%;" />

Y ejecutamos el siguiente comando:

***New-AzRoleDefinition -InputFile $HOME/az104-02a-customRoleDefinition.json***

<img src="/img/5ºimagenn.png" alt="5ºimagenn" style="zoom:80%;" />

### TASK 3:

------

***Home>Azure AD>Users>New User***

Creamos un nuevo usuario

| Settings                   | Value                         |
| -------------------------- | ----------------------------- |
| User name                  | **az104-02-aaduser1**         |
| Name                       | **az104-02-aaduser1**         |
| Let me create the password | enabled                       |
| Initial password           | **Provide a secure password** |

Copiamos el nombre junto con el dominio ya que posteriormente nos hara falta

az104-02-aaduser1@ramonperuoutlook.onmicrosoft.com

<img src="/img/10ºimagenn.png" alt="10ºimagenn" style="zoom:80%;" />

***Grupos de Administracion>az104-02-mg1> IAM(Control Acceso)>+Add***

<img src="/img/11ºimagenn.png" alt="11ºimagenn" style="zoom:80%;" />

Añadimos el rol custom que insertamos anteriormente via powershell dentro de nuestro grupo de administracion y ademas seleccionamos como miembro el ultimo usuario creado.

<img src="/img/13ºimagenn.png" alt="13ºimagenn" style="zoom:80%;" />

Comprobamos las limitaciones.

Dentro de una ventana en incognito accedemos con el nuevo usuario, podra ver los **grupos de recursos**

<img src="/img/15ºimagenn.png" alt="15ºimagenn" style="zoom:80%;" />

No podra ver nada dentro de la pestaña **Todos los recursos**

<img src="/img/16ºimagenn.png" alt="16ºimagenn" style="zoom:80%;" />

Creacion de la solicitud de soporte y ayuda

<img src="/img/17ºimagenn.png" alt="17ºimagenn" style="zoom:80%;" />

### TASK 4:

------

Azure AD> Users>Profile

Copiamos Object ID y abrimos PowerShell para ejecutar el siguiente comando

Object ID: 6cfd1aab-d43b-4f99-8f4b-ac70594bb9db

​    ***$scope = (Get-AzRoleDefinition -Name 'Support Request Contributor (Custom)').AssignableScopes | Where-Object {$_ -like 'managementgroup'}     Remove-AzRoleAssignment -ObjectId '[object_ID]' -RoleDefinitionName 'Support Request Contributor (Custom)' -Scope $scope***

Donde sustituimos [objet_ID] por nuestro numero recien copiado

Despues ejecutamos el comando para borrar el rol:

***Remove-AzRoleDefinition -Name 'Support Request Contributor (Custom)' -Force***

Borramos el usuario desde Azure AD>Users

Por ultimo vamos a Administracion de grupos y reasociamos nuestra suscripcion al tenant root 

***Home>Management Groups>Tenant Root Group> Add Subscription***

<img src="/img/18ºimagenn.png" alt="18ºimagenn" style="zoom:80%;" />

Para borrar por ultimo el grupo de administracion que creamos al principio

<img src="/img/19ºimagenn.png" alt="18ºimagenn" style="zoom:80%;" />
