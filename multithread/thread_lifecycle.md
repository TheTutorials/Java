> 订阅 [TheTutorials/Java](https://github.com/TheTutorials/Java) 学习更多 Java 相关的知识

# 线程的生命周期

![线程的生命周期](../images/threadLife_cycle.jpg)

<details>
  <summary>Thread.State</summary>

```java
public enum State {
    /**
     * Thread state for a thread which has not yet started.
     */
    NEW,

    /**
     * Thread state for a runnable thread.  A thread in the runnable
     * state is executing in the Java virtual machine but it may
     * be waiting for other resources from the operating system
     * such as processor.
     */
    RUNNABLE,

    /**
     * Thread state for a thread blocked waiting for a monitor lock.
     * A thread in the blocked state is waiting for a monitor lock
     * to enter a synchronized block/method or
     * reenter a synchronized block/method after calling
     * {@link Object#wait() Object.wait}.
     */
    BLOCKED,

    /**
     * Thread state for a waiting thread.
     * A thread is in the waiting state due to calling one of the
     * following methods:
     * <ul>
     *   <li>{@link Object#wait() Object.wait} with no timeout</li>
     *   <li>{@link #join() Thread.join} with no timeout</li>
     *   <li>{@link LockSupport#park() LockSupport.park}</li>
     * </ul>
     *
     * <p>A thread in the waiting state is waiting for another thread to
     * perform a particular action.
     *
     * For example, a thread that has called {@code Object.wait()}
     * on an object is waiting for another thread to call
     * {@code Object.notify()} or {@code Object.notifyAll()} on
     * that object. A thread that has called {@code Thread.join()}
     * is waiting for a specified thread to terminate.
     */
    WAITING,

    /**
     * Thread state for a waiting thread with a specified waiting time.
     * A thread is in the timed waiting state due to calling one of
     * the following methods with a specified positive waiting time:
     * <ul>
     *   <li>{@link #sleep Thread.sleep}</li>
     *   <li>{@link Object#wait(long) Object.wait} with timeout</li>
     *   <li>{@link #join(long) Thread.join} with timeout</li>
     *   <li>{@link LockSupport#parkNanos LockSupport.parkNanos}</li>
     *   <li>{@link LockSupport#parkUntil LockSupport.parkUntil}</li>
     * </ul>
     */
    TIMED_WAITING,

    /**
     * Thread state for a terminated thread.
     * The thread has completed execution.
     */
    TERMINATED;
}
```
</details>

* NEW

  尚未启动的线程处于此状态。
  ``` java
  Thread thread = new Thread(() -> {
      /* do something */
  });
  /* output: NEW */
  System.out.println(thread.getState());
  ```
* RUNNABLE
  
  在Java虚拟机中执行的线程处于这种状态。
  ``` java
  Thread thread = new Thread(() -> {
      /* do something */
  });
  thread.start();
  /* output: RUNNABLE */
  System.out.println(thread.getState());
  ```
* BLOCKED

  等待监视器锁定而被阻塞的线程处于此状态。
  ``` java
  public static void main(String[] args) throws InterruptedException {
      Thread thread1 = new Thread(new MyRunnable());
      Thread thread2 = new Thread(new MyRunnable());

      thread1.start();
      thread2.start();

      Thread.sleep(1000);
      
      /* output: BLOCKED */
      System.out.println(thread2.getState());
      System.exit(0);
  }

  static class MyRunnable implements Runnable {
      @Override
      public void run() {
          doWork();
      }

      public static synchronized void doWork() {
          while (true) {
              /* do something */
          }
      }
  }
  ```
* WAITING

  无限期地等待另一个线程执行特定操作的线程处于此状态。
* TIMED_WAITING
  
  正在等待另一个线程执行操作的线程最多达到指定的等待时间，该线程处于此状态。
  ``` java
  Thread thread = new Thread(() -> {
      try {
          Thread.sleep(5000);
      } catch (InterruptedException e) {
          e.printStackTrace();
      }
  });
  thread.start();

  Thread.sleep(1000);

  /* output: TIMED_WAITING */
  System.out.println(thread.getState());
  ```
* TERMINATED

  退出的线程处于此状态。
  ``` java
  Thread thread = new Thread(() -> {
      /* do something */
  });
  thread.start();

  Thread.sleep(1000);

  assert !thread.isAlive();

  /* output: TERMINATED */
  System.out.println(thread.getState());
  ```

在给定的时间点，线程只能处于一种状态。这些状态是虚拟机状态，不反映任何操作系统线程状态。


