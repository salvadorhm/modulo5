# Md́oulo 5

Laravel y API REST

## 1. Instalación de MySQL y Laravel

Se crea el archivo **docker-compose.yaml** con la configuracion de MySQL y Laravel

```yaml
services:
  mariadb:
    image: 'bitnami/mariadb:latest'
    environment:
      - ALLOW_EMPTY_PASSWORD=yes
      - MARIADB_USER=bn_myapp
      - MARIADB_DATABASE=bitnami_myapp
      - MARIADB_PASSWORD=b1tnam1_my@pp
    volumes:
      - 'mariadb_data:/bitnami/mariadb'
    networks:
      - laravel-network

  application:
    image: 'bitnami/laravel:latest'
    environment:
      - LARAVEL_DATABASE_TYPE=mysql
      - LARAVEL_DATABASE_HOST=mariadb
      - LARAVEL_DATABASE_PORT_NUMBER=3306
      - LARAVEL_DATABASE_NAME=bitnami_myapp
      - LARAVEL_DATABASE_USER=bn_myapp
      - LARAVEL_DATABASE_PASSWORD=b1tnam1_my@pp
    ports:
      - '8000:8000'
    volumes:
      - './src:/app'
    depends_on:
      - mariadb
    networks:
      - laravel-network

volumes:
  mariadb_data:
    driver: local

networks:
  laravel-network:
    driver: bridge
```

## 2. Construir los contenedores

Se crean los contenedores y se levanta el servidor de **laravel**

```bash
docker compose up --build -d
```

## 3. Detener los contenedores

Para detener los contenderos se utiliza el siguiente comando

```bash
docker compose down
```

## 4. Verificar los contenedores

Con el comando ps se puede verficiar el estatus de los contenedores

```bash
docker compose ps
```

## 5. Conectarse al contenedor

Con el siguiente comando se accede al contenedor creado a traves de la terminal

```bash
docker compose exec application bash
```