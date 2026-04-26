# Práctica 1 - Despliegue de ownCloud con contenedores

Este repositorio contiene el desarrollo de la Práctica 1, centrada en el despliegue del servicio ownCloud utilizando tecnologías de contenedores y orquestación.

El objetivo general del proyecto es construir y documentar distintas soluciones de despliegue para ownCloud, partiendo de una arquitectura básica y evolucionando posteriormente hacia configuraciones más completas y realistas. Para más información de cada escenario, consulte el README.md asociado a cada directorio.

## Entorno de desarrollo y de producción utilizado
El desarrollo y validación de la práctica se ha realizado principalmente en el servidor `docker.ugr.es`, utilizando un entorno basado en Linux y herramientas de contenedores como Podman y podman-compose.

### Herramientas adicionales utilizadas
- **kubectl**: `v1.35.3`
- **minikube**: `v1.38.1`
- **HAProxy**: `3.0`
- **OpenLDAP**: `1.5.0`
- **MariaDB**: `11`
- **Redis**: `7`
- **ownCloud**: `10.15.3`


## Estructura del repositorio
El trabajo se organiza en subdirectorios independientes, cada uno correspondiente a una parte o escenario de la práctica:

- escenario1/: implementación correspondiente al escenario 1.
- escenario2/: implementación correspondiente al escenario 2.
- docker/: replica del escenario 1 en docker (no funcional)
- kubernetes/: replica el escenario 1 mediante minikube
- README.md: Fichero de descripci´n general del proyecto
- .gitignore

## Conclusión
En definitiva, esta práctica me ha permitido desplegar ownCloud en distintos entornos y con varias herramientas, comprobando cómo cambia la arquitectura en función del nivel de complejidad requerida de dicho escenario. 

Sin lugar a dudas, la mayor complejidad fue la integración y ajuste de todos los servicios entre sí, especialmente como funcionaba la autenticación mediante LDAP y, más adelante, la transición hacia una arquitectura con balanceo de carga y varias instancias de ownCloud, donde en la configuración se me atrancó un poco. 

En conjunto, la práctica sirve como una breve introducción para entender mejor cómo desplegar una aplicación real en contenedores y cómo escalarla a escenarios más completos.


## Referencias bibliográficas
- OpenLDAP Software 2.6 Administrator's Guide - Quick Start:
https://www.openldap.org/doc/admin26/quickstart.html

- HAProxy Documentation 2.6 - Introduction:
http://docs.haproxy.org/2.6/intro.html

