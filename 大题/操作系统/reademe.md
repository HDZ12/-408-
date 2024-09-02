[2016]某个进程训度程序采用基于优先数(priority)的调度策略，即选择优
先数最小的进程运行，进程创建时由用户指定一个nice作为静态优先数。为了动态调整
优先数，引入运行时间cpuTime和等待时间waitTime,.初值均为0。进程处于执行态时，
cpuTime定时加1,且waitTime置O;进程处于就绪态时，cpuTime置O,waitTime定时
加1。请回答下列问题：

1. 若调度程序只将nice的值作为进程的优先数，即priority=nice,则可能会出现饥饿
现象。为什么?
因为cputime在执行态时加一，在执行完进入就绪态又变为0，所有处于就绪态的进程cputime都为零，这样无法判定哪个没执行过
可能一直处于就绪态

2. 使用nice,cpuTime和waitTime设计一种动态优先数计算方法，以避免产生饥饿现象，
并说明waitTime的作用。

