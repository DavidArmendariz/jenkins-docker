# Jenkins Docker

Crear un bridge network en Docker para jenkins:

```bash
docker network create jenkins
```

Construir la imagen de Jenkins a partir del Dockerfile:

```bash
docker build -t myjenkins-blueocean:2.462.2-1 .
```

Para crear el contenedor de Jenkins:

```bash
docker run \
  --name jenkins-blueocean \
  --restart=on-failure \
  --detach \
  --network jenkins \
  --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client \
  --env DOCKER_TLS_VERIFY=1 \
  --publish 49000:8080 \
  --publish 50000:50000 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  myjenkins-blueocean:2.462.2-1
```
