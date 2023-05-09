# Repo Purpose
Example of db-backup tool with mongoDB.
https://github.com/tiredofit/docker-db-backup

# Steps to Run
## Run Docker Compose
- Run docker compose using `docker-compose up`

It would take a few seconds to start all services and run the mongo Express. You can proceed to the next step once all containers are running.

## Create Database and Add Data
The docker compose includes mongo Express, a web interface to mongoDB. This can be accessed in a browser by navigating to `localhost:8081`. Create a DB called "my-db", a collection with any name and add some data to it.

## Create a Manual Backup
Create a manual backup by entering the docker container terminal/shell and typing 
`backup-now`

## Restore to a Different Database
**Restore Command Syntax**: 
`restore <filename> <db_type> <db_hostname> <db_name> <db_user> <db_pass> <db_port>`

Use below command in docker container terminal/shell to restore the backed up database 'my-db':
`restore "" mongo mongo "" "" "" 27017`

This would now prompt for the backup to be restored, which will showup as a list. Use the latest database backup by choosing the corresponding number.

For user name and password, leave them blank and press Enter.

The core restore command being used is:
`mongorestore ${mongo_compression} -d=${r_dbname} -h=${r_dbhost} --port=${r_dbport} ${mongo_user} ${mongo_pass} --archive=${r_filename}`

Example:
`mongorestore --gzip -h=mongo --port=27017 "" "" --archive=mongo_all_mongo_20230509-101500.archive.gz`
`mongorestore --gzip -d=my-db-1 -h=mongo --port=27017 "" "" --archive=mongo_all_mongo_20230509-101500.archive.gz`
