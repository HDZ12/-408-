[2016]某个进程训度程序采用基于优先数(priority)的调度策略，即选择优
先数最小的进程运行，进程创建时由用户指定一个nice作为静态优先数。为了动态调整
优先数，引入运行时间cpuTime和等待时间waitTime,.初值均为0。进程处于执行态时，
cpuTime定时加1,且waitTime置O;进程处于就绪态时，cpuTime置O,waitTime定时
加1。请回答下列问题：

1. 若调度程序只将nice的值作为进程的优先数，即priority=nice,则可能会出现饥饿
现象。为什么?
由于采用了静态优先数，当就绪队列中总有优先数较小的进程时，优先数较大的进程一
直没有机会运行，因而会出现饥饿现象。

2. 使用nice,cpuTime和waitTime设计一种动态优先数计算方法，以避免产生饥饿现象，
并说明waitTime的作用。

priority = nice+k1 * cputime-k2 * waitTIme,k1>0,k2>0,分别用来调整cpuTime和waitTime在priority中所占的比例。若一个进程的运行时间较长，则其cpuTime就增加，进而降低其优先级：若一个进程的等待时间较长，则其waitTime增加，进而会提高其优先级。于是，wait Time就可使长时间等待的进程优先数减少，进
而避免出现饥饿现象。
