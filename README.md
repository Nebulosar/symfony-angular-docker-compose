# symfony-angular-docker-compose
Docker compose for symfony + mysql + angular project

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
7) Add `symfony-app.dev` to `/etc/hosts` 
```
127.0.0.1   symfony-app.dev
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

Hacks
-----
For correct work with angular app you must fix `package.json`
```
"scripts": {
    "ng": "ng",
    "start": "ng serve --host 0.0.0.0",
    ....
```

Access to projects
------------------
Symfony: http://symfony-app.dev

Angular: http://localhost:4200

Phpmyadmin: http://localhost:3000

[symfony-fix-permissions-link]: http://symfony.com/doc/current/setup/file_permissions.html