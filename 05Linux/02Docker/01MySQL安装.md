# Docker----MySQL安装

## 1、下载镜像

```shell
docker pull mysql:8.0
```

## 2、配置文件

```shell
mkdir -p /usr/mysql/conf /usr/mysql/data
chmod -R 755 /usr/mysql/
vim /usr/mysql/conf/my.cnf



[client]

#socket = /usr/mysql/mysqld.sock

default-character-set = utf8mb4

[mysqld]

#pid-file        = /var/run/mysqld/mysqld.pid

#socket          = /var/run/mysqld/mysqld.sock

#datadir         = /var/lib/mysql

#socket = /usr/mysql/mysqld.sock

#pid-file = /usr/mysql/mysqld.pid

datadir = /usr/mysql/data

character_set_server = utf8mb4

collation_server = utf8mb4_bin

secure-file-priv= NULL

# Disabling symbolic-links is recommended to prevent assorted security risks

symbolic-links=0

# Custom config should go here

!includedir /etc/mysql/conf.d/

```

## 3、启动MySQL

```
docker run --restart=unless-stopped -d --name mysql8 -v /usr/mysql/conf/my.cnf:/etc/mysql/my.cnf -v /usr/mysql/data:/var/lib/mysql -v /usr/mysql/log:/var/log/mysql  -p 6033:3306 -e MYSQL_ROOT_PASSWORD=123456 mysql:8.0
```

