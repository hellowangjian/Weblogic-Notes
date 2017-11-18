## java.lang.OutOfMemoryError: unable to create new native thread
## Cannot create worker GC thread. Out of system resources.

 此问题**可能**是因为 Linux 对普通用户的创建进程数量有限制，默认是 1024 个，可以使用 `ulimit -u` 命令查看。
```BASH
    ~]$ ulimit -u
    1024
```

或者使用`ulimit -a `命令显示所有的 limit 设置值，`max user processes` 的值即是 Linux 对当前用户的进程数量限制。
```BASH
    ~]$ ulimit -a
    core file size          (blocks, -c) 0
    data seg size           (kbytes, -d) unlimited
    scheduling priority             (-e) 0
    file size               (blocks, -f) unlimited
    pending signals                 (-i) 79824
    max locked memory       (kbytes, -l) 64
    max memory size         (kbytes, -m) unlimited
    open files                      (-n) 1024
    pipe size            (512 bytes, -p) 8
    POSIX message queues     (bytes, -q) 819200
    real-time priority              (-r) 0
    stack size              (kbytes, -s) 10240
    cpu time               (seconds, -t) unlimited
    max user processes              (-u) 1024
    virtual memory          (kbytes, -v) unlimited
    file locks                      (-x) unlimited
```

使用 `ps mU USERNAME | wc -l` 命令查看当前用户创建的所有进程数量。
```BASH
    ~]$ ps mU weblogic | wc -l
    82
```

有两个配置文件可以修改系统对用户的进程数量限制：

1. /etc/security/limits.conf
2. /etc/security/limits.d/90-nproc.conf

在其中任何一个文件中加入如下配置即可：
```BASH
    weblogic   soft    nproc    5000
    weblogic   hard    nproc    5000
```

## 完

### Reference：
https://www.cnblogs.com/myshare/archive/2016/02/02/5177135.html
http://cn.linux.vbird.org/linux_basic/0410accountmanager_5.php#limits
https://www.cnblogs.com/pangguoping/p/5792075.html