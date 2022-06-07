# Configuration for MariaDB with phpMyAdmin

## To run
`docker-compose up -d`

__Please note:__ The configuration file requires the setting of [environment variable](#environment-variables). This can also be done using an _.env_ file right in the folder of the docker compose file or by passing it as part of the docker compose command:

`docker-compose --env-file env.dev up -d`

## Ports at the host
* 3306 - Database port for MariaDB
* 3380 - HTTP port for phpMyAdmin

## Environment variables
Environment variables that need to be configured in the shell or using the [.env](https://docs.docker.com/compose/environment-variables/) file:
* MARIADB_ROOT_PASSWORD - root password for the database. This password is also used by phpMyAdmin
* MARIADB_USER - default user for MariaDB
* MARIADB_PASSWORD - password of default user for MariaDB
* MARIADB_DATABASE - default database that will be created on startup if not exists

## Volumes
Only MariaDB database folder is persistent in a volume. The files can be found in _/var/lib/docker/volumes/mariadb_db_data_ on a Linux system.
