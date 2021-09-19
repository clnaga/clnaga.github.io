---
layout: mypost
title: 浅谈 CountDownLatch、Semaphore、CyclicBarrier
categories: [Java]
---



Java并发包中有三个类用于同步一批线程的行为，分别是CountDownLatch、Semaphore和CyclicBarrier。

## CountDownLatch

countDownLatch这个类使一个线程等待其他线程各自执行完毕后再执行。 

是通过一个计数器来实现的，计数器的初始值是线程的数量。每当一个线程执行完毕后，调用 countDown方法，计数器的值就减1，当计数器的值为0时，表示所有线程都执行完毕，然后在等待的线程就可以恢复工作了。 

只能一次性使用，不能reset

由于CountDownLatch有个countDown()方法并且countDown()不会引起阻塞，所以CountDownLatch可以应用于主线程等待所有子线程结束后再继续执行的情况

在某些业务场景中，程序执行需要等待某个条件完成后才能继续执行后续的操作；典型的应用如并行计算，当某个处理的运算量很大时，可以将该运算任务拆分成多个子任务，等待所有的子任务都完成之后，父任务再拿到所有子任务的运算结果进行汇总。

```java
public class Main {
    public static void main(String[] args) throws InterruptedException {
        final CountDownLatch latch = new CountDownLatch(2);
        for (int i = 0; i < 2; i ++) {
            new Thread(new Runnable() {
                @Override
                public void run() {
                    System.out.println(Thread.currentThread().getName() + "start");
                    try {
                        Thread.sleep(1000);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                    System.out.println(Thread.currentThread().getName() + "end");
                    latch.countDown();
                }
            }).start();
        }
        System.out.println("waiting");
        latch.await();
        System.out.println("finish all threads");
    }
}
```

## CyclicBarrier

CyclicBarrier 主要功能和CountDownLatch类似，也是通过一个计数器，使一个线程等待其他线程各自执行完毕后再执行。但是其可以重复使用（reset）

CyclicBarrier也是一个同步辅助类，它允许一组线程相互等待，直到到达某个公共屏障点（common barrier point）。通过它可以完成多个线程之间相互等待，只有当每个线程都准备就绪后，才能各自继续往下执行后面的操作。

### CountDownLatch与CyclicBarrier的区别

- CountDownLatch主要是实现了1个或N个线程需要等待其他线程完成某项操作之后才能继续往下执行操作，描述的是**1个线程或N个线程等待其他线程**的关系。
- CyclicBarrier主要是实现了多个线程之间相互等待，直到所有的线程都满足了条件之后各自才能继续执行后续的操作，描述的**多个线程内部相互等待**的关系。
- CountDownLatch是一次性的，而CyclicBarrier则可以被重置而重复使用。

```java
public static void main(String[] args) {
        CyclicBarrier cyclicBarrier = new CyclicBarrier(3, new Runnable() {
            @Override
            public void run() {
                System.out.println("go");
            }
        });
        for (int i = 0; i < 9; i ++) {
            new Thread(new Runnable() {
                @Override
                public void run() {
                    try {
                        System.out.println(Thread.currentThread().getName() + "start");
                        Thread.sleep(1000);
                        cyclicBarrier.await();
                        System.out.println(Thread.currentThread().getName() + "end");
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    } catch (BrokenBarrierException e) {
                        e.printStackTrace();
                    }
                }
            }).start();
        }
    }
```

## Semaphore

Semaphore可以控制同时访问的线程个数，通过acquire()方法获取一个许可，没有就等待，使用release()释放一个许可

它也被更多地用来**限制流量**，类似阀门的功能。

> 1. acquire()
> 2. acquire(int permits)
> 3. release()
> 4. release(int permits)

```java
public static void main(String[] args) {
    Semaphore semaphore = new Semaphore(5);
    for (int i = 0; i < 5; i ++) {
        new Worker(i, semaphore).start();
    }
}
private static class Worker extends Thread{
    private int num;
    private Semaphore semaphore;
    public Worker(int i, Semaphore semaphore) {
        this.num = num;
        this.semaphore = semaphore;
    }
    @Override
    public void run() {
        semaphore.acquire();
        System.out.println(Thread.currentThread().getName() + "start");
        Thread.sleep(1000);
        System.out.println(Thread.currentThread().getName() + "end");
        semaphore.release();
    }
}
```

## 异同

### 区别

1. CountDownLatch 使一个线程A或是组线程A等待其它线程执行完毕后，一个线程A或是组线程A才继续执行。CyclicBarrier：一组线程使用await()指定barrier，所有线程都到达各自的barrier后，再同时执行各自barrier下面的代码。Semaphore：是用来控制同时访问特定资源的线程数量，它通过协调各个线程，以保证合理的使用公共资源
2. CountDownLatch是减计数方式，计数==0时释放所有等待的线程；CyclicBarrier是加计数方式，计数达到构造方法中参数指定的值时释放所有等待的线程。Semaphore，每次semaphore.acquire()，获取一个资源，每次semaphore.acquire(n)，获取n个资源，当达到semaphore 指定资源数量时就不能再访问线程处于阻塞，必须等其它线程释放资源，semaphore.relase()每次资源一个资源，semaphore.relase(n)每次资源n个资源。
3. CountDownLatch当计数到0时，计数无法被重置；CyclicBarrier计数达到指定值时，计数置为0重新开始。
4. CountDownLatch每次调用countDown()方法计数减一，调用await()方法只进行阻塞，对计数没任何影响；CyclicBarrier只有一个await()方法，调用await()方法计数加1，若加1后的值不等于构造方法的值，则线程阻塞
5. CountDownLatch、CyclikBarrier、Semaphore 都有一个int类型参数的构造方法。CountDownLatch、CyclikBarrier这个值作为计数用，达到该次数即释放等待的线程，而Semaphore 中所有acquire获取到的资源达到这个数，会使得其它线程阻塞。

### 相同

1. CountDownLatch与CyclikBarrier两者的共同点是都具有await()方法，并且执行此方法会引起线程的阻塞，达到某种条件才能继续执行（这种条件也是两者的不同）。Semaphore，acquire方获取的资源达到最大数量时，线程再次acquire获取资源时，也会使线程处于阻塞状态。CountDownLatch与CyclikBarrier两者的共同点是都具有await()方法，并且执行此方法会引起线程的阻塞，达到某种条件才能继续执行（这种条件也是两者的不同）。Semaphore，acquire方获取的资源达到最大数量时，线程再次acquire获取资源时，也会使线程处于阻塞状态。CountDownLatch、CyclikBarrier、Semaphore 都有一个int类型参数的构造方法。
2. CountDownLatch、CyclikBarrier、Semaphore 都有一个int类型参数的构造方法。

> REF: 
>
> [CountDownLatch、CyclicBarrier、Semaphore共同之处与区别](https://blog.csdn.net/jackyechina/article/details/52931453)
>
> [CountDownLatch、Semaphore和CyclicBarrier - 知乎](https://zhuanlan.zhihu.com/p/133076404)

