# RocketMQ

## 一、Linux安装

https://archive.apache.org/dist/rocketmq/

### 1.解压

```
unzip rocketmq-all-4.9.2-bin-release.zip
```

### 2.修改启动配置

修改目录rocketmq-4.9.2/bin下的配置文件： runserver.sh、runbroker.sh不然会报insufficient memory
**修改runserver.sh 中原有内存配置，更改为**

```
JAVA_OPT="${JAVA_OPT} -server -Xms256m -Xmx256m -Xmn512m -XX:MetaspaceSize=128m -XX:MaxMetaspaceSize=320m"
```

**修改runbroker.sh 中原有内存配置，更改为**

```
JAVA_OPT="${JAVA_OPT} -server -Xms256m -Xmx256m -Xmn128m"
```

修改rocketmq-4.9.2/conf/broker.conf文件，添加配置

```
namesrvAddr=192.168.50.10:9876
brokerIP1=192.168.50.10
```

### 3.启动

进入rocketmq-4.9.2，启动 NameServer

```
nohup sh bin/mqnamesrv &
```

进入rocketmq-4.9.2，启动 Broker

```shell
#启动命令，192.168.50.10:9876为namesrv的IP和端口，保证地址以及端口能够访问。并且指定配置文件启动
nohup sh bin/mqbroker -n 192.168.50.10:9876 -c ./conf/broker.conf &
```

### 4.修改默认端口

#### 4.1 namesrv端口

修改namesrv默认端口（默认9876）

在rocketmq的conf目录下添加namesrv.properties文件，文件中添加端口配置

```
listenPort=8876
```

使用配置信息后台启动namesrv

```
nohup sh bin/mqnamesrv -c conf/namesrv.properties &
```

#### 4.2 broker端口

修改broker默认端口（默认10911）

```
brokerClusterName = DefaultCluster
brokerName = broker-a
brokerId = 0
deleteWhen = 04
fileReservedTime = 48
brokerRole = ASYNC_MASTER
flushDiskType = ASYNC_FLUSH
# 新增的配置，broker默认端口
namesrvAddr=192.168.50.10:8876
brokerIP1=192.168.50.10
listenPort=8911

```

使用配置信息后台启动broker

```
nohup sh bin/mqbroker -n localhost:8876 -c conf/broker.conf &
```





