> 运行class文件

![](/assets/import11.png)

> 执行jps

![](/assets/import12.png)

> 执行pidstat -p 3618 -u 1 3

![](/assets/import13.png)

> 执行pidstat -p 3618 -u 1 3 -t

![](/assets/import14.png)

> 发现是线程id为3636占用CPU

> 导出dump

> jstack -l 3618 &gt; ./t.txt
>
> 发现HoldCPUTask类，它的nid=0xe34，转成十进制正好是3636，即：占用CPU线程。

![](/assets/import16.png)

