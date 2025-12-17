# Instalación de Apache Airflow en Docker (Windows)

Apache Airflow es una plataforma de **orquestación de flujos de trabajo** que permite programar, monitorizar y gestionar tareas complejas de manera eficiente. Este documento está diseñado para guiarte paso a paso en la **instalación y ejecución de Airflow usando Docker y Docker Compose** en WINDOWS.

# Requisitos
Tener instalado Docker y Docker Compose. Lo podemos verificar en la shell

    docker --version
    docker compose version
Se recomienda tener versiones:
- Docker: 20.10.0+
- Docker Compose 2.3+

En windows cuando instalamos Docker Desktop se instala automáticamente Docker Compose.
Se puede descargar Docker Desktop en la siguiente url: [Docker Desktop](https://docs.docker.com/desktop/setup/install/windows-install/)

## Estructura de carpetas y ficheros

Debemos definir la siguiente estructura de proyecto:
- proyecto/
	- config/
	- dags/
	- logs/
	- plugins/
	- .env
	- docker-compose.yaml
	
La carpeta **config**/ contiene archivos de configuración personalizados de Airflow.
La carpeta **dags**/ contiene tus DAGs (Directed Acyclic Graphs), que son los flujos de trabajo que Airflow ejecuta.
La carpeta **logs**/ es donde Airflow escribe logs automáticamente aquí, y tú puedes revisarlos para depurar tus flujos de trabajo.
La carpeta **plugins**/ lugar para plugins personalizados de Airflow, como operadores, sensores o hooks que extienden la funcionalidad de Airflow.
El fichero **.env** sirve para almacenar las variables de entorno.
El fichero **docker-compose.yaml** para levantar Airflow y sus servicios relacionados mediante Docker Compose. Define qué contenedores se necesitan (webserver, scheduler, database, worker), cómo se comunican y qué volúmenes montar. Ejecutas `docker-compose up` y Docker crea todos los contenedores según esta configuración.

Creamos el proyecto y accedemos a la carpeta:

    mkdir proyecto
    cd proyecto
   
Creamos las carpetas (config, dags, logs y plugins)

    mkdir config, dags, logs, plugins
    
Creamos el fichero .env y definimos la variable AIRFLOW_UID

    New-Item -Path . -Name ".env" -ItemType "file" -Force
    Add-Content .env "AIRFLOW_UID=50000"
    
Descargamos el fichero docker-compose.yaml en la siguiente url: [docker-compose.yaml](https://airflow.apache.org/docs/apache-airflow/3.1.5/docker-compose.yaml)


## Inicializamos el entorno y corremos AIRFLOW

Lo primero que debemos hacer es inicializar la base de datos

    docker compose up airflow-init
    
Una vez terminado iniciamos el resto de servicios

    docker compose up

Una vez terminado ya podemos acceder a la interfaz gráfica de airflow en local en la siguiente url
[http://localhost:8080/](http://localhost:8080/)

El usuario y la contraseña es **airflow**
