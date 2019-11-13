# SMF-Docker
Configurable Docker image for SMF

## Requirements
- git
- Docker
- docker-compose

## install

```bash
git clone git@github.com:MissAllSunday/SMF-Docker.git
git clone git@github.com:SimpleMachines/SMF2.1.git smf
```

You can also clone an SMF 2.0 instead if you have access to it.

```bash
cp .env.dist .env
```

Edit your env variables according to your needs, set your external port if you're already using the default provided.

Add smf.local to your hosts
```bash
sudo vim /etc/hosts
```
Add smf.local to 127.0.0.1

```bash
127.0.0.1       localhost smf.local
```

Run

```bash
docker-compose -up -d
```

Might take a while to build on the first try.  
Open http://smf.local:88 (or the port you specified on your `.env file` ) with your fav browser and complete the SMF install process.

Use `smf_mysql as the DB hostname`unless you modified the `CONTAINER_PREFIX` on your `.env var

##### Tested on Mac 10.14.5 and Ubuntu 18.04.3

#### Tips
- http://smf.local:88/info.php shows a `phpinfo();` page
- If you modify anything inside `docker/php/DockerFile` make sure you run `docker-compose build to get the changes.

#### Defaults
- PHP 7.3
- MySQL 5.7






