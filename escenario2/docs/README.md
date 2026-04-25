# Práctica 1 - Escenario 2

## Descripción general
En este directorio se presenta la segunda parte de la primera práctica, que consiste en la ampliación del despliegue básico de ownCloud hacia una arquitectura con mayor tolerancia a fallos. Y el sistema está compuesto por los siguientes servicios:

- HAProxy: balanceador de carga encargado de distribuir las peticiones entre las instancias de ownCloud.
- ownCloud1: primera instancia del servicio principal de almacenamiento y gestión de archivos accesible vía web.
- ownCloud2: segunda instancia del servicio principal de almacenamiento y gestión de archivos accesible vía web.
- MariaDB: sistema de gestión de base de datos relacional utilizado por ownCloud para almacenar su información persistente.
- Redis: servicio auxiliar utilizado como caché y para mejorar la gestión interna del sistema.
- OpenLDAP: servicio de directorio y autenticación centralizada para la gestión de usuarios.

La solución se ha diseñado como una evolución del escenario básico, siguiendo la descripción del escenario 2 del enunciado, en el que se introduce redundancia en la capa web mediante dos instancias ownCloud detrás de un balanceador.

## Objetivos
El objetivo de esta implementación es extender la arquitectura mínima del escenario básico hacia una solución con balanceo de carga y mayor disponibilidad del servicio.

Además, se busca demostrar la integración de un balanceador de carga con múltiples instancias de la aplicación, la replicación de al menos uno de los microservicios, en este caso el servidor web ownCloud, la continuidad del servicio ante la caída de una de las instancias web, la persistencia de datos mediante volúmenes y la autenticación de múltiples usuarios mediante LDAP.

## Arquitectura desplegada
La solución se ha diseñado como una arquitectura mononodo con varios contenedores conectados mediante una red interna. HAProxy actúa como punto de entrada al sistema y reparte el tráfico entre owncloud1 y owncloud2.

Ambas instancias de ownCloud se conectan internamente con:

- MariaDB, para el almacenamiento de datos,
- Redis, como servicio auxiliar,
- OpenLDAP, para la autenticación de usuarios.

De esta forma, se simula una arquitectura con alta disponibilidad en la capa de aplicación, de modo que el servicio siga estando accesible aunque una de las dos instancias web deje de estar disponible.

## Puertos utilizados
Se ha usado el rango de puertos asignado en docker.ugr.es:

- 20172 → HAProxy
- 20173 → ownCloud1
- 20174 → ownCloud2
- 20175 → OpenLDAP

Mientras que el resto no se exponen, ya que reducen la superficie de exposición y mantiene esos servicios accesibles únicamente desde la red interna de contenedores.


## Estructura del proyecto
```text
escenario2/
├── docs/
├── haproxy/
│   └── haproxy.cfg      # configuración del balanceador HAProxy
├── ldap/
│   └── users.ldif       # usuarios de prueba para OpenLDAP
├── .env                 # variables de entorno del despliegue
└── compose.yaml         # definición de los servicios, red y volúmenes