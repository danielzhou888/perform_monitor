### 远程访问：

参考：[配置jconsole远程监视 \(jconsole Remote Monitoring\)](https://www.cnblogs.com/sunxucool/archive/2012/12/18/2823221.html)

> 启动：
>
> java -Djava.rmi.server.hostname=192.168.200.117 -Dcom.sun.management.jmxremote.port=60001 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false -cp ./ com.dreamwin.wowza.monitor.HoldCPUMain

#### 建立远程连接

![](/assets/import36.png)

![](/assets/import31.png)

![](/assets/import33.png)

#### 内存监测

可以看到，随着程序的运行，Eden Space会逐渐变满，到100%之后，Eden Space会变成0%，Survivor Space会变大；Survivor Space变100%之后，会挪到Tenured Gen中，Survivor Space变0%。这个过程和上面讲到的GC过程是一样的，很直观。

也可以观察上面的曲线图，Eden Space的图是类似波形图，每次到波谷都是进行了一次GC。Tenured Gen则是类似梯田，一直向上涨，直到内存溢出。如下两张图所示。

![](/assets/import35.png)

![](/assets/import34.png)

#### 检测死锁

![](/assets/import37.png)



