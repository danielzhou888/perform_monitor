### pidstat—诊断工具

准备测试DEMO

```
package com.dreamwin.wowza.monitor;

/**
 * <p><em>Copyright:</em> All Rights Reserved</p>
 * <p><em>Company:</em> 创盛视联数码科技（北京）有限公司   https://www.bokecc.com/</p>
 *
 * @author Daniel Zhou / zzx
 **/
public class HoldCPUMain {
    public static class HoldCPUTask implements Runnable {

        @Override
        public void run() {
            while (true) {
                double a = Math.random()*Math.random();
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
        new Thread(new HoldCPUTask()).start();
        new Thread(new LazyTask()).start();
        new Thread(new LazyTask()).start();
        new Thread(new LazyTask()).start();
    }

}
```

> 运行class文件

![](/assets/import11.png)

> 执行jps

![](/assets/import12.png)

> 执行pidstat -p 3618 -u 1 3

![](/assets/import13.png)

> 执行pidstat -p 3618 -u 1 3 -t

![](/assets/import14.png)

> 发现是线程id为3636占用CPU
>
> 导出dump
>
> jstack -l 3618 &gt; ./t.txt
>
> 发现HoldCPUTask类，它的nid=0xe34（十六进制），转成十进制正好是3636，即：占用CPU线程。

![](/assets/import16.png)



