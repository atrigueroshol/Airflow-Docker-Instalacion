# Instalación de Apache Airflow en Docker (Windows)

Apache Airflow es una plataforma de **orquestación de flujos de trabajo** que permite programar, monitorizar y gestionar tareas complejas de manera eficiente. Este documento está diseñado para guiarte paso a paso en la **instalación y ejecución de Airflow usando Docker y Docker Compose** en WINDOWS.

# Requisitos
Tener instalado Docker y Docker Compose. Lo podemos verificar en la shell

    docker --version
    docker compose version

## Estructura de carpetas y ficheros

Debemos definir la siguiente estructura de proyecto:
- proyecto/
	- config/
	- dags/
	- logs/
	- plugins/
	- .env
	- docker-compose.yaml
	
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
