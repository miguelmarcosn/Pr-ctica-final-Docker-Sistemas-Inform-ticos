# Pra-ctica-final-Docker-Sistemas-Informa-ticos

En esta práctica voy a desplegar la aplicación que llevamos preparando este trimestre en contenedores de Docker.

Nuestro proyecto consiste en un front-end, un back-end y una base de datos, voy a utilizar todos los archivos disponibles en nuestra rama *Docker* de nuestro repositorio de Github que puede ser visionado aquí: <https://github.com/abascunana/LocalCritic/tree/docker>. Dispone de un archivo .war que contiene todo el contenido de nuestra web (en nuestro caso java, html, css y javascript), un archivo .yml que comentaremos posteriormente y un archivo .sql para la creación de las tablas de nuestra base de datos.


## Archivo .yml (docker-compose)

Dentro de este archivo tenemos todos los datos necesarios para el correcto despliegue de nuestros los tres contenedores que crearemos.

### MySql
Primero los datos necesarios para la creación de la base de datos mysql:

A comentar tenemos:
  - El nombre del contenedor, en este caso db.
  - El tipo de imagen, en este caso mysql.
  - Los puertos a utilizar, en este caso el puerto 3307 ya que el MySql-workbench utiliza el puerto 3306.
  - Declaramos dos volúmenes uno para la creación de la base de datos con el archivo mysql.
  - Declaramos la información necesaria para la creación de la base de datos.
  ![image](https://user-images.githubusercontent.com/91747025/173107830-ae4488e0-da76-44a1-9f06-350ef5e5f9a8.png)

  
 ### phpmyadmin
 A comentar tenemos:
  - Depende del contenedor 'db', el contenedor creado anteriormente para la base de datos
  - El nombre del contenedor, en este caso 'phpmyadmin'. 
  - El tipo de imagen, en este caso 'phpmyadmin/phpmyadmin'. 
  - El puerto que utiliza, en este caso el 8082.
  - Declaramos la contraseña y el host.
  - ![image](https://user-images.githubusercontent.com/91747025/173108383-c346e9f9-b97e-4c29-a2a3-0d22aca2b287.png)
### Tomcat
 A comentar tenemos:
  - El tipo de imagen a utilizar, en este caso el tomcat 10.0 ya que es el que hemos utilizado en nuestro proyecto.
  - Los archivos a utilizar para el despliegue de la web utilizando el .war.
  - El nombre del contenedor, en este caso tomcat.
  - Los datos de la base de datos a utilizar.
  ![image](https://user-images.githubusercontent.com/91747025/173108948-db3f8993-757e-4a80-b7a7-caa239b87f73.png)

## Pasos para el despliegue de la aplicación
Para el despliegue de la aplicación deberemos tener instalado correctamente docker, en mi caso docker desktop.
Ejecutamos la terminal en la carpeta donde tengamos los archivos.
![image](https://user-images.githubusercontent.com/91747025/173109528-8f0c9ceb-ac50-4daf-a9c7-cb00a045d095.png)

Dentro de la terminal ejecutamos el comando 'docker-compose up -d' para que se descarguen las imágenes necesarias
![image](https://user-images.githubusercontent.com/91747025/173109816-8116c441-27f9-4f07-8d7e-9d8e2dda93b6.png)
Y comprobamos que se hayan descargado correctamente
![image](https://user-images.githubusercontent.com/91747025/173110068-dd1522fc-81bb-448b-9079-438f4fb60294.png)
Una vez hecho esto ya podemos comprobar que funcione nuestra página

## Comprobación de la página 
Primero de todo nos dirigimos a `localhost:8080/LocalCritic`que es donde está nuestro proyecto dentro de tomcat.
![image](https://user-images.githubusercontent.com/91747025/173110570-8c1d036a-72b2-4875-91d6-e77555c54488.png)

Ahora comprobamos que se haya creado correctamente nuestra base de datos visitando el puerto 8082
![image](https://user-images.githubusercontent.com/91747025/173110797-f45d6060-b322-4810-9a90-7fdfbda36185.png)
Y nos registramos con las credenciales que hemos declarado para la base de datos
![image](https://user-images.githubusercontent.com/91747025/173110922-0291caf6-ee0b-408b-9768-1f9d5d64e63d.png)
Una vez dentro nos dirigiremos a la tabla 'usuarios' dentro de la base de datos 'LocaLcritic', podemos ver un usuario ya registrado, que es el utilizado para la práctica.
![image](https://user-images.githubusercontent.com/91747025/173111307-86d03bda-e3c3-493c-b35c-50f831de3c5c.png)
Ahora solo queda comprobar que funcionan los servlets, lo cual comprobaremos registrando un nuevo usuario.
![image](https://user-images.githubusercontent.com/91747025/173111628-9000c905-a975-418b-bee9-fcd7782004d7.png)
![image](https://user-images.githubusercontent.com/91747025/173111677-d6667fc4-322e-47a7-bc71-5a742053b1e3.png)
Usuario registrado correctamente, comprobemos el login
![image](https://user-images.githubusercontent.com/91747025/173111833-9786161f-65f6-4bb9-b794-cb987d343dba.png)
El login funciona correctamente, podemos ver que estamos logeados
![image](https://user-images.githubusercontent.com/91747025/173111996-7732debd-4db8-4484-ad9f-02a04b431f25.png)
Una vez hecho todo esto podemos ver que está desplegado correctamente.

## Preparación y subida a docker hub 
Primero ejecutamos `docker images` para poder ver los tags que tienen nuestra imágenes y poder subirlas a dockerhub
![image](https://user-images.githubusercontent.com/91747025/173113535-bd595061-5d34-4e8c-ba32-443493498715.png)
Y ahora ejecutamos `docker tag` para poder subir los conetendores al docker hub correctamente
Una vez le hayamos cambiado el nombre a los 3 hacemos un docker pull con cada uno de ellos para subirlos a nuestra cuenta
![image](https://user-images.githubusercontent.com/91747025/173118838-99b18688-8161-492f-9c36-fbafa98a17c8.png)
Y comprobamos que se hayan subido a nuestro dockerhub
![image](https://user-images.githubusercontent.com/91747025/173118931-057df6cd-8692-4691-8ef1-ec873a8af5fd.png)

## Conclusiones
Debido a que ya lo tenía bastante aprendido, el único problema que he tenido era que no me dejaba subir las imágenes al docker hub, lo he solucionado cambiando el perfil a privado, haciendo logout y luego volviendo a hacer un login.
## Anexos

Imágenes:
 - phpmyadmin: https://hub.docker.com/r/miguelmarcosnazco/phpmyadmin
 - MySql: https://hub.docker.com/r/miguelmarcosnazco/mysql
 - Tomcat: https://hub.docker.com/r/miguelmarcosnazco/tomcat



