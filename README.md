# psql-client-docker
Containerized PostgreSQL client for executing SQL commands in containerized environments

The `psql-client` image is stored on Docker Hub in the [rtdl/psql-client repository](https://hub.docker.com/r/rtdl/psql-client).

## rtdl - The Real-Time Data Lake
This is a sub-project of [rtdl](https://github.com/realtimedatalake/rtdl) – the real-time 
data lake. Please go to rtdl's repo and give it a star.

## How to use
This image is not interactive and has no default ENTRYPOINT. You can use the `entrypoint` option to execute psql commands and `volumes` to load scripts that can be executed with the psql client.
### Docker Run example
```
docker run --name psql-client \
-v ${PWD}/catalog/scripts/create-user-db.postgres.sql:/create-user-db.postgres.sql \
--entrypoint psql \
rtdl/psql-client:latest \
-h dbhost -p 5433 -U postgres -f /create-user-db.postgres.sql
```

### Docker Compose example
```
psql-client:
  image: rtdl/psql-client:latest
  container_name: psql-client
  volumes:
    - ./catalog/scripts/create-user-db.postgres.sql:/create-user-db.postgres.sql
  entrypoint: psql -h dbhost -p 5433 -U postgres -f /create-user-db.postgres.sql
```

## Build
If you want to build the image yourself, clone the repo and run `docker build -t rtdl/psql-client:latest .`.
