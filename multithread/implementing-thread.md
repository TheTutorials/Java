> 订阅 [TheTutorials/Java](https://github.com/TheTutorials/Java) 学习更多 Java 相关的知识

## Java 多线程
Java 本身提供了对多线程的支持，多线程允许并发的执行程序的多个部分，最大成程度的利用 `CPU`，一个进程是由多个线程所组成，因此线程可以看作轻量级进程。

## Java 实现多线程

* 继承 `Thread`
    ``` java
    public static void main(String[] args) {

        /* 创建线程 */
        MyThread firstThread = new MyThread("firstThread");
        MyThread secondThread = new MyThread("secondThread");

        /* 启动线程，当线程获取CPU时间片的时候就会开始运行 */
        firstThread.start();
        secondThread.start();
    }

    static class MyThread extends Thread {
        MyThread(String name) {
            super(name);
        }

        MyThread() {
            super();
        }

        @Override
        public void run() {
            super.run();
            System.out.format("线程%s正在运行，线程id:%d\n",
                    Thread.currentThread().getName(), Thread.currentThread().getId());
        }
    }
    ```
    输出
    ``` bash
    线程secondThread正在运行，线程id:22
    线程firstThread正在运行，线程id:21
    ```

* 实现 `Runnable` 接口 (推荐)
    ``` java
    public static void main(String[] args) {
        Thread firstThread = new Thread(new MyThread(), "firstThread");
        Thread secondThread = new Thread(new MyThread(), "secondThread");

        firstThread.start();
        secondThread.start();
    }

    static class MyThread implements Runnable {
        @Override
        public void run() {
            System.out.format("线程%s正在运行，线程id:%d\n",
                    Thread.currentThread().getName(), Thread.currentThread().getId());
        }
    }
    ```
    输出
    ``` bash
    线程secondThread正在运行，线程id:22
    线程firstThread正在运行，线程id:21
    ```

* 匿名 `Runnable` 类 (Java 8 之前的版本)
    ``` java
    new Thread(new Runnable() {
        @Override
        public void run() {
            new Thread(()-> System.out.format("线程%s正在运行，线程id:%d\n",
                    Thread.currentThread().getName(), Thread.currentThread().getId())).start();
        }
    }).start();
    ```

* Java 8 `lambda` 语法格式实现多线程
    ``` java
    public static void main(String[] args) {
        Thread firstThread = new Thread(()-> System.out.format("线程%s正在运行，线程id:%d\n",
                Thread.currentThread().getName(), Thread.currentThread().getId()));
        firstThread.start();

        new Thread(()-> System.out.format("线程%s正在运行，线程id:%d\n",
                Thread.currentThread().getName(), Thread.currentThread().getId())).start();
    }
    ```

### 使用 `Thread` 还是 `Runnable`
* 如果我们的类继承了 `Thread`，那么将无法继承其他的类,因为 Java 不支持多继承,而当我们实现 `Runnable` 接口还能继续继承其他的类

* 如果继承 `Thread` 类我们可以实现基本的功能，因为 `Thread` 提供类一些内置函数如 `yield()`, `interrupt` 等，这些是实现 `Runnable` 接口没有的功能

## References
1. https://stackoverflow.com/questions/541487/implements-runnable-vs-extends-thread-in-java
