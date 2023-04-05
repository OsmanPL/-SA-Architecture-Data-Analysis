# -SA-Architecture-Data-Analysis

## Descripción
Se crea una arquitectura para el analisis de datos.
Consiste en los siguientes elementos:
- Base de datos: MySQL
- Gestor de notebooks de analisis de datos: Jupyter Lab
- Software de visualización de datos: Grafana


## Docker Compose

### Servicio db:
Se utiliza la imagen latest de mysql, se colocan las variables de entorno necesarias para el contenedor, en este caso la contraseña para el usuario root, una base de datos y otro usuario con su contraseña, tambien estara el puerto donde estara el contenedor en nuestro caso sera el 3306.
Tambien tiene el volumen del contenedor el cual apunta al directorio "./data/mysql" de nuestro pc y el directorio "var/lib/mysql" dentro del contenedor.
Y se une a la red "my-network"

```yml
db:
    image: mysql:latest
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: example
      MYSQL_DATABASE: example
      MYSQL_USER: example
      MYSQL_PASSWORD: example
    volumes:
      - ./data/mysql:/var/lib/mysql
    ports:
      - "3306:3306"
    networks:
      - my-network
```

### Servicio db:
Se utiliza la imagen latest de jupyter/datascience-notebook, se coloca el puerto donde estara el contenedor que sera el 8888.
Tambien estara un volumen para los notebooks el cual estara en el directorio de nuestra pc en "./notebooks" y en el contenedor estara en el directorio "/home/jovyan/work".
Y se unira a la red "my-network".

```yml
jupyter:
    image: jupyter/datascience-notebook:latest
    restart: always
    volumes:
      - ./notebooks:/home/jovyan/work
    ports:
      - "8888:8888"
    networks:
      - my-network
```


### Servicio db:
Se utiliza la imagen latest de grafana/grafana, se coloca el puerto donde estara el contenedor que sera el 3000.
Tambien estara un volumen para los notebooks el cual estara en el directorio de nuestra pc en "./data/grafana" y en el contenedor estara en el directorio "/var/lib/grafana".
Y se unira a la red "my-network".

```yml
grafana:
    image: grafana/grafana:latest
    restart: always
    ports:
      - "3000:3000"
    networks:
      - my-network
```


### Creación de la red

Con el siguiente codigo se pueden crear las redes necesarias para el docker-compose.

```yml
networks:
  my-network:
```

## Ejemplo

