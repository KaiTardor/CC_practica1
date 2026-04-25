# Práctica 1 - Escenario básico

## Descripción general
En este directorio se presenta la parte básica de la primera práctica, que consiste en el despliegue de un servicio ownCloud autohospedado usando contenedores. La arquitectura se despliega en `docker.ugr.es` utilizando Podman. Y el sistema está compuesto por los siguientes servicios:

- ownCloud: servicio principal de almacenamiento y gestión de archivos accesible vía web
- MariaDB: sistema de gestión de base de datos relacional utilizado por ownCloud para almacenar su información persistente.
- Redis: servicio auxiliar utilizado como caché y para mejorar la gestión interna del sistema.
- OpenLDAP: servicio de directorio y autenticación centralizada para la gestión de usuarios.

La solución se ha diseñado como un despliegue mononodo, siguendo las descripciones para el escenario 1 del enunciado.

## Objetivos
El objetivo de esta implementación es desplegar la arquitectura mínima funcional exigida en la práctica, integrando los cuatro servicios obligatorios (ownCloud, MariaDB, Redis y OpenLDPA). Ademas se busca demostrar el despliegue reproducible con contenedores, la comunicación entre servicios, la persistencia de datos mediante volúmenes y la autenticación de usuarios mediante LDAP.

## Arquitectura desplegada
La solución se ha diseñado como una arquitectura simple y funcional, formada por un único nodo con un contenedor para cada servicio. La aplicación ownCloud se conecta internamente con MariaDB para el almacenamiento de datos, con Redis como servicio auxiliar y con OpenLDAP para la autenticación de usuarios.

## Puertos utilizados
Se ha usado el rango de puertos asignado en docker.ugr.es: 

- 20170 → ownCloud
- 20171 → OpenLDAP

Mientras que el resto no se exponen, ya que reducen la superficie de exposición y mantiene esos servicios accesibles únicamente desde la red interna de contenedores.


## Estructura del proyecto
```
practice1/
├── docs/
├── ldap/
│   └── users.ldif      # fichero LDIF con usuarios de prueba para OpenLDAP
├── .env                # variables de entorno del despliegue
└── compose.yaml        # definición de los servicios, red y volúmenes
```

