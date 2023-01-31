leetcode
1114. 按序打印
https://leetcode.cn/problems/print-in-order/solution/an-xu-da-yin-by-leetcode/

AtomicInteger
```java
class Foo {

  private AtomicInteger firstJobDone = new AtomicInteger(0);
  private AtomicInteger secondJobDone = new AtomicInteger(0);

  public Foo() {}

  public void first(Runnable printFirst) throws InterruptedException {
    // printFirst.run() outputs "first".
    printFirst.run();
    // mark the first job as done, by increasing its count.
    firstJobDone.incrementAndGet();
  }

  public void second(Runnable printSecond) throws InterruptedException {
    while (firstJobDone.get() != 1) {
      // waiting for the first job to be done.
    }
    // printSecond.run() outputs "second".
    printSecond.run();
    // mark the second as done, by increasing its count.
    secondJobDone.incrementAndGet();
  }

  public void third(Runnable printThird) throws InterruptedException {
    while (secondJobDone.get() != 1) {
      // waiting for the second job to be done.
    }
    // printThird.run() outputs "third".
    printThird.run();
  }
}
```

CountDownLatch
```java
class Foo {

    private final CountDownLatch firstDone;
    private final CountDownLatch secondDone;

    public Foo() {
        firstDone = new CountDownLatch(1);
        secondDone = new CountDownLatch(1);
    }

    public void first(Runnable printFirst) throws InterruptedException {
        // printFirst.run() outputs "first". Do not change or remove this line.
        printFirst.run();
        firstDone.countDown();
    }

    public void second(Runnable printSecond) throws InterruptedException {
        firstDone.await();
        // printSecond.run() outputs "second". Do not change or remove this line.
        printSecond.run();
        secondDone.countDown();
    }

    public void third(Runnable printThird) throws InterruptedException {
        secondDone.await();
        // printThird.run() outputs "third". Do not change or remove this line.
        printThird.run();
    }
}
```
Semaphore
```java
    private Semaphore two = new Semaphore(0);
    private Semaphore three = new Semaphore(0);

    public Foo() {

    }

    public void first(Runnable printFirst) throws InterruptedException {

        // printFirst.run() outputs "first". Do not change or remove this line.
        printFirst.run();
        two.release();
    }

    public void second(Runnable printSecond) throws InterruptedException {
        two.acquire();
        // printSecond.run() outputs "second". Do not change or remove this line.
        printSecond.run();
        three.release();
    }

    public void third(Runnable printThird) throws InterruptedException {
        three.acquire();
        // printThird.run() outputs "third". Do not change or remove this line.
        printThird.run();
    }
```

CountDownLatch源码内有两种具体的用法
