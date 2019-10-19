# SMF-Docker
Configurable Docker image for SMF

## install

```bash
git clone git@github.com:MissAllSunday/SMF-Docker.git
git clone git@github.com:SimpleMachines/SMF2.1.git smf
cd smf
cp other/{install.php,Settings.php,install_2-1_mysql.sql} .
sudo vim /etc/hosts
```
Add smf.local to 127.0.0.1

```bash
127.0.0.1       localhost smf.local
```

```bash
cp .env.dist .env
```
Edit your env variables

```bash
cd docker
docker login
docker-compose -up -d
```

Open smf.local with your fav browser





