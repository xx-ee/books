# JDK安装

## 1.tar包

```shell
mkdir /usr/local/java
tar -xvf jdk-8u131-linux-x64.tar.gz   -C   /usr/local/java/ 

vi /etc/profile
JAVA_HOME=/usr/local/java/jdk-8u131
PATH=$JAVA_HOME/bin:$PATH
CLASSPATH=$JAVA_HOME/jre/lib/ext:$JAVA_HOME/lib/tools.jar
export PATH JAVA_HOME CLASSPATH

source /etc/profile
java -version
echo $JAVA_HOME
```

## 2.yum

```shell
yum list installed | grep java

yum -y remove java-1.8.0*
yum -y remove tzdata-java.noarch
yum -y remove javapackages-tools.noarch



####安装
yum -y list java*
yum install -y java-1.8.0-openjdk.x86_64
```

