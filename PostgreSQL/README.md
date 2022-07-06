# Configuration for PostGreSQL with pgAdmin

## To run
`docker-compose up -d`

__Please note:__ The configuration file requires the setting of [environment variable](#environment-variables). This can also be done using an _.env_ file right in the folder of the docker compose file or by passing it as part of the docker compose command:

`docker-compose --env-file env.dev up -d`

## Ports at the host
* 5432 - Database port for PostGreSQL
* 5480 - HTTP port for pgAdmin

## Environment variables
Environment variables that need to be configured in the shell or using the [.env](https://docs.docker.com/compose/environment-variables/) file:
* POSTGRES_PASSWORD - root password for the database. This password is also used by phpMyAdmin
* POSTGRES_USER - default user for MariaDB
* PGADMIN_DEFAULT_EMAIL - password of default user for MariaDB
* PGADMIN_DEFAULT_PASSWORD - default database that will be created on startup if not exists

## Volumes
PostGreSQL database folder and PGAdmin folder are persistent in volumes. The files can be found in _/var/lib/docker/volumes/_ on a Linux system.

## Creating a database dump
Use the following command:

`docker-compose exec <container> pg_dump --username=<user> -d <database> > dump.sql`

Where:
* _database_ is the name of the database to be exported.
* _user_ is the name of the database user (e.g. postgres)
* _container_ name of the PostGreSQL container
