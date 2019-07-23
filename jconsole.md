### 远程访问：

参考：[配置jconsole远程监视 \(jconsole Remote Monitoring\)](https://www.cnblogs.com/sunxucool/archive/2012/12/18/2823221.html)

> 启动：
>
> java -Djava.rmi.server.hostname=192.168.200.117 -Dcom.sun.management.jmxremote.port=60001 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false -cp ./ com.dreamwin.wowza.monitor.HoldCPUMain

![](/assets/import31.png)

![](/assets/import33.png)

