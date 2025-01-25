# Flujo de trabajo y despliegue de Jekyll

Aunque la documentación está escrita en asciidoc, también se puede
desplegar como un sitio web usando el generador de sitios estáticos Jekyll.
La versión de Jekyll crea una página para cada grupo de temas relacionados,
más de 100 páginas en total.

El funcionamiento de Jekyll se ha envuelto en un Makefile para mayor comodidad:

- `make build` construirá el sitio y todos los activos en el directorio `_site`
  para alojamiento

- `make preview` construirá el sitio y ejecutará una vista previa en un servidor
  HTTP ligero en el puerto que se imprime en la línea de comando

- `make all` construirá el sitio y ejecutará una serie de pruebas. Se
  recomienda hacer esto antes de publicar

- `make clean` limpiará los archivos generados por el proceso de construcción

Jekyll y el proceso de construcción ambos utilizan asciidoctor, por lo que
necesitas todas las mismas dependencias para la construcción de adoc además de
las dependencias de Jekyll y GNU make. Para simplificar la replicación de este
proceso se proporciona un `Containerfile` en el repositorio. Debería ser compatible
con el comando `docker` aunque se desarrolló con el comando `podman` completamente
libre. Un ejemplo de uso:

```sh
REPO=~/repos/onboarding-to-bitcoin-core/
podman build -v $REPO:/srv/ -t guide $REPO
id=$( podman run --cap-add NET_ADMIN --cap-add NET_RAW --detach -v $REPO:/srv/ -p 0.0.0.0:8080:4000 -it localhost/guide:latest )
podman attach $id
```

O para Docker:

```
REPO=~/repos/onboarding-to-bitcoin-core/

# docker build
docker build -f $REPO/Dockerfile -t guide $REPO
# o con docker buildx
docker build --load -f $REPO/Dockerfile -t guide $REPO

id=$( docker run --detach -v $REPO:/srv/ -p 8080:4000 -it guide:latest )
docker attach $id

bundle install # no debería ser necesario después de la construcción del Dockerfile, pero lo es...
```
