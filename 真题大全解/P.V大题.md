![1731550651463](https://github.com/user-attachments/assets/586ecf03-85f9-43aa-a1f0-07d538f6cc29)# 2009 
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


