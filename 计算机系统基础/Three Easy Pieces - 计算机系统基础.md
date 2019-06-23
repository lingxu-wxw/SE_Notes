## Three Easy Pieces 

------

### 第七章

* Policy 策略 ：Process scheduling policy 进程调度策略，replacement policy 淘汰策略 

* 进程运行环境假设
  * 运行时间一样；同时开始；进程都能执行到结束；每个job只使用CPU；job的运行时间是知道的

* 调度评价指标
  * Turnaround time，系统完成时间
    * 从到这里，到完成服务，turnaround time= completion - arrival
    * job的运行时间和系统的完成时间不一样
    * 三个进程，10s，turnaround time 10s,20s,30s，对于进程运行时间一样挺好的
    * 进程时间不一样，会有传递效应 – shortest job first
    * 可以中断，检测最先能完成的先做，- shortest time-to-completion first
  * Response time，响应时间
    * 从到这里，到开始服务，response time=first turn – arrival
    * 通过round rabin尽早开始服务，降低响应时间
    * Round rabin的缺点：Switch cost保存、读取上下文，flush TLB（置零，频繁的TLB miss），flush硬件流水线（异常处理）；补偿amortization 

* 策略优化过程
  * First in，first out， FIFO
  * 弱化运行时间一样，Shortest job first， SJF
  * 弱化同时开始，没啥办法
  * 弱化进程都能执行到结束，shortest time-to-completion first，STCF
  * Round rabin，任务切片，定义单位执行时间 time slice,  RR
  * 弱化每个job只使用CPU（使用IO）
  * Overlap io and cpu
  * 每次有io的时候把进程block一下，去做一点别的job，实现io和cpu的overlap
  * 弱化知道每个job的运行时间,让历史告诉未来， MLFQ
  * 根据过去运行表露出来的特征，预测一下未来
  * 周期性的job效果会比较好

*  

------

### 第八章

* 不知道每个job的运行时间怎么办？ MLFQ策略

* Basic rules

  * 0. 任何一个job只能出现在一个队列里面，每个队列都有执行的priority
  * 1. 优先级高的进程会得到执行
  * 2. 如果队列a和队列b优先级一样，就RR
  * 3. 初始的时候，当一个job刚刚进入system，都会被置为最高优先级
  *    4a. 如果一个job用完了全部的time slice时间，那么priority降低

  *    4b. 如果job在time silce用完之前释放了CPU，那么priority不变

* Workload的组成部分

  * Interactive jobs：键盘敲击，每次用完都会fresh cpu
  * Longer-running CPU-bound jobs，response time不是很重要

  * 一系列io-intensive的和 cpu-intensive的workload

* 策略
  * 当一个job来了，MLFQ将他看成short job，给他最高priority
  * 如果是就执行完，不是就降低priority
  * 如果是interactive job，做很多io的那种，每次用完time slice之前都会释放cpu，那就一直停在最高的priority

* MLFQ的问题
  * Starvation饿死，在priority底层等待的job得不到执行。但没有恶意
  * Gaming scheduler attack，实际上是一个要用很长时间cpu的job，每次在time slice快到的时候就issue一个io，io是释放cpu的，io不用做什么事情，这样就保持job一直在最高级priority
  * Change its behavior

* Rules更新 priority boost
  *    5a. 每过一点时间s，所有jobs都会被提到最高的priority
  *    5b.如果从cpu-bound变成interactive，就一直待在最高级别

* Rules更新 better accounting
  *    4a. 设定与time slice以外的allotment，allotment累计使用cpu的时间，用完了就降级（之前一释放cpu就清空了），allotment比time slice大一点点

* 参数确定 tuning MLFQ
  * 几个队列？Time slice？Priority boost？
  * OUSTERHOUTS law 调参

*  

------

### 第二十二章

* I/O bottleneck
  * 磁盘读写顺序：cylinder圆柱体-> 找platter盘片-> 找track (磁道)-> 旋转找sector(扇区) 
  * 磁盘访问时间 = 寻道时间 + 旋转时间 + 传送时间
  * 总线：The integrated device electronics IDE, 集成电路设备 66MB/s 

* 策略

  * to layout the blocks of a file contiguously

  * to prefetch an entire track of data on each read

  * 省读的时间：一起读进来，read request per 384 loop

    ![1554463288134](http://ww3.sinaimg.cn/large/006tNc79ly1g4b9ghhkkaj30fh02l0st.jpg)                                         

  * 写的时间延迟。不立即写磁盘，多存一些一次性写到磁盘上去 Improve by dallying & batching write requests

    ![1554463318559](http://ww3.sinaimg.cn/large/006tNc79ly1g4b9ggo7tcj30fy01o0sr.jpg)

  * 并行

    ![1554463357821](http://ww4.sinaimg.cn/large/006tNc79ly1g4b9gh0i05j30c406odgf.jpg)

  * Tradeoff：可靠性reliability和性能performance

    * 参数：写的latency要多久

* Cache管理 replacement policy
  * 参数：AMAT average memory access time = Phit * Tmemory + Pmiss * Tdisk
  * Memory access 约100ns，disk access 10ms -> miss rate影响很大

* 淘汰策略
  * Optimal策略：理论最优，预知未来，replace page will be accessed furthest in the future 
  * FIFO策略：问题 - Belady Anomaly(异常)：当cache size变大，命中率应该会提高，但FIFO不一定会这样
  * Random策略：超过40%的时间里，random跟optimal一样好
  * LRU策略：没有Belady异常；Subset属性，与FIFO不同，当cache size变大，原先留着的都还会留着
  * LFU policy 历史上用的次数最少的淘汰 least-frequently-access
  * Clock algorithm：Access bit 1被访问，0没有被访问

* Workload种类
  * Random access workload
    * 各种策略的hit rate基本和cache size成正比，跟具体策略关系不大，低于optimal
    * 当cache足够大，那跟策略没差了
  * 80-20 workload：hot page，cold page，20%的page被访问了80%的次数
    * LRU表现挺好，但并不一定可以说明LRU优于FIFO
  * Looping sequential workload 循环访问
    * 当cache足够大的时候，各种策略都好；不够大时，LRU表现糟糕，几乎为0

* 如何实现LRU

  * 拿不到时间戳，排序也很慢？

  * 实际上使用的是一个近似LRU的clock algorithm

*  

------

### 第二十九章

* 基于锁的并发数据结构
  * 锁：two status：unlock，lock
  * POSIX标准，提供了锁的数据类型pthread_mutex_t，也叫mutex

  * 锁的初始化 pthread_mutex_init
  * 锁调用的函数 pthread_mutex_lock， pthread_mutex_unlock
  * 在status是lock的情况下调用lock会把线程block住
    * Trylock函数，如果失败就返回failure
    * Timedlock函数，block的等待时间是无期限的，申请锁给一个time值，在这个值之后返回

* Lock如何应用到数据结构的设计当中去

  * 加锁会损失性能，但能够保证访问数据结构是安全的
  * 几个并发的数据结构：Counter，Simple lined list，Concurrent Queue，Concurrent hash table

* 案例一：Counter
  * Struct Counter_t { int value; pthread_mutex_t lock;  }
  * Sample：有两个线程，分别加1000次，结果要等于2000

  * 每一次incre和decre前后都加锁，安全性肯定是可以保证的
  * Scalable counting：目标：多线程时候的性能和单线程差不多

* 改进案例一：Sloppy counting
  * 把一个count打碎：local counting，global counting
  * 每一个local count都有一把local lock
  * Local value阶段性的更新到global count，更新的时候用global lock
    * 参数：多久更新一次？ Sloppiness，Threshold（门槛）

  * 读值的方式
    * Scalable read：只读global值，不准确
    * Exact（non-scalable）read：读所有的global和local，精确，性能不好
  * 如何设置sloppiness
    * Sloppiness较小 -> global count比较精确，效率低
    * Sloppiness = 256

* 案例二：Simple Linked List
  * 普通的链表，value，*next；功能函数：insert，lookup

* 改进案例二：
  * 目前lib提供的malloc是可以多线程的，锁可以不用包括malloc
  * 减少程序的分支，尽可能一开一关
  * 性能锁：把原本加在list上的lock改成加在node上的lock（不适用的原因，加锁解锁过于频繁，overhead太大，不实际）

* 案例三：Concurrent Queue

  * 队列操作：enqueue，dequeue（先进先出）

* 改进案例三：Michael and Scott Concurrent Queue
  * 提供两把锁：headlock和taillock，实现enqueue和dequeue可以一起做，但不能多线程一起做enqueue
  * 最理想的数据结构是没有锁的数据结构

  * Dummy node，head始终指向dummy node，head和tail最初都指在dummy node上
  * 边界条件，对列为空，刚刚enqueue就可以dequeue 

* 案例四：Concurrent hash table
  * Hash_t ，List_t lists[BUCKETS]

* 

------

### 第二十八章

* 锁的实现
  * Sigprocmask，开关中断的操作以阻塞某一个signal，sigblock/setmask
    * 局限性：用户必须是值得信任的；不适用于多cpu的中断操作；即使是善意的操作 -> 通常只用在内核态和操作系统 

  * Test And Set，Compare And Swap，Load Linked， Store Conditional，Ticket Lock: Fetch and add

* 第一次尝试
  * 简单的flag, mutex->flag：Cons：并发情况下正确性没有保障；当拿不到锁的时候在while中自旋

* 实现正确性
  * TestAndSet，读old值，将new值置入，return回old值
    * 需要保证在硬件执行上是原子的, kernel指令
  * While (TestAndSet(&lock->flag, 1) == 1);
    * New值1被置入，读出原先的0，
    * 发现别人对这把锁感兴趣的时候，把自己的锁置为0，让出锁
    * 能够避免死锁，但是活锁是不能避免的；同时也不能在多处理器中正常工作
    * 没有公平性
  * While (CompareAndSwap(&lock->flag, 0, 1) == 1);
    * 返回flag的原先值，如果原先值 == expect，将其置为new值

* 实现公平性
  * Ticket lock： fetch and add
  * 先来后到的策略 myturn = FetchAndAdd(&lock->ticket);  while (lock->turn != myturn);

* 优化：减少无意义的自旋
  * 主动放弃yield，在没有拿到锁的情况下，让出cpu时间
  * Queue，让等待的线程都被block住，这样就不会占用cpu资源，并且在得到锁之前不会再被调度到
  * 唤醒sleep中的进程，lock->guard
  * Park()是让进程休眠

* Shortcut效果：在 || 的时候，如果前半条为真，则不执行后半条 

* 设计锁需要考虑到的：正确性，效率，公平性

* Park和unpark

  * 当有线程申请锁的时候，构造一个队列，如果没有拿到锁，就在队列当中排队

  * Lock->flag是大锁，置1表示锁已经被其他线程拿走了；guard是申请锁的过程中要一把锁；queue维护申请锁的排队 

* 实现lock和unlock
  * 为什么不能park放前面？guard是1的情况下park，线程就去睡觉了，其他想要获取锁的线程就凉了，即使unlock也不行

  * 假设线程中断，lock中guard置零后中断，这段时间执行了unpark，当线程回归，再执行park会有点问题

* Two phase locks
  * 第一阶段：spin一会
  * 第二阶段：caller被睡了

* 

------

### 第三十章

* 条件成立就执行代码，条件不成立就不执行代码
* Conditional variable： 如果状态不满足就wait 

* 声明条件变量：pthread cond_t c;

* 线程锁：pthread mutex_t m;

* 两个原子操作：wait()和signal()唤醒，wait的参数需要有一把锁

* 一般不建议写成 if (done == 0) pthread_cond_wait(&c,&m);

* Mesa semantics：状态发生变化的时候唤醒，但不保证执行的时候还是这个数据（用while更保险的原因）

* Hoare semantics：状态发生变化的时候唤醒，保证执行的时候数据不变

* 现在signal的通知不知道发给谁