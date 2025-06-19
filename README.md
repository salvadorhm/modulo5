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

Otra forma de verificar el estado de los contenedores 

```bash
docker container ls -a
```

## 5. Conectarse al contenedor

Con el siguiente comando se accede al contenedor creado a traves de la terminal

```bash
docker compose exec application bash
```

## 6. Iniciar los contenedores nuevamente

Con el siguiente comando se levantan nuevamente los contenedores

```bash
  docker compose up -d
```

# API REST

## 1. Listar eventos

```bash
curl http://localhost:8000/api/eventos
```


## 2. Agregar un nuevo evento

```bash
curl -X POST http://localhost:8000/api/eventos \
  -H "Content-Type: application/json" \
  -d '{
    "titulo": "Escuela Pública de Código",
    "descripcion": "Inicia oficialmente el curso de Bases tecnológicas en el servicio público",
    "fecha_inicio": "2025-01-01",
    "fecha_fin": "2025-06-30",
    "ubicacion": "En línea"
  }'
```

## 3. Consultar evento

```bash
curl http://localhost:8000/api/eventos/1
```

## 4. Actualizar evento

```bash
curl -X PUT http://localhost:8000/api/eventos/1 \
  -H "Content-Type: application/json" \
  -d '{
    "titulo": "Curso actualizado",
    "descripcion": "Descripción modificada",
    "fecha_inicio": "2025-02-01",
    "fecha_fin": "2025-07-31",
    "ubicacion": "Presencial"
  }'
```

## 5. Borrar evento 

```bash
curl -X DELETE http://localhost:8000/api/eventos/1
```

