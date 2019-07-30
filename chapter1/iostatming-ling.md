### iostat命令—监控IO使用

[Linux iostat命令详解](https://www.jellythink.com/archives/438)

```
语法：
iostat [ -c ] [ -d ] [ -h ] [ -N ] [ -k | -m ] [ -t ] [ -V ] [ -x ] [ -z ] [ device [...] | ALL ] [ -p [ device [,...] | ALL ] ] [ interval [ count ] ]
```

> iostat -d -k 1 2
>
> 参数 -d 表示，显示设备（磁盘）使用状态；-k某些使用block为单位的列强制使用Kilobytes为单位；2表示，数据显示每隔2秒刷新一次。
>
> ![](/assets/import45.png)

![](/assets/import3.png)

iostat -x

![](/assets/import4.png)

iostat -d 2 3

![](/assets/import5.png)

