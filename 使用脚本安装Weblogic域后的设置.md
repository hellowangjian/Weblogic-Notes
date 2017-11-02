## 使用脚本安装Weblogic域后的设置

1、 确保启动脚本和关闭脚本里应用端口是否正确。

```
	# grep "port" ./bin/startWeblogic
	# grep "port" ./bin/stopWeblogic
```

2、 在$WL_HOME/bin/setDomainEnv.sh第362行处，增加设置log4j的配置文件存放路径。

```
	362 LOG4J_CONFIG_FILE="/PATH/TO/log4j.properties"
```

3、 修改Linux上Weblogic使用的jdk $JAVA_HOME/jre/lib/security/java.security 文件。  

```
	将securerandom.source=file:/dev/urandom   
	修改为：  
	securerandom.source=file:/dev/./urandom

	这样可以解决任何一个域Weblogic启动慢的问题
```