## Pasos para instalar trastienda.

### Prerequisito

_correr estos comandos en el servidor nuevo_

```sh
sudo apt-get remove docker docker-engine docker.io containerd runc
```
```sh
sudo apt-get update
```
```sh
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```
```sh
sudo mkdir -p /etc/apt/keyrings
```
```sh
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```
```sh
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
```sh
sudo apt-get update
```
```sh
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```
```sh
sudo groupadd docker
```
```sh
sudo usermod -aG docker $USER
```
```sh
newgrp docker
```
```sh
sudo systemctl enable docker.service
```
```sh
sudo systemctl enable containerd.service
```

### Copiar el proyecto de una sucursal activa

_ingresar en la terminal del servidor de donde se va a copiar_

```sh
docker cp trastienda-php:/var/www/html/ ./trastienda && tar -czf trastienda.tar.gz trastienda/ && rm -r trastienda
```
_copiar el archivo trastienda.tar.gz y pegar en el servidor nuevo_

```sh
rm -r trastienda
```

### Instalar los servicios

_En el servidor nuevo ejecutar lo sigtes comandos_

```sh
tar -xzf trastienda.tar.gz trastienda && cd ./trastienda
```
```sh
docker compose -f ./docker-compose.production.yml up --build -d
```
```sh
cd ../ && rm -r trastienda
```

### Backup de la base de datos

_Con PGadmin realizar backup de la base de datos de una sucursal activa y restaurar en el servidor nuevo con el nombre de trastienda_prod_
_En la base de datos nueva ejecutar la sigte sentencia_
```sql
ALTER SEQUENCE add_desposte_sec RESTART WITH 1;
ALTER SEQUENCE add_factura RESTART WITH 1;
ALTER SEQUENCE add_produccion_sec RESTART WITH 1;
ALTER SEQUENCE add_snc RESTART WITH 1;
ALTER SEQUENCE add_transformacion_sec RESTART WITH 1;
ALTER SEQUENCE log_error_internalid_seq RESTART WITH 1;
ALTER SEQUENCE next_cod_snc RESTART WITH 1;


TRUNCATE 
add_compra_cabecera,
add_compra_detalle,
add_desposte_cab,
add_desposte_det,
add_error_remito_cab,
add_error_remito_det,
add_produccion,
add_snc_cabecera,
add_snc_detalle,
add_transferencia_interna_cab,
add_transferencia_interna_det,
add_transformacion_cab,
add_transformacion_det,
confirmados,
his_pedido,
his_pedido2,
log_error,
salida_sap,
sap_pedido_cabecera,
sap_pedido_desposte,
sap_pedido_detalle,
sap_remision_cabecera,
sap_remision_detalle,
sap_sol_remision_cabecera,
sap_sol_remision_detalle,
xpk;
```

_Por ultimo y muy importante, actualizar los datos de la tabla config con los datos correspondientes a la sucursal nueva_
