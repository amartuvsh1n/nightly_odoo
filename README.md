# Build Odoo ERP container image from [Docker](https://github.com/odoo/docker.git)

Odoo ERP системийн контейнер дээр ажиллуулах. 

## download dockerfile
```
git clone https://github.com/odoo/docker.git
# choose version you want
cd 16 
```

Replace your odoo version in ODOO_VERSION, ODOO_RELEASE.
If did not found odoo.deb SHA, just remove it. 

```diff
vim Dockerfile
ENV ODOO_VERSION 16.0
ARG ODOO_RELEASE=20230825
ARG ODOO_SHA=12ce0c5d56051d71ec3d9d474b3f4694fdcae45a 
# if not found
&& echo "${ODOO_SHA} odoo.deb" | sha1sum -c - \ 

```

## Create container image
```
docker built -t image_name:tag 
```

## Check error
контейнер лог харах. 
```
docker logs -f odoo
```
Odoo ERP сервис лог харах. Хост серверт байх лог файл контейнер руу mount хийгдээгүй бол контейнер дотроос харах(заавал асаалттай үед харна).  
```
$ tail -f ./odoo_log/odoo.log 
 
# Хэрэв контейнер унтарсан бол асаасны дараа лог харна
$ docker start odoo 
$ docker exec odoo 'cat /var/log/odoo/odoo.log' 
```
