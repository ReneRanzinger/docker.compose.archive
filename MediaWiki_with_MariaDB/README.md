# Configuration for MariaDB with phpMyAdmin

## To run
`docker-compose up -d`

__Please note:__ The configuration file requires the setting of [environment variable](#environment-variables). This can also be done using an _.env_ file right in the folder of the docker compose file or by passing it as part of the docker compose command:

`docker-compose --env-file env.dev up -d`

## Ports at the host
* 8080 - HTTP port for the mediawiki
* 3380 - HTTP port for phpMyAdmin

## Environment variables
Environment variables that need to be configured in the shell or using the [.env](https://docs.docker.com/compose/environment-variables/) file:
* MARIADB_ROOT_PASSWORD - root password for the database. This password is also used by phpMyAdmin
* MARIADB_USER - default user for MariaDB
* MARIADB_PASSWORD - password of default user for MariaDB
* MARIADB_DATABASE - default database that will be created on startup if not exists

## Volumes
Only MariaDB database folder is persistent in a volume. The files can be found in _/var/lib/docker/volumes/mariadb_db_data_ on a Linux system.

## Setup
There are several steps to finalize setting up the wiki system:
* Start the containers using the _docker-compose_ command above
* Connect to the wiki webserver with the browser (default localhost:8080)
* Follow the instructions
  * On page 3 provide the database information (default mariadb) and credentials from the _.env_ file
  * On page 5 make sure to select the "Ask me more questions" option
  * On page 6 you can enable extensions. The following are recommended:
    * CategoryTree
    * CiteThisPage
    * Cite
    * CodeEditor
    * ReplaceText
    * VisualEditor
    * WikiEditor
    * ParserFunctions
    * Scribunto
    * Gadgets
    * PdfHandler
    * ReplaceText
    * SyntaxHighlight_GeSHi
    * Math
    * ImageMap
    * MultimediaViewer
  * On the same page enable file uploads in the images section
  * In the end a _LocalSettings.php_ file is created and needs to be downloaded to the local file system
* Copy the _LocalSettings.php_ into the folder with the _docker-compose.yaml_
* Add the following line to the volume definitation of the mediawiki container in the _docker-compose.yaml_

`- ./LocalSettings.php:/var/www/html/LocalSettings.php`

* Restart the container
* If editing a page results into an error message "error contacting the parsoid/restbase server (curl error 7) couldn't connect to server" add the following line to the end of the _LocalSettings.php_ and restart the container:

`$wgCanonicalServer = "http://localhost:80";`
