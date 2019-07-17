### pidstat—I/O监控

准备测试DEMO

```
package com.dreamwin.wowza.monitor;

import java.io.*;

/**
 * <p><em>Copyright:</em> All Rights Reserved</p>
 * <p><em>Company:</em> 创盛视联数码科技（北京）有限公司   https://www.bokecc.com/</p>
 *
 * @author Daniel Zhou / zzx
 **/
public class HoldIOMain {
    public static class HoldIOTask implements Runnable {

        @Override
        public void run() {
            while (true) {
                try {
                    FileOutputStream fos = new FileOutputStream(new File("zhouzhixiang.log"));
                    for (int i = 0; i < 100000; i++) {
                        fos.write(i);
                    }
                    fos.close();
                    FileInputStream fis = new FileInputStream(new File("zhouzhixiang.log"));
                    while (fis.read() != -1);
                } catch (FileNotFoundException e) {
                    e.printStackTrace();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }

    public static class LazyTask implements Runnable {

        @Override
        public void run() {
            while (true) {
                try {
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }
    }

    public static void main(String[] args) {
        new Thread(new HoldIOTask()).start();
        new Thread(new LazyTask()).start();
        new Thread(new LazyTask()).start();
        new Thread(new LazyTask()).start();
    }

}
```

> 运行class文件

![](/assets/import17.png)

> 执行jps

![](/assets/import18.png)

> 执行pidstat -p 3922 -d -t 1 3

![](/assets/import19.png)

> 发现是线程id为3940占比磁盘I/O
>
> 导出dump
>
> jstack -l 3922 &gt; ./tiovi.txt
>
> 发现HoldIOTask类，它的nid=0xf64（十六进制），转成十进制正好是3940，即：占用CPU线程。

![](/assets/import20.png)



