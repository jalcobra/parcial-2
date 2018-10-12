Documentacion 
-------------------------------------------
Para poder migrar los servidores de Redhat/CentOS a Ubuntu server
-------------------------------------------
Configuracion de los dockers


primer paso, creación y configuraciones de dockers
-------------------------------------------

1. Debes construir un docker personalizado que incluye el servidor openssh,

```
docker build -t server:16.04 . 
```
En el paso anterior debes verificar el ID de la imágen que se creó y seleccionarla para los pasos a continuación.

Segundo paso, despliege
-------------------------------------------
Creacion de contenedores.
Crearemos unas maquinas para el despliegue de: apache y mysql.

El nombre para los contenedor web y mysql seran: web_server y mysql_server.

web_server afectara los puertos 2221:22 y 80:80.

mysql_server afectara los puertos 2222:22 y 3306:3306

```
docker run -d -P --name web_server -p 2221:22 -p 80:80 server:16.04
```

```
docker run -d -P --name mysql_server -p 2222:22 -p 3306:3306 server:16.04
```

Tercer paso, configuración de alias
-------------------------------------------

Opción 1: edita el archivo ```/etc/hosts``` y adiciona 2 alias a localhost
```
127.0.0.1       web_server mysql_server
```
Opción 2: adición automática en el archivo de hosts del sistema
```
echo "127.0.0.1 web_server mysql_server" | sudo tee -a /etc/hosts
```

Cuarto paso, adicionar las llaves ssh
-------------------------------------------
Ejecutamos los siguientes comandos para darle los ```permisos 0600``` que son los de escritura y lectura. 
```
chmod 0600 ../key.private
```
```
chmod 0600 authorized_keys
```

```
ssh -o StrictHostKeyChecking=no root@web_server -p 2221 -i ../key.private hostname 
```
```
ssh -o StrictHostKeyChecking=no root@mysql_server -p 2222 -i ../key.private hostname
```

Quinto paso, confirmación
-------------------------------------------
Realiza una prueba de conexión a las maquinas que se crearon recientemente, por defecto el paso anterior crea n cantidad de dockers con el ```puerto 2221 y 2222``` abiertos para conexión:
```
ssh root@web_server -p 2221 -i ../key.private 
ssh root@mysql_server -p 2222 -i ../key.private
```

Si la conexión se establece, ya está listo para seguir con ansible.
-------------------------------------------
