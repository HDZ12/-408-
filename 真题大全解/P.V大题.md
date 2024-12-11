# 2009 
![1731547060175](https://github.com/user-attachments/assets/9f18c78b-a2ae-4d85-8789-e72ac0b33c22)
```C
semaphore empty=N;//空的位置
semaphore full1=0;//奇数的数量
semaphore mutex=1;//互斥进入缓冲区
semaphore full2;//偶数的数量
P1(){
  while(1){
    n=produce();
    P(empty);
    P(mutex);
    put();
    V(mutex);
    if(n%2==0)
      V(full2);
    else
      V(full1);
  }
}
P2(){
  while(1){
    P(full1);
    P(mutex);
      getodd();
    V(mutex);
    V(empty);
    countodd();
  }
}
p3(){
  while(1){
    P(full2);
    P(mutex);
      geteven();
    V(mutex);
    V(empty);
    counteven();
  }
}
```
![1733571194564](https://github.com/user-attachments/assets/0d163247-72ed-41e1-bffb-d3e018b22d36)


  
# 2011
![1731548461169](https://github.com/user-attachments/assets/66ef52db-9ed3-44ef-b69e-c861c31243b3)
```C
semaphore empty=10;//空座位
semaphore full=0;//等待的人；
semaphore mutex=1;//叫号机互斥使用
semaphore service=0;//等待叫号
cobegin{
  process 顾客 i
  {
    while(1){
      P(empty);
      P(mutex);
      从取号机获取一个空号码；
 		  V(mutex);
		  V(full);
		  p(service);
		  获取服务；
		}
	}
  	process 营业员
	{
	while(1){
		p(full);
		V(empty);
		V(service);
		为客户服务；
	}
	}
} 

```
![1733571248985](https://github.com/user-attachments/assets/52281a45-cbfd-4124-ac2a-96b98453ceee)
# 2013
![1731549848649](https://github.com/user-attachments/assets/d30eaa28-7c62-4db8-8f93-be8152b9bd3d)
![1731549862712](https://github.com/user-attachments/assets/8490fde9-4542-4ad2-a584-91dcbc6bf6d0)

```C
semaphore empty = 500 ; // 还能容纳多少人
semaphore full = 0 ； //已经有多少人在里面
semaphore mutex = 1; //进,出门的互斥访问
cobegin 
	参观者进程 i：
	{
		P(empty);
		P(mutex);
			进门；
		V(mutex);
			V(full);
			参观；
		P(mutex);
			出门；
		V(mutex);
		P(full);
		V(empty);
	}
```
# 2014
![1731550651463](https://github.com/user-attachments/assets/e315abad-32e0-4f5b-be93-9a95acb287bb)
```C
semaphore empty = 1000; // 缓冲区空位数量；
semaphore full = 0; //缓冲区产品数量；
semaphore mutex1 = 1;//消费者之间的互斥
semaphore mutex2 = 1;//生产者消费者访问缓冲区互斥；
生产者 i：
{
	P(empty);
	P(mutex2);
	生产一件产品；
	V(mutex2);
	V(full);
}
消费者 i：
{
	p(mutex1);
		for(int i=0;i<10;i++){
			P(full);
			P(mutex2);
			取走一件产品；
			V(mutex2);
			V(empty);
			消费产品；
		}
	V(mutex1);
}
```
# 2015
![1731552352870](https://github.com/user-attachments/assets/dcdca4af-94f4-4414-a6b4-dfe94dcd045e)
```C
semaphore empty1 = M-x; //A的空位置；
semaphore full1 = x; //A 的邮件数量；
semaphore empty2 = N-y；// B的空位置；
semaphore full2 = y； //B的邮件数量；
semaphore mutex_A = 1;
semaphore mutex_B = 1;
A{
	P(full1);
	P(mutex_A);
	从 A 中取出一个邮件；
	V(mutex_A)
	V(empty1);
	回答问题并提出一个新问题；
	P(empty2);
	p(mutex_B);
	将新邮件放入B的邮箱；
	V(mutex_B);
	V(full2);
}
B{
	P(full2);
	P(mutex_B)
	从B中取出一个邮件；
	V(mutex_B)
	V(empty2);
	回答并提出一个新问题；
	P(empty1);
	P(mutex_A)
	将新邮件放入A；
	V(mutex_A)
	V(full1);
}
```
# 2017
![1731558161819](https://github.com/user-attachments/assets/ed6d96e0-7481-4a4d-944d-e1719c8bb77b)
```C
semaphore mutex_y1=1;//thread 1,thread3对y的互斥访问
semaphore mutex_y2=1;//thread 2,thread3对y的互斥访问；
semaphore mutex_z=1;//对z的互斥访问
thread1{
	cnum w;
	P(mutex_y1);
	w=add(x,y);
	V(mutex_y1);
}
thread2{
	cnum w;
	P(mutex_y2);
	P(mutex_z);
	w=add(y,z);
	V(mutex_y2);
	V(mutex_z);
}
thread3{
	cnum w;
	w.a=1;
	w.b=1;
	P(mutex_z)
	z=add(z,w);
	V(mutex_z);
	P(mutex_y1);
	P(mutex_y2);
	y=add(y,w);
	V(mutex_y1);
	V(mutex_y2);
}
```

![1733723552756](https://github.com/user-attachments/assets/24b9eac4-916d-49dd-8994-1d05358c0691)
# 2019
![1731559256568](https://github.com/user-attachments/assets/8656a792-f765-4776-ab64-458d513cc370)
```C
semaphore bow; //空碗数量；
semaphore chopstick[n];//筷子的互斥访问
bow = min(n-1,m);
for(int i=0;i<n;i++)
	chopstick[i]=1;
哲学家 i(){
	while(1){
		P(bow);
		P(chopstick[i]);
		P(chopstick[(i+1)%n]);
		进餐；
		V(chopstick[i]);
		V(chopstick[(i+1)%n]);
		V(bow);
	}
}
```
![1733811764108](https://github.com/user-attachments/assets/660a1903-f4e4-4704-999a-638ada3da562)
# 2020

![1731560107033](https://github.com/user-attachments/assets/30fdc18a-5ea9-42e4-95e4-ca6f3d6580c0)

```C
semaphore Sac = 0; //A与C的同步；
semaphore Sbc = 0; //B与C的同步；
semaphore Sce = 0；//C与E之间的同步；
semaphore Sde = 0；//D与E之间的同步；
A(){
	A操作执行；
	V(Sac);
}
B(){
	B操作执行；
	V(Sbc);
}
C(){
	P(Sac);
	P(Sbc);
	C操作执行；
	V(Sce);
}
D(){
	D操作执行；
	V(Sde);
}
E(){
	P(Sce);
	P(Sde);
	E操作执行；
}
```
# 2021
![1731560542687](https://github.com/user-attachments/assets/b0075c52-da8b-4d6b-bfe5-f29f5cd90452)

(1)

多个进程共享变量S，多个进程都可对S进行操作，所以访问必须互斥；

(2)

方法1错误。在wait()中，当S<=0时，关中断后，其他进程无法修改S的值，whi1e语句陷入死循环。方法2正确。方法2在循环体中有一个开中断操作，这样就可以使其他进程修改S的值，从而避免while语句陷入死循环。

(3)

用户程序不能使用开/关中断指令实现临界区互斥。因为开中断和关中断指令都是特权指令，不能在用户态下执行，只能在内核态下执行。
# 2022
![1731561106319](https://github.com/user-attachments/assets/0a236b70-0204-4625-b707-2bedeac17f59)
```C
semaphore Sac = 0; //A与C之间的同步
seamphore Sce = 0;//C与E之间的同步；
T1(){
	while(1){
		A;
		V(Sac);
		P(Sce);
		E;
		F;
	}
}
T2(){
	while(1){
		B;
		P(Sac);
		C;
		V(Sce);
		D;
	}
}
```
# 2023
![1731561610659](https://github.com/user-attachments/assets/cdb60c1f-4d4c-4e8f-a6a2-7b22906d95f2)
(1)

if(key == TRUE)->while(key == TRUE);
退出区：lock=FALSE；

(2)

否。因为多个线程可以并发执行newSwap(),newSwap(O执行时传递给形参b的是共享变量lock的地址，在newSwap0中对lock既有读操作又有写操作，并发执行时不能保证实现两个变量值的原子交换，从而导致并发执行的线程同时进入临界区。例如，线程A和线程B并发执行，初始时lock值为FALSE,当线程A执行完 * a=  * b后发生了进程调度，切换到线程B执行，线程B执行完newSwap后发生线程切换，此时线程A和B都能进入临界区，不能实现互斥访问。
# 2024
![1731563676653](https://github.com/user-attachments/assets/6c583b68-f78e-4034-a996-d042ee92e323)

(1)

是，互斥访问

(2)
```C
semaphore mutex =0;
p1(){
	写入B；
	V(mutex);
}
P2(){
	P(mutex);
	读出B；
}
```
（3）
```C
seamphore mutex=1;
p2(){
	P(mutex);
	修改；
	V(mutex);
}
P3(){
	P(mutex);
	修改；
	V(mutex);
}
```
# 相关知识点
## 同步机制原则
1. 空闲让进
2. 忙则等待
3. 有限等待
4. 让权等待
# 硬件与软件方法
## 硬件(不能实现让权等待)
中断屏蔽，硬件指令，swap指令，TestAndSet指令
## 软件
- 单标志法（违法空闲让进）
- 双标志先检查法（违反忙则等待）（检查和上锁不是原子操作）
- 双标志后检查法（违反了有限等待和空闲让进）（会引起饥饿）
- peterson算法（违反了让权等待）
# 信号量
## 整形信号量（不满足让权等待）
# 记录型信号量（满足让权等待）
# 管程
只要有管程外就是错误
