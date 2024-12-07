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


  
# 2010
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

