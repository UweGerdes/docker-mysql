# Docker uwegerdes/mysql

This is a special mysql image with a little database for my frontend-development project.

## Building mysql image

If you download the Dockerfile please make sure to include the other files from the github repo before running build.

```bash
$ docker build -t uwegerdes/mysql ./mysql/
```

## Running the mysql container

Run the mysql container in background (-d) with:

```bash
$ docker run -d \
	-e 'MYSQL_ROOT_PASSWORD=123456' \
	--name mysql \
	uwegerdes/mysql
```

The mysql container exposes port 3306 but we don't expose it on the host system. The php-fpm container get's a direct link.

To keep the database on your host you could add `-v /srv/docker/mysql:/var/lib/mysql` to the run command and the database files are stored in `/src/docker/mysql`.

To work with the database exec commands in the running container:

```bash
$ docker exec -i mysql mysql -u root -p123546 demoDb < ./mysql/init_database.sql
$ docker exec -i mysql mysqldump -u root -p123546 demoDb > demoDbDump.sql
$ docker exec -it mysql bash
```
