# symfony-angular-docker-compose
Docker compose for symfony + angular project

Setup
-----
1) Clone this repository
```bash
$ git clone https://github.com/zhooravell/symfony-angular-docker-compose.git
```
2) Create `.env` file
```bash
$ cd symfony-angular-docker-compose && cp env.dist .env
```
3) Set value to environment variables in `.env`
```
SYMFONY_APP=/absolute/path/to/symfony/app
ANGULAR_APP=/absolute/path/to/angular/app
```
4) Fixing file permissions in Symfony App ([Official documentation][symfony-fix-permissions-link])
```bash
// For Linux
$ HTTPDUSER=$(ps axo user,comm | grep -E '[a]pache|[h]ttpd|[_]www|[w]ww-data|[n]ginx' | grep -v root | head -1 | cut -d\  -f1)
$ sudo setfacl -dR -m u:"$HTTPDUSER":rwX -m u:$(whoami):rwX var
$ sudo setfacl -R -m u:"$HTTPDUSER":rwX -m u:$(whoami):rwX var
```
5) Prepare docker
```bash
$ docker-compose pull
$ docker-compose build --force-rm
$ docker volume create --name=mysql-data
```
6) Check docker config
```bash
$ docker-compose config
```
Usage
-----
Run development environment
```bash
$ docker-compose up
```
or run in background
```bash
$ docker-compose up -d
```
To down environment
```bash
$ docker-compose down
```
Useful
------
Show all container
```bash
$ docker-compose ps
```
Connect to container
```bash
$ docker exec -it {container_name} bash
```
Fix minor problem with docker images
```bash
$ docker-compose up --force-recreate
```

Access to projects
------------------
Symfony: http://symfony-app.dev

Angular: http://localhost:4200

Phpmyadmin: http://localhost:3000

[symfony-fix-permissions-link]: http://symfony.com/doc/current/setup/file_permissions.html