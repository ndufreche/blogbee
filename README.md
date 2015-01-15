##BlogBee

BackBee is an open source Content Management System (CMS) project built on top of Symfony Components and Doctrine 2.

This tutorial describe the creation of real web application, we will say more on day 2 about the application and features we expect to be implemented. This kind of site is very popular and very easy to build with BackBee CMS, for instance you should take a look at Medium.

This goal is to demonstrate that BackBee can be used to make websites with style and little efforts.

Each day of this tutorial is meant to last between one and two hours, and will be the occasion to learn BackBee by coding a real website, from start to finish. Every day, new features will be added to the application, and we'll take advantage of this development to introduce you to new BackBee functionalities as well as good practices in web development.

This tutorial is also inspired from so famous Jobeet, the book to learn symfony 1.x which describe how to build a business jobs application.


##How to start ?

There is two way to do this toturial.


###Basic way:

Go on [tutorial](https://backbee.github.io/blogbee) and follow each step one before other.


###Start from a custom day:
:warning: Never follow this install mode too set an BackBee web site in production mode. Use this unsecured installation method only for trainning.

:warning: This tutorial follow linux shell command line style and most of this command are unvailable in window shell

:warning: Be shure, that all prerequisites are in place, if you don't know watch [day1 tutorial](https://backbee.github.io/blogbee/day1.html).

####Start by clone this repo.
```shell
git clone https://github.com/backbee/blogbee.git
cd blogbee
```

Checkout the day from how you want start
```shell
git checkout tag/day{day number}
```

####Install dependencies

```shell
composer install
```

####Create the cache and log folder
```shell
mkdir -m 777 cache/ log/
```


####Edit bootstrap.yml and doctrine.yml in repository/Config folder

In boostrap.yml you have to specify your container folder. In the most of case we basicly dump the container in the cache folder.

:warning: The dump directory accept only absolute path.

```yml
debug: true

# container configuration
container:
    dump_directory: /path/to/your/site/cache
    autogenerate: true
```

In the doctrine.yml specify your database access
```yml
dbal:
    driver: pdo_mysql
    host: localhost
    port: 3306
    dbname: blogbee
    user: root
    password: ~
    charset: utf8
    collation: utf8_general_ci
    defaultTableOptions:
        collate: utf8_general_ci
        engine: InnoDB
        charset: utf8
```

####Create your database in MySQL or MariaDB
```shell
mysql -u root -p
```
```sql
CREATE DATABASE `blogbee` CHARACTER SET utf8 COLLATE utf8_general_ci;

exit;
```

Import the blogbee database
```shell
mysql -u root -p -b blogbee < /path/to/your/site/dump/site.sql
```

Before the Day 4 you have to load the fixtures
```
404 command missing
```

####Configure your vhost in apache2 or nginx
:warning: Don't forget to set "127.0.0.1   blogbee.dev" into your host.

nginx configuration
```
server {
    listen 80;

    server_name blogbee.dev;
    root /path/to/your/site/public/;

    error_log /var/log/nginx/blogbee.error.log;
    access_log /var/log/nginx/blogbee.access.log;

    location ~ /resources/(.*) {
        alias /var/www/html/truc/;
        try_files /BackBuilder/Resources/$1 /repository/Resources/$1 break;
    }

    location ~ /(css|fonts|img)/(.*) {
        try_files $uri @rewriteapp;
    }

    location @rewriteapp {
        rewrite ^(.*)$ /index.php last;
    }

    location ~ ^/(config|index)\.php(/|$) {
        fastcgi_pass unix:/var/run/php5-fpm.sock;
        include fastcgi_params;
    }
}
```

apache2 configuration
```xml
<VirtualHost *:80>
    ServerName blogbee.dev
    DocumentRoot /path/to/your/site/public/
    RewriteEngine On

    RewriteCond %{DOCUMENT_ROOT}/../repository/Resources/$1 -f
    RewriteRule ^/resources/(.*)$ %{DOCUMENT_ROOT}/../repository/Resources/$1 [L]

    RewriteCond %{DOCUMENT_ROOT}/../BackBuilder/Resources/$1 -f
    RewriteRule ^/resources/(.*)$ %{DOCUMENT_ROOT}/../BackBuilder/Resources/$1 [L]

    RewriteCond %{DOCUMENT_ROOT}/../repository/Data/Storage/$1/$2.$4 -f
    RewriteRule ^/images/([a-f0-9]{3})/([a-f0-9]{29})/(.*)\.([^\.]+)$ %{DOCUMENT_ROOT}/../repository/Data/Storage/$1/$2.$4 [L]

    RewriteCond %{DOCUMENT_ROOT}/../repository/Data/Media/$1/$2.$4 -f
    RewriteRule ^/images/([a-f0-9]{3})/([a-f0-9]{29})/(.*)\.([^\.]+)$ %{DOCUMENT_ROOT}/../repository/Data/Media/$1/$2.$4 [L]

    RewriteCond %{DOCUMENT_ROOT}/../repository/Data/Storage/$1 -f
    RewriteRule ^images/(.*)$ %{DOCUMENT_ROOT}/../repository/Data/Storage/$1 [L]

    RewriteCond %{DOCUMENT_ROOT}/../repository/Data/Media/$1 -f
    RewriteRule ^images/(.*)$ %{DOCUMENT_ROOT}/../repository/Data/Media/$1 [L]
</VirtualHost>
```
