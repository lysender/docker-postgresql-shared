# Docker PostgreSQL Shared

Docker compose setup for PostgreSQL with intention of sharing it with multiple projects.

Pgbouncer sits in front of the PostgreSQL database but you can still connect directly
to the database if needed.

Note: This is meant to be used for development/testing machines only as you would likely use a bigger database setup in production like AWS RDS.

## Usage

Copy the `.env-example` file to start using the template. Change the port mapping and root password when necessary.

```
cd /path/to/docker-postgresql-shared
docker-compose up -d
```

## Shell Access

```
psql -h 127.0.0.1 -p 54320 -U postgres -W
```

## Pgbouncer

To use pgbouncer, you need to create a user that you'll use in your project.

Login using psql:

```
psql -h 127.0.0.1 -p 54320 -U postgres -W
```

Create a user and a database.

```
CREATE USER username WITH PASSWORD 'password' SUPERUSER;
CREATE DATABASE project_name;
```

Login using psql:

```
psql -h 127.0.0.1 -p 54320 -U username -W -d project_name
```

Once the login is working, edit `.env` to use the new `POSTGRES_USERNAME` and `POSTGRES_PASSWORD`.

```
docker compose down
docker compose up -d
```

Since we are storing our postgres data into a volume, we should be able to destroy and re-create
the containers and the existing data should still be intact.

Try loggin in using pgbouncer:

```
psql -h 127.0.0.1 -p 64320 -U username -d project_name -W
```

You should be able to login via pgbouncer now.
