# MongoDB-Docker-Basic

![](https://www.arsys.es/blog/file/uploads/2016/10/MongoDB.jpg)
![](https://miro.medium.com/v2/resize:fit:1000/1*JK4VDnsrF6YnAb2nyhMsdQ.png)

Para correr MongoDB en Docker seguiremos los siguientes pasos en los que crearemos una series de instrucciones en el archivo .yml para instalar MongoDB en el contenedor, luego crearemos el .sh para ejecutar la creacion del contenedor (ejecutando el .yml) y entrar al mismo. 


Instalar Mongo: 
En la línea de comando.
____________________________________________________________

<ol>
<li>Crear documento de docker-compose</li>

Opción 1.

> Usar docker compose, visual estudio code, instalando la extensión de docker.

Opción 2.

> Con el comando touch crearemos el archivo .yml

    touch docker-compose.yml

> Con el comando cat > escribiremos ese archivo con las instrucciones del paso siguiente

    cat > docker-compose.yml
_____________________________________________
<li>Crear documento de docker-compose.yml</li>

    version: '2.2'

    services:

     mongo:
      image: mongo:4.0.4
      restart: always
      container_name: monguito
      environment:
        - MONGODB_USER="user"
        - MONGODB_PASS="pass"
      
      volumes:
        - ./monguitodata:/data/db
        - ./monguitodata/log:/var/log/mongodb/
      ports:
        - "27017:27017"
    
(En las palabras entre "" se puede reemplazar el nombre del usuario y la contraseña por una a eleccion para acceder)
(Presionaremos Ctrl + D para cerrar la escritura del archivo)
____________________________________________________________
<li>Crear archivos para correr comando en la la terminal</li>

> touch mongo.sh
__________________________________________
<li>Cargar comandos al archivo creado</li>

> cat > mongo.sh   	(Copiar y pegar los comandos que queremos se ejecuten automáticos)

**Crear carpeta para volumen de mongo:**

    mkdir monguitodata
    
    cd monguitodata
    
    mkdir log

**Iniciar el contenedor:**

    sudo docker-compose up -d

**Mostrar mensaje:**

    echo "Monguito está iniciandose ......."

**Entrar en el contenedor**

    sudo docker exec -it monguito bash

_______
<li>Salimos del archivo para que se escriba</li>

> Control + d
_________________________________________________________
<li>Asignar permisos de ejecución y ejecutar mongo.sh</li>

> chmod u+x mongo.sh
> 
> ./mongo.sh 
</ol>


### Una vez que tenemos MongoDB corriendo ya podemos probar los comandos basicos:


# COMANDOS MONGO DB
_______________________
Mostrar Bases de datos:

     show dbs
______________________________________
Crear o ubicarse en uns base de datos:

     use databasename
_______________________________________
Saber que base de datos estamos usando:

    db
________________
Crear colección:
 
    db.createCollection('nameCollection')
    {"Clave": "Valor"}

________________
Mostrar el contenido de una colección:

    showCollections
