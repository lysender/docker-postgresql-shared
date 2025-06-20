# Docker PostgreSQL Shared

Docker compose setup for PostgreSQL with intention of sharing it with multiple projects.

Note: This is meant to be used for development/testing machines only as you would likely use a bigger database setup in production like AWS RDS.

## Usage

Copy the `.env.example` file to start using the template. Change the port mapping and root password when necessary.

~~~
cd /path/to/docker-postgresql-shared
sudo docker-compose up -d
~~~

## CLI Access

Note: Using the default configuration.

~~~
mysql --port 3307 --protocol tcp -u root -pdarkstardb
~~~
