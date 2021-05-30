
# 写三个线程，循环打印出`A`、`B`、`C`
1、使用原始的`wait`、`notify`方法来实现
```java 
    private static class MyThread extends Thread {
        private String name;
        private final Object prev;
        private final Object self;

        public MyThread(String name, Object prev, Object self) {
            this.name = name;
            this.prev = prev;
            this.self = self;
        }

        @Override
        public void run() {
            while (true) {
                synchronized (prev) {
                    synchronized (self) {
                        System.out.println(name);

                        self.notify();
                    }
                    try {
                        // 存在虚假唤醒的可能性
                        prev.wait();
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
            }
        }
    }

    public static void main(String[] args) throws InterruptedException {
        Object a = new Object();
        Object b = new Object();
        Object c = new Object();

        Thread aThread = new MyThread("A", c, a);
        Thread bThread = new MyThread("B", a, b);
        Thread cThread = new MyThread("C", b, c);

        aThread.start();
        Thread.sleep(100);
        bThread.start();
        Thread.sleep(100);
        cThread.start();
        Thread.sleep(100);
    }
```
使用wait、notify这种机制来实现是有点难度的，真实业务上是不可能这么写的。

2、信号量方法实现
```java 
    private static class MyThread extends Thread {
        private String name;
        private final Semaphore current;
        private final Semaphore next;

        public MyThread(String name, Semaphore current, Semaphore next) {
            this.name = name;
            this.current = current;
            this.next = next;
        }

        @Override
        public void run() {
            while (true) {
                try {
                    current.acquire();
                    System.out.println(name);
                    next.release();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }
    }
    // 以A开始的信号量,初始信号量数量为1
    private static Semaphore A = new Semaphore(1);
    // B、C信号量,A完成后开始,初始信号数量为0
    private static Semaphore B = new Semaphore(0);
    private static Semaphore C = new Semaphore(0);

    public static void main(String[] args) throws InterruptedException {
        Thread aThread = new MyThread("A", A, B);
        Thread bThread = new MyThread("B", B, C);
        Thread cThread = new MyThread("C", C, A);

        aThread.start();
        Thread.sleep(100);
        bThread.start();
        Thread.sleep(100);
        cThread.start();
        Thread.sleep(100);
```