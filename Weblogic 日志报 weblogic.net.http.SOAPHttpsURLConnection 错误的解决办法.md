## <center>Weblogic 日志报 weblogic.net.http.SOAPHttpsURLConnection 错误的解决办法</center>

> <http://blog.csdn.net/u014520797/article/details/50263089>

导致 贯众健康应用 微信退款失败，参考以上链接解决：

```
    ~]$ cd /u/home/weblogic/Oracle/Middleware/Oracle_Home/user_projects/domains/domain7017_domain
    domain7017_domain]$ vim ./bin/startWeblogic.sh
    101 JAVA_OPTIONS="${SAVE_JAVA_OPTIONS}"
    改为：
    101 JAVA_OPTIONS="${SAVE_JAVA_OPTIONS} -DUseSunHttpHandler=true"
```

（完）