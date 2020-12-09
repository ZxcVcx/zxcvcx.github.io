---
layout: default
---


``` java

public class twoThreads
{
    public static void main(String[] args)
    {
        //Thread1 thread1 = new Thread1();
        Thread thread1 = new Thread(new Thread1());
        Thread thread2 = new Thread(new Thread2());
        thread1.start();
        thread2.start();
    }    
}

// thread1
// class Thread1 extends Thread 
// {
//     public void run()
//     {
//         System.out.println("thread1");
//     }
// }
class Thread1 implements Runnable
{
    public void run()
    {
        System.out.println("thread1");
    }
}

// thread2
class Thread2 implements Runnable
{
    public void run()
    {
        System.out.println("thread2");
    }
}
```