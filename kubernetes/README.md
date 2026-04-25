# Práctica 1 - Despliegue con Kubernetes

## Descripción general
Replica del escenario básico pero en vez de utilizar podman-compose, se utiliza el docker compose.

Para más información, véase el [README del escenario 1](../escenario1/README.md).

## Arquitectura desplegada
La solución se ha diseñado como una arquitectura mononodo dentro de un clúster local de Kubernetes. Cada servicio se despliega mediante un Deployment, y la comunicación interna se realiza a través de Service de tipo `ClusterIP`.

El acceso externo al servicio ownCloud se realiza mediante un Service de tipo NodePort, lo que permite exponer la aplicación fuera del clúster para su prueba y validación.

## Ficheros principales
El despliegue se organiza mediante los siguientes manifiestos:

- `namespace.yaml`: crea el espacio de nombres `practice1`.
- `configmap.yaml`: contiene la configuración no sensible del despliegue.
- `secret.yaml`: contiene las credenciales sensibles del sistema.
- `mariadb.yaml`: despliegue y servicio de MariaDB.
- `redis.yaml`: despliegue y servicio de Redis.
- `openldap.yaml`: despliegue y servicio de OpenLDAP.
- `owncloud.yaml`: despliegue y servicio de ownCloud.
- `users.ldif`: usuarios de prueba para importar en OpenLDAP.

## Despliegue
Para desplegar los recursos:

```bash
kubectl apply -f namespace.yaml
kubectl apply -f secret.yaml
kubectl apply -f configmap.yaml
kubectl apply -f mariadb.yaml
kubectl apply -f redis.yaml
kubectl apply -f openldap.yaml
kubectl apply -f owncloud.yaml
```

Para comprobar el estado de los recursos:
```bash
kubectl get all -n practice1
```

Acceso al servicio

Una vez desplegado, la URL de acceso a ownCloud puede obtenerse con:
```bash
minikube service owncloud -n practice1 --url
```

## Otras consideraciones
Hay que tener kubernetes o en este caso minukune funcionando, para ello se puede hacer con:
```bash
minikube start
```
