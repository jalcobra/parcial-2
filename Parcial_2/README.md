
Para realizar las prácticas se debe tener instalado en el equipo o servidor de pruebas:
  - Docker
  - Python

##  Se instala  Ansible 

        pip install ansible

## Construcción de la imagen personalizada
Ingresa a la carpeta ```Dockerfile``` y sigue los pasos que dicen allí.



Documentación: 

En acuerdo a como se solicitó en la actividad de migrar los servidores de Redhat/CentOS a Ubuntu server, se plantearon las siguientes dudas.
## ¿Cómo crear los contenedores de Docker? 
Para poder crear los contenedores se optó por hacer un ```Dockerfile```, para crear la imagen que es la que nos permitirá hacer los contenedores y un archivo llamado ```authorized_keys```.

## ¿Cómo se realiza la migración del servidor mediante Ansible? 
En la actividad se plantearon 2 servicios los cuales se tenían que migrar que son ```web_server``` y ```mysql_server```
lo que debiamos hacer en estos 2 servicios era buscar dentro de los ```Modulos de Ansible``` el equivalente de ```Redhat/CentOS``` a ```Ubuntu server``` y aplicarlos en cada uno de ellos.

Por ejemplo los Modulos ```yum``` de Redhat/CentOS que su equivalente es el ```apt``` en Ubuntu server.






Esta stack LAMP puede estar en un solo nodo o en varios nodos. El archivo de inventario
'hosts' define los nodos en los que se deben configurar las stack.

        [webservers]
        localhost

        [dbservers]
        bensible

Aquí el servidor web sería configurado en el host local y el dbserver en un servidor llamado "bensible". La stack  se puede implementar mediante el siguiente comando:

        ansible-playbook -i hosts site.yml

Una vez hecho esto, puede comprobar los resultados consultando http://localhost/index.php.
se debería ver una página de prueba simple y una lista de bases de datos
servidor de base de datos.

