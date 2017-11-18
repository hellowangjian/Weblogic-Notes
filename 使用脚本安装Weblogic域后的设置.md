## 使用脚本安装Weblogic域后的设置

1、 确保配置文件中的里应用端口是否正确。

```
	# grep "port" ./config/config.xml
```

2、 在$WL_HOME/bin/setDomainEnv.sh第362行处，增加设置log4j的配置文件存放路径。

```
	362 LOG4J_CONFIG_FILE="/PATH/TO/log4j.properties"
```

3、 修改Linux上Weblogic使用的jdk $JAVA_HOME/jre/lib/security/java.security 文件。  

```
	将securerandom.source=file:/dev/random   
	修改为：  
	securerandom.source=file:/dev/./urandom

	这样可以解决任何一个域Weblogic启动慢的问题

    针对单个 Weblgoic 域：
    这是SUN,JDK一个bug解决办法是在weblogic启动脚本里setDomainEnv.sh: 加入以下内容
    JAVA_OPTIONS="${JAVA_OPTIONS} -Djava.security.egd=file:/dev/./urandom"
    export JAVA_OPTIONS
```

