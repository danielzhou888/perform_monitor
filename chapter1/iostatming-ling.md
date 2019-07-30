## iostat命令—监控IO使用

[Linux iostat命令详解](https://www.jellythink.com/archives/438)

### 语法

```
语法：
iostat [ -c ] [ -d ] [ -h ] [ -N ] [ -k | -m ] [ -t ] [ -V ] [ -x ] [ -z ] [ device [...] | ALL ] [ -p [ device [,...] | ALL ] ] [ interval [ count ] ]
```

> 通过iostat方便查看CPU、网卡、tty设备、磁盘、CD-ROM 等等设备的活动情况, 负载信息。

### 命令参数

* C 显示CPU使用情况

* -d 显示磁盘使用情况

* -k 以 KB 为单位显示

* -m 以 M 为单位显示

* -N 显示磁盘阵列\(LVM\) 信息

* -n 显示NFS 使用情况
* -p\[磁盘\] 显示磁盘和分区的情况
* -t 显示终端和CPU的信息
* -x 显示详细信息
* -V 显示版本信息

### 显示所有设备负载情况

> iostat

![](/assets/import48.png)

cpu属性值说明：

* %user：CPU处在用户模式下的时间百分比。
* %nice：CPU处在带NICE值的用户模式下的时间百分比。
* %system：CPU处在系统模式下的时间百分比。
* **%iowait：CPU等待输入输出完成时间的百分比。**
* %steal：管理程序维护另一个虚拟处理器时，虚拟CPU的无意识等待时间百分比。
* **%idle：CPU空闲时间百分比。**

**注意：**如果%iowait的值过高，表示硬盘存在I/O瓶颈，%idle值高，表示CPU较空闲，如果%idle值高但系统响应慢时，有可能是CPU等待分配内存，此时应加大内存容量。%idle值如果持续低于10，那么系统的CPU处理能力相对较低，表明系统中最需要解决的资源是CPU。

### -d与-k

> iostat -d -k 1 2
>
> 参数 -d 表示，显示设备（磁盘）使用状态；-k某些使用block为单位的列强制使用Kilobytes为单位；2表示，数据显示每隔2秒刷新一次。

![](/assets/import45.png)

**输出信息含义：**

```
tps：该设备每秒的传输次数（Indicate the number of transfers per second that were issued to the device.）。"一次传输"意思是"一次I/O请求"。多个逻辑请求可能会被合并为"一次I/O请求"。"一次传输"请求的大小是未知的。

kB_read/s：每秒从设备（drive expressed）读取的数据量；
kB_wrtn/s：每秒向设备（drive expressed）写入的数据量；
kB_read：读取的总数据量；
kB_wrtn：写入的总数量数据量；这些单位都为Kilobytes。
```

> 指定监控的设备名称为sda，该命令的输出结果和上面命令完全相同。

![](/assets/import46.png)

### -x

> iostat还有一个比较常用的选项**-x**，该选项将用于显示和io相关的扩展数据
>
> iostat -x -d -k 1 2

![](/assets/import47.png)

**输出信息含义：**

```
rrqm/s：每秒这个设备相关的读取请求有多少被Merge了（当系统调用需要读取数据的时候，VFS将请求发到各个FS，如果FS发现不同的读取请求读取的是相同Block的数据，FS会将这个请求合并Merge）；wrqm/s：每秒这个设备相关的写入请求有多少被Merge了。

rsec/s：每秒读取的扇区数；
wsec/：每秒写入的扇区数。
rKB/s：The number of read requests that were issued to the device per second；
wKB/s：The number of write requests that were issued to the device per second；
avgrq-sz 平均请求扇区的大小
avgqu-sz 是平均请求队列的长度。毫无疑问，队列长度越短越好。    
await：  每一个IO请求的处理的平均时间（单位是微秒毫秒）。这里可以理解为IO的响应时间，一般地系统IO响应时间应该低于5ms，如果大于10ms就比较大了。
         这个时间包括了队列时间和服务时间，也就是说，一般情况下，await大于svctm，它们的差值越小，则说明队列时间越短，反之差值越大，队列时间越长，说明系统出了问题。
svctm    表示平均每次设备I/O操作的服务时间（以毫秒为单位）。如果svctm的值与await很接近，表示几乎没有I/O等待，磁盘性能很好，如果await的值远高于svctm的值，则表示I/O队列等待太长，         系统上运行的应用程序将变慢。
%util： 在统计时间内所有处理IO时间，除以总共统计时间。例如，如果统计间隔1秒，该设备有0.8秒在处理IO，而0.2秒闲置，那么该设备的%util = 0.8/1 = 80%，所以该参数暗示了设备的繁忙程度
。一般地，如果该参数是100%表示设备已经接近满负荷运行了（当然如果是多磁盘，即使%util是100%，因为磁盘的并发能力，所以磁盘使用未必就到了瓶颈）。
```

iostat -d 2 3

![](/assets/import5.png)

