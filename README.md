
# Instalacion de trastienda la vienesa

## Prerequisito

Para instalar la trastienda primero se necesita Git y Doker. 
Se puede seguir los pasos de instalacion segun su sistema operativo en los sigtes links.

[Guia para Docker](https://docs.docker.com/get-started/get-docker/)

[Guia para Git](https://git-scm.com/downloads)

## Trastienda

Para instalar la trastienda tenemos que clonar el proyecto (solicitar token de acceso).
```bash
git clone https://github.com/utonio1/trastienda_lavienesa.git && cd ./trastienda_lavienesa
```

Crear el archivo .env dentro de la carpeta `trastienda_lavienesa` con el contenido sigte
```txt
DB_USER="postgres"
DB_PASSWORD="postgres"
DB_PORT="5432"
DB_DATABASE="trastienda"
DB_HOST="trastienda-postgres"
```

Luego corremos el comando sigte.
```bash
docker compose -f ./docker-compose.production.yml up --build -d
```
desde la terminal corremos el sigte comando

```bash
docker run -it -w /var/www/html --volumes-from trastienda-php --name trastienda-bash bash:latest bash
apk add php
apk add composer
```

Con esto vamos a tener creados los servicios de la trastienda(postgres, php y nginx). Luego de esto y dentro del contenedor de php correr el comando

```bash
composer install
```

Por ultimo y con la ayuda de Pgadmin podemos conectarnos a la nueva base de datos para realizar el restore de la base de datos


# Actualizaciones de trastienda la vienesa

Para mantener el proyecto actualizado desde la terminal:

1. Navegá hasta la raíz del proyecto, por ej:
```bash
cd /ruta/a/tastienda_lavienesa
```

2. Ejecutá el pull de los últimos cambios:

```bash
git pull
```

3. Al realizar el pull, se solicitará un nombre identificador (quién actualizó) y un token de acceso personal.
- Si no tenés el token, solicitá uno al equipo técnico.
- El token tiene una validez de 24hs.

