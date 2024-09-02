# Laboratorio Machine Learning con Docker

https://docs.google.com/document/d/1k-ZFOHercG_88iAVoYOFP-RWvLRbQWVWMo1Y8vvuZgQ/edit?usp=sharing

Este es el lab de la clase del 2024-08-28, la idea es montar un pequeño modelo de Machine Learning pero usando Kubernets.

## Forma normal

> docker compose up

Facil o que?

Las peticiones se le hacen tipo POST a la direccion:
http://localhost:8000/prediction/

Con un cuerpo tipo:

Body:

> {"hour": 12, "day": 7}

## Con Kubernetes

La idea es:

1. Subir el archivo a Dockerhub o en este caso a Github
2. Crear el my-deployment.yaml como se muestra en el otro lab, un deployment y un servicio para poner esto a funcionar.
3. Probar a ver si funciona

### Imperativamente

1. Crear el my-deployment.yaml como se muestra en el otro lab:
   https://docs.google.com/document/d/15KnHpWAB4o_zkm_7N3wTTHVOL1mz1bkwYC5-GOyncs4/edit?usp=sharing

2. Listoooooo, a ver si funciona:

   > kubectl apply -f my-deployment.yaml

3. Y comandos pa inspeccionar:
   > kubectl get deployments
   > kubectl get services
   > kubectl get pods

#### Guardar imagen contenedor en GitHub

https://docs.github.com/es/packages/working-with-a-github-packages-registry/working-with-the-container-registry
