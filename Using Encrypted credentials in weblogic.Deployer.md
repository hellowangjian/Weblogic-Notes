## Using Encrypted credentials in weblogic.Deployer

### 参考：
[Using encrypted credentials in WLST](http://theheat.dk/blog/?p=157)

在使用 weblogic.Deployer 实现[使用命令行对 weblogic 进行项目自动发布](http://blog.csdn.net/zlxfogger/article/details/52768360)，但是需要指定用户名和密码，用户名和密码写在脚本中，心好慌。 其实这个用户名和密码可以加密存储在一个文件中，让 weblogic.Deployer 使用时再自行进行解密使用，这样不就安全了吗！

#### 创建包含加密用户名和密码的文件和解密秘钥文件

```BASH
    . /app/oracle/domains/wlsTestDomain/bin/setDomainEnv.sh # 设置环境变量
    java weblogic.WLST  # 执行 WLST 命令
    connect(username='weblogic', password='mypw', url='t3://testwls01:7001') # 登录 weblogic 域
    storeUserConfig(userConfigFile='/app/oracle/scripts/userconfig.secure', userKeyFile='/app/oracle/scripts/userkey.secure', nm='false') # 指定两个文件的保存路径及文件名
```
connect() 和 storeUserConfig() 是 WLST 子命令，在运行 WLST 中使用。

### 在 weblogic.Deployer 中使用
```bash
    java -cp $wlslib/weblogic.jar:$wlslib/wlepool.jar:$wlslib/wleorb.jar weblogic.Deployer -adminurl t3://SERVER_IP:PORT -userConfigFile /app/oracle/scripts/userconfig.secure -userKeyFile /app/oracle/scripts/userkey.secure -name PROJECT_NAME -targets AdminServer -deploy /PATH/TO/XX.war
```
