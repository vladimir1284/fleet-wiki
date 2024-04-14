# Rutas y vistas de software de renta

## Control de acceso

### Login
El [estado actual](https://fleet.crabdance.com/signin) de esta vista.

Esta hay que arrglarla para que se vea bien y debe formar parte de la identidad. No podemo usar un referente para esto.

### Código enviado
El [estado actual](https://fleet.crabdance.com/verifyRequest) de esta vista. Esto carga cuando te autenticas con un enlace mágico que te es enviado al correo. Una vez enviado el código te redirecciona a esta vista.

## Dashboard

El [estado actual](https://fleet.crabdance.com/dashboard) de esta vista.
La información que debe mostrarse allí, al menos inicialmente es la [del gestor](https://playground.towithouston.com/erp/). 
![Alt text](./dashboard.jpeg)
Hay que considerar que de lo que se muestra actualmente en el gestor, solo las que se marcan en la siguiente figura importan.

## People
### Clients
Esta es la[ vista actual](http://fleet.crabdance.com/clients). 

Además se puede crear:

![Alt text](./create_client.png)

y editar:

![Alt text](./edit_client.png)


### Users
Esta es la[ vista actual](http://fleet.crabdance.com/users) de los ususrios. Los usuarios son los que pueden ingresar a la plataforma con base a su correo. Por eso, ese es el único dato que se les pide.


Además se puede crear y editar desde un tenant normal:

![Alt text](./Create_user_from_tenant.png)



o desde el tenant admin:

![Alt text](./Create_user_from_admin.png)

En este caso, además del correo y el rol, se necesita especificar el tenant. El tenant admin es para ser usado en la gestión del negocio, es el único que puede crear nuevos tenants y crear usuarios en los mismos.

### Profile
Esta es la[ vista actual](http://fleet.crabdance.com/profile). Los usuarios son responsables de administrar su perfil:

![Alt text](./Profile.png)

Modificar los datos:

![Alt text](./Update_profile.png)

## Tenants

Esta es la[ vista actual](http://fleet.crabdance.com/admin/tenants).  


Además se puede crear:

![Alt text](./create_tenat.png)

y editar:

![Alt text](./update_tenant.png)

En este se puede asignar un dueño al tenant. El dueño tiene priviliegio para crear nuevos ususarios asignados a su tenant.

### Seleccionar tenant
Esto debería hacerse como en odoo:


