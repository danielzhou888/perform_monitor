## iostat命令—监控IO使用

[Linux iostat命令详解](https://www.jellythink.com/archives/438)

### 语法

```
语法：
iostat [ -c ] [ -d ] [ -h ] [ -N ] [ -k | -m ] [ -t ] [ -V ] [ -x ] [ -z ] [ device [...] | ALL ] [ -p [ device [,...] | ALL ] ] [ interval [ count ] ]
```

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

iostat -d 2 3

![](/assets/import5.png)

