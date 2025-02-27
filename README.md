
# Instalacion de trastienda la vienesa

## Prerequisito

Para instalar la trastienda primero se necesita Git y Doker. 
Se puede seguir los pasos de instalacion segun su sistema operativo en los sigtes links.

[Guia para Docker](https://docs.docker.com/get-started/get-docker/)

[Guia para Git](https://git-scm.com/downloads)

## Trastienda

Para instalar la trastienda tenemos que clonar el proyecto (solicitar token de aceso).
```bash
git clone https://github.com/utonio1/trastienda_lavienesa.git && cd ./trastienda_lavienesa
```

Crear el archivo .env dentro de la carpeta `trastienda_lavienesa` con el contenido sigte
```txt
DB_USER="postgres"
DB_PASSWORD="postgres"
DB_PORT="5432"
DB_DATABASE="trastienda"
DB_HOST="localhost"
```

Luego corremos el comando sigte.
```bash
docker compose -f ./docker-compose.production.yml up --build -d
```
desde la terminal corremos el sigte comando

```bash
docker run -it -w /var/www/html --volumes-from trastienda-php --name trastienda-bash bash:latest bash
```

Con esto vamos a tener creados los servicios de la trastienda(postgres, php y nginx). Luego de esto y dentro del contenedor de php correr el comando

```bash
composer install
```

Por ultimo y con la ayuda de Pgadmin podemos conectarnos a la nueva base de datos para realizar el restore de la base de datos
