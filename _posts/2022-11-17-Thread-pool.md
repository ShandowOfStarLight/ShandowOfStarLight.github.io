---
title: Java 线程池
author: kai
date: 2022-11-17
category: spring
layout: post
---

## 线程池的创建

### Executors Executor 和 ExecutorService

Executor接口定义了方法
{% highlight Java %}

public interface Executor {

    /**
     * Executes the given command at some time in the future.  The command
     * may execute in a new thread, in a pooled thread, or in the calling
     * thread, at the discretion of the {@code Executor} implementation.
     *
     * @param command the runnable task
     * @throws RejectedExecutionException if this task cannot be
     * accepted for execution
     * @throws NullPointerException if command is null
     */
    void execute(Runnable command);
}

{% endhighlight %}

ExecutorService继承了Executor

使用方法
{% highlight Java %}

Executor executor = Executors.newSingleThreadExecutor();
executor.execute(() -> log.info("in Executor"))

ExecutorService executorService = Executors.newCachedThreadPool();
executorService.submit(()->log.info("in ExecutorService"))
executorService.shutdown();

{% endhighlight %}

### ThreadPoolExecutor

ThreadPoolExecutor是ExecutorService接口的一个实现。

ThreadPoolExectuor创建
{% highlight Java %}

    ThreadPoolExecutor threadPoolExecutor =
            new ThreadPoolExecutor(1, 1, 0L, TimeUnit.MILLISECONDS,new LinkedBlockingQueue<Runnable>());
    threadPoolExecutor.submit(()->log.info("submit through threadPoolExecutor"));
    threadPoolExecutor.shutdown();

{% endhighlight %}

### 线程池参数说明

#### corePoolSize

核心池的大小，如果调用了prestartAllCoreThreads()或者prestartCoreThread()方法，会直接预先创建corePoolSize的线程，否则当有任务来之后，就会创建一个线程去执行任务，当线程池中的线程数目达到corePoolSize后，就会把到达的任务放到缓存队列当中；这样做的好处是，如果任务量很小，那么甚至就不需要缓存任务，corePoolSize的线程就可以应对；

#### maximumPoolSize

线程池最大线程数，表示在线程池中最多能创建多少个线程，如果运行中的线程超过了这个数字，那么相当于线程池已满，新来的任务会使用RejectedExecutionHandler 进行处理；

#### keepAliveTime

表示线程没有任务执行时最多保持多久时间会终止，然后线程池的数目维持在corePoolSize 大小；

#### unit

参数keepAliveTime的时间单位；

#### workQueue

一个阻塞队列，用来存储等待执行的任务，如果当前对线程的需求超过了corePoolSize大小，才会放在这里；

#### threadFactory

线程工厂，主要用来创建线程，比如可以指定线程的名字；

#### handler

如果线程池已满，新的任务的处理方式（饱和策略）

### 饱和策略

#### ThreadPoolExecutor.AbortPolicy

处理程序遭到拒绝将抛出运行时RejectedExecutionException。

#### ThreadPoolExecutor.CallerRunsPolicy

线程调用运行该任务的execute本身。此策略提供简单的反馈控制机制，能够减缓新任务的提交速度。

#### ThreadPoolExecutor.DiscardPolicy

不能执行的任务将被删除。

#### ThreadPoolExecutor.DiscardOldestPolicy

如果执行程序尚未关闭，则位于工作队列头部的任务将被删除，然后重试执行程序（如果再次失败，则重复此过程）
