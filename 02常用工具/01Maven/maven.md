# Maven

## 1.Linux安装

https://mirrors.bfsu.edu.cn/apache/maven/maven-3/

```shell
#解压
tar -zxvf apache-maven-3.5.4-bin.tar.gz

# 在全局配置文件中添加maven环境变量
sudo vi /etc/profile
# 添加配置
export M2_HOME=/usr/local/apache-maven-3.5.4
export PATH=${M2_HOME}/bin:$PATH

#使修改的配置立刻生效
source /etc/profile

#验证安装是否成功
mvn -v

#更换maven源为国内ali源  settings.xml
#在mirrors中添加节点
	<mirror>
	    <id>aliyunmaven</id>
	    <mirrorOf>central</mirrorOf>
	    <name>aliyun maven</name>
	    <url>https://maven.aliyun.com/repository/public </url>
	</mirror>


<!-- 中央仓库1 -->
  <mirror>
      <id>repo1</id>
      <mirrorOf>central</mirrorOf>
      <name>Human Readable Name for this Mirror.</name>
      <url>http://repo1.maven.org/maven2/</url>
  </mirror>
  <!-- 中央仓库2 -->
  <mirror>
      <id>repo2</id>
      <mirrorOf>central</mirrorOf>
      <name>Human Readable Name for this Mirror.</name>
      <url>http://repo2.maven.org/maven2/</url>
  </mirror>



```

## 2、安装本地

```
mvn install:install-file -Dfile=mq-client-open-4.9.2.jar -DgroupId=com.sohu.tv -DartifactId=mq-client-open -Dversion=4.9.2 -Dpackaging=jar

```

