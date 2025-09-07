# Docker PostgreSQL Shared

Docker compose setup for PostgreSQL with intention of sharing it with multiple projects.

Pgbouncer sits in front of the PostgreSQL database but you can still connect directly
to the database if needed.

Note: This is meant to be used for development/testing machines only as you would likely use a bigger database setup in production like AWS RDS.

## Usage

Copy the `.env-example` file to start using the template. Change the port mapping and root password when necessary.

Copy the `pgbouncer-example.ini` file to configure pgbouncer but you can leave the default values at first.

```
cd /path/to/docker-postgresql-shared
sudo docker-compose up -d
```

## Shell Access

```
psql -h 127.0.0.1 -p 5432 -U postgres -W
```

## Pgbouncer

To use pgbouncer, you need to create a user that you'll use in your project.

Login using psql:

```
psql -h 127.0.0.1 -p 5432 -U postgres -W
```

Create a user and a database.

```
CREATE USER username WITH PASSWORD 'password' SUPERUSER;
CREATE DATABASE project_name;
```

Login using psql:

```
psql -h 127.0.0.1 -p 5432 -U username -W -d project_name
```
