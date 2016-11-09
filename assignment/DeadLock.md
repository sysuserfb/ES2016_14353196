#死锁的产生和原理
###产生死锁的四个必要条件
- 互斥使用
  - 一个资源每次只能给一个进程使用
- 不可抢占
  - 进程已获得的资源，在末使用完之前，不能强行剥夺
- 请求和保持
  - 一个进程在申请新的资源的同时保持对原有资源的占有
- 循环等待
  - 若干进程之间形成一种头尾相接的循环等待资源关系
  
###程序发生死锁停止的截图如下
![deadlock](https://raw.githubusercontent.com/sysuserfb/ES2016_14353196/master/20161110002716.png)<br>
那么为何程序会发生死锁呢？
- 首先看一下DeadLock的代码
```java
class Deadlock implements Runnable{
	A a=new A();
	B b=new B();

	Deadlock(){
		Thread t=new Thread(this);
		int count=20000;
		t.start();
		while(count-->0);
		a.methodA(b);
	}
	public void run(){
		b.methodB(a);
	}
	public static void main(String args[]){
		new Deadlock();
	}
}
class A{
	synchronized void methodA(B b){
		b.last();
	}
	synchronized void last(){
		System.out.println("Inside A.last()");
	}
}
class B{
	synchronized void methodB(A a){
		a.last();
	}
	synchronized void last(){
		System.out.println("Inside B.last()");
	}
}
```
- 从代码中就可以看出这个程序的流程是怎样的<br>
![float](https://raw.githubusercontent.com/sysuserfb/ES2016_14353196/master/1111.png)
- 我们从结果中可以发现，先print A和先print B这两种情况是均有出现的，而从流程图中也可以看出t.start()执行之后t.run()就立刻开始了，而它们的接下来一条语句分别是`while(count-->0);a.methodA(b);`和`b.methodB(a)`，那么到底谁先谁后呢？关键就在于`while(count-->0);`以及计算机的运算速度
- 当然从结果中的两种情况可以看出，先A还是先B其实是不稳定的，所以假定有那么一刻
```java
//当run()执行到
synchronized void methodB(A a){
		a.last();
} -->这里阻塞了class B的所有方法，所以deadlock不能调用B.last()

synchronized void last(){
		System.out.println("Inside A.last()");
} --> 由于class A的所有方法被阻塞所以也陷入等待状态 ----> 甚至导致了methodB被阻塞

//deadlock（a.methodA(b);）执行到

synchronized void methodA(B b){ --> 由于下面的last函数阻塞所以同时也一样陷入等待，阻塞了所有class A的所有方法
		b.last();
}
synchronized void last(){ -->由于run调用methodB而被阻塞，陷入等待
		System.out.println("Inside B.last()");
}
至此，所有方法都被互相阻塞，线程t和class deadlock想入互相等待资源的循环中，死锁的四个必要条件被满足

/*或者*/
//当run()执行到
synchronized void methodB(A a){
		a.last();
}
//deadlock（a.methodA(b);）执行到
synchronized void last(){
		System.out.println("Inside B.last()");
}
//也是同理
```
- 这也从另一方面说明了停下来的次数的随机性
