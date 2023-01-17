

# LAB 01 - Manage Azure Active Directory Identities

Enero 17 de 2023*, Ramón Peinado Ruiz

Este laboratorio requiere permisos para crear usuarios de Azure Active Directory (Azure AD), crear roles personalizados de Azure Role Based Access Control (RBAC) y asignar estos roles a usuarios de Azure AD.

**Objetivos:**

------

• Task 1: Implementar Grupos de Administracion

• Task 2: Crear roles customizados RBAC

• Task 3: Asignar roles RBAC

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



"AssignableScopes": [

​    "/providers/Microsoft.Management/managementGroups/az104-02-mg1",

​    "/subscriptions/***5097fbdf-333c-428b-821a-e6802b29f570"***





Subimos nuestro archivo .json a azure via powershell

<img src="/img/9ºimagenn.png" alt="9ºimagenn" style="zoom:80%;" />

Y ejecutamos el siguiente comando:

***New-AzRoleDefinition -InputFile $HOME/az104-02a-customRoleDefinition.json***

<img src="/img/5ºimagenn.png" alt="5ºimagenn" style="zoom:80%;" />

### TASK 3:

------

***AD>Users>New User***

Creamos un nuevo usuario

| Settings                   | Value                         |
| -------------------------- | ----------------------------- |
| User name                  | **az104-02-aaduser1**         |
| Name                       | **az104-02-aaduser1**         |
| Let me create the password | enabled                       |
| Initial password           | **Provide a secure password** |

Copiamos el nombre junto con el dominio ya que posteriormente nos hara falta

az104-02-aaduser1@ramonperuoutlook.onmicrosoft.com

***Grupos de Administracion>az104-02-mg1> IAM(Control Acceso)>+Add***



Añadimos el rol custom que insertamos anteriormente via powershell dentro de nuestro grupo de administracion y ademas seleccionamos como miembro el ultimo usuario creado.



Comprobamos las limitaciones.



