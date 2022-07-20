# Docker----MySQL安装

## 一、MySQL8.0

### 1、下载镜像

```shell
docker pull mysql:8.0
```

### 2、配置文件

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

### 3、启动MySQL

```
docker run --restart=unless-stopped -d --name mysql8 -v /usr/mysql/conf/my.cnf:/etc/mysql/my.cnf -v /usr/mysql/data:/var/lib/mysql -v /usr/mysql/log:/var/log/mysql  -p 6033:3306 -e MYSQL_ROOT_PASSWORD=123456 mysql:8.0
```

## 二、MySQL5.7

### 1、下载镜像

```
docker pull mysql:5.7
```

### 2、配置文件

```
vi /mydata/mysql/conf/my.cnf

[client]
default-character-set=utf8
[mysql]
default-character-set=utf8
[mysqld]
init_connect='SET collation_connection = utf8_unicode_ci'
init_connect='SET NAMES utf8'
character-set-server=utf8
collation-server=utf8_unicode_ci
skip-character-set-client-handshake
skip-name-resolve




use mysql
ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY '654321';
 flush privileges
```

### 3、启动MySQL

```
# --name指定容器名字 -v目录挂载 -p指定端口映射  -e设置mysql参数 -d后台运行
sudo docker run -p 3306:3306 --name mysql \
-v /mydata/mysql/log:/var/log/mysql \
-v /mydata/mysql/data:/var/lib/mysql \
-v /mydata/mysql/conf:/etc/mysql \
-e MYSQL_ROOT_PASSWORD=123456 \
-d mysql:5.7
####
-v 将对应文件挂载到主机
-e 初始化对应
-p 容器端口映射到主机的端口






docker run --restart=unless-stopped -d --name mysql57 -v /usr/mysql/conf/my.cnf:/etc/mysql/my.cnf -v /usr/mysql/data:/var/lib/mysql -v /usr/mysql/log:/var/log/mysql  -p 6033:3306 -e MYSQL_ROOT_PASSWORD=123456 mysql:5.7
```

