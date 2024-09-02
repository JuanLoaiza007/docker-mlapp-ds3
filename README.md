# Laboratorio Machine Learning con Docker

https://docs.google.com/document/d/1k-ZFOHercG_88iAVoYOFP-RWvLRbQWVWMo1Y8vvuZgQ/edit?usp=sharing

Este es el lab de la clase del 2024-08-28, la idea es montar un pequeño modelo de Machine Learning pero usando Kubernets.

## Forma normal

> docker compose up

Facil o que?

Las peticiones se le hacen tipo POST a la direccion:
http://localhost:8000/prediction/

Con un cuerpo así:

Body:

> {"hour": 12, "day": 7}

## Con Kubernetes

La idea es:

1. Subir el archivo a Dockerhub o en este caso a Github.
2. Crear el my-deployment.yaml como se muestra en el otro lab: un deployment y un servicio para poner esto a funcionar.
3. Probar a ver si funciona.

### Creando imagen y subiendola a Github

Se usa esta guia para subir la imagen a Github, esto se hace gracias al servicio de Github Packages:
https://docs.github.com/es/packages/working-with-a-github-packages-registry/working-with-the-container-registry

#### Iniciar sesion en Github Packages

Es necesario contar con un token clásico y con los permisos para escribir y borrar paquetes.

Para iniciar sesión en Github Packages usar:

> cat token.txt | docker login ghcr.io -u USERNAME --password-stdin

- USERNAME: es el usuario de github

#### Construir imagen

> docker build -t ghcr.io/NAMESPACE/IMAGE_NAME:1.0 .

- NAMESPACE: es el nombre del usuario de github.
- IMAGE_NAME: es el nombre de la imagen.
- 1.0: es la version de la imagen, puede usarse cualquiera.

#### Publicar la imagen a github packages:

> docker push ghcr.io/NAMESPACE/IMAGE_NAME:1.0

Se encontrará en la ruta:

> https://github.com/users/NAMESPACE/packages/container/package/IMAGE_NAME

#### Correr con Docker Run

En este caso es posible correr la imagen con Docker Run así:

> docker run -d -p 8000:8000 --name mlapp-ds3-container ghcr.io/NAMESPACE/IMAGE_NAME:1.0

- Hay que agregarle el puerto por la naturaleza de esta app
- mlapp-ds3-container: es el nombre que se le da al contenedor pero se puede poner cualquiera

### Creando el deployment

1. Crear el my-deployment.yaml como se muestra en el otro lab, en este caso es intuitivo siguiendo el ejemplo y considerando como se corre con Docker Run, aqui esta el ejemplo:
   https://docs.google.com/document/d/15KnHpWAB4o_zkm_7N3wTTHVOL1mz1bkwYC5-GOyncs4/edit?usp=sharing

2. Listoooooo, a ver si funciona:

> kubectl apply -f my-deployment.yaml

3. Y comandos pa inspeccionar:
   > kubectl get deployments
   > kubectl get services
   > kubectl get pods
