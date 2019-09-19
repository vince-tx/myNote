# CountDownLatch、CyclicBarrier、Semaphore的使用
## CountDownLatch（计数器）
主线程等待另外三个线程执行完成后再执行
```
public static void main(String[] args) {
    //定义一个CountDownLatch
    CountDownLatch countDownLatch = new CountDownLatch(3);
    // 主线程等待另外三个线程执行完成后再执行
    new Thread(() -> {
        try {
            System.out.println("开始执行01");
            Thread.sleep(3000);
            System.out.println("执行完成01");
            countDownLatch.countDown();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }).start();

    new Thread(() -> {
        try {
            System.out.println("开始执行02");
            Thread.sleep(3000);
            System.out.println("执行完成02");
            countDownLatch.countDown();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }).start();

    new Thread(() -> {
        try {
            System.out.println("开始执行03");
            Thread.sleep(3000);
            System.out.println("执行完成03");
            countDownLatch.countDown();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }).start();

    try {
        System.out.println("等待3个线程执行完毕。。。");
        countDownLatch.await();
        System.out.println("主线程开始执行");
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
}

```

## CyclicBarrier（回环栅栏）
三个线程互相等待await执行完成后继续执行
```
public static void main(String[] args) {
    CyclicBarrier cyclicBarrier = new CyclicBarrier(3);

    // 三个线程互相等待await执行完成后继续执行
    new Thread(() -> {
        try {
            System.out.println("开始执行01");
            Thread.sleep(3000);
            System.out.println("执行完成01");
            cyclicBarrier.await();
        } catch (InterruptedException e) {
            e.printStackTrace();
        } catch (BrokenBarrierException e) {
            e.printStackTrace();
        }
        System.out.println(Thread.currentThread().getName()+"所有线程执行完毕，继续处理其他任务...");
    }).start();

    new Thread(() -> {
        try {
            System.out.println("开始执行02");
            Thread.sleep(3000);
            System.out.println("执行完成02");
            cyclicBarrier.await();
        } catch (InterruptedException e) {
            e.printStackTrace();
        } catch (BrokenBarrierException e) {
            e.printStackTrace();
        }
        System.out.println(Thread.currentThread().getName()+"所有线程执行完毕，继续处理其他任务...");
    }).start();

    new Thread(() -> {
        try {
            System.out.println("开始执行03");
            Thread.sleep(3000);
            System.out.println("执行完成03");
            cyclicBarrier.await();
        } catch (InterruptedException e) {
            e.printStackTrace();
        } catch (BrokenBarrierException e) {
            e.printStackTrace();
        }
        System.out.println(Thread.currentThread().getName()+"所有线程执行完毕，继续处理其他任务...");
    }).start();

}

```
## Semaphore（信号量）

8个工人使用5台机器

```

public class Test {
    public static void main(String[] args) {
        int N = 8;            //工人数
        Semaphore semaphore = new Semaphore(5); //机器数目
        for(int i=0;i<N;i++)
            new Worker(i,semaphore).start();
    }

    static class Worker extends Thread{
        private int num;
        private Semaphore semaphore;
        public Worker(int num,Semaphore semaphore){
            this.num = num;
            this.semaphore = semaphore;
        }

        @Override
        public void run() {
            try {
                semaphore.acquire();
                System.out.println("工人"+this.num+"占用一个机器在生产...");
                Thread.sleep(2000);
                System.out.println("工人"+this.num+"释放出机器");
                semaphore.release();           
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```

## 总结
* CountDownLatch用作某个线程等待其他的线程执行完成后，它才执行。
* CyclicBarrier用作一组线程等待到某个状态，然后这组线程才继续执行。
* CountDownLatch是不能够重用的，而CyclicBarrier是可以重用的。
* Semaphore类似于锁，对资源访问权限控制。