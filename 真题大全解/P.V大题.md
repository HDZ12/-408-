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
