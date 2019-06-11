## 操作系统

------

#### 第一讲 Introduction & 8 Important Problems in Modern Operating Systems

* 操作系统是什么
  * 定义：操作系统是管理硬件资源、控制程序运行、改善人机界面和为应用软件提供支持的一种系统软件；向上提供服务，向下管理资源
    * OS对apps管理和隐藏资源，隐藏tedious/complex的底层细节，为apps提供执行环境
  * 广义定义：包括管理程序，操作系统，运行时环境

* 操作系统发展的两个观点
  * 硬件与应用蓬勃发展，在端和数据中心侧可能孕育新的操作系统
  * 传统操作系统如Linux进入架构稳定期，难以根本上适应新硬件与应用需求

* 8 Important Problems of OS

  * Scale Up；Security & Trustworthy；Energy Efficiency；Mobility；
  * Write Correct (Parallel) Code；Scale out；Non-Volatile Storage；Virtualization

* Issue 1 ：Scale Up (Performance Scalability) 纵向扩展

  * Challenge 1：make software performance follow Moore's Law
  * Andy-Bill’s Law：安迪指英特尔前CEO安迪·格鲁夫，比尔指微软前任CEO比尔·盖茨，这句话的意思是，硬件提高的性能，很快被软件消耗掉了。
  * Scalability 扩展性
    * 理论上应用在多核(N)上运行应该比单核快N倍
    * 但实际上受限于Amdahl's Law (Lock，共享数据结构，共享硬件DRAM/NIC)
  * Scale Up OS
    * 对用户apps提供更好的抽象
    * 消除不可扩展的同步
    * 最小化共享数据结构
    * 跨过memory wall

* Issue 2 ：Security & Trustworthy 安全问题

  * Meltdown和Spectre攻击：利用分支预测和乱序执行的漏洞
  * KPTI (Kernel Page Table Isolation)，内核页表隔离来预防meltdown攻击
  * Formal verification 形式化验证 (seL4)，针对Trustworthy问题

* Issue 3 ：Power Efficiency 能源效率

  * 典型服务器各组件的耗电情况

    ![1554557487878](Pictures/Operating_System/1554557487878.png)

  * 关于Power，OS可以做的事

    * 动态电压、频率适应：根据overload来调整CPU的主频
    * 关闭设备来省电：disk，LCD 液晶显示器，memory
    * 问题：能源消耗是不随overload的增加而增加的 (Static power, leakage power)
    * Threshold Voltage 阈值/临界电压

* Issue 4 ：Mobility 移动性

  * 智能手机的操作系统：Symbian，Windows Mobile，RIM Blackberry OS，Apple iOS，Google Android，Palm WebOS，Windows Phone 7

  * Android操作系统的架构

    ![1554557978966](Pictures/Operating_System/1554557978966.png)

  * 移动端OS的特殊性

    * 更高的能源利用效率；更丰富的用户体验；更有限的资源；更严峻的安全问题 (更多的user data存在OS中)

* Issue 5 ：Write Correct Parallel Code 正确的并发代码

  * Parallel Code的难点
    * 并发程序容易出现并发错误
    * 并发bug的特点：不确定性，难以复现/debug
  * 解决问题的方法
    * 并发错误检测：race detection, atomicity violation detection, deadlock bug detection
    * 并发程序测试：详尽的测试，不同的涵盖范围准则
    * 并发编程语言/模型设计：transactional memory
  * 关于并发，OS可以做的事
    * 减少资源的不确定性
    * 容忍应用的bug
    * 忠实地捕获并发bug并进行复制
    * 提供更好的编程接口来简化编程

* Issue 6 ：Scale Out  (use distributed systems) 横向扩展

  * 分布式系统需要解决的问题
    * Ease-of-use：解决地理隔离；给用户/应用提供位置透明性
    * Availability：用一些unreliable的组件构建reliable的系统
    * Scalable capacity：聚合许多computer的资源
    * Modular functionality：只需要构建能完成single task的service就行
  * Scale Out的挑战
    * System Design 系统设计：interface，abstraction
    * Consistency 一致性
    * Fault Tolerance 容错
    * Different deployment scenarios 不同的部署场景：Clusters, wide area distribution, sensor network
    * Security 安全：authenticate clients/servers，defend misbehaving server
    * Implementation 实现：bottleneck

* Issue 7 ：Non-Volatile Storage 非易失性内存

  * 新式的存储

    ![1554607824587](Pictures/Operating_System/1554607824587.png)

  * 关于存储，OS可以做的事

    * 适应新的存储模型
    * 非易失性内存会改变OS的管理存储资源的方式
    * 提供更好的IO performance

* Issue 8 ：Virtualization 虚拟化

  * 虚拟化架构

    ![1554608063907](Pictures/Operating_System/1554608063907.png)

  * 虚拟化的优势

    * 最大化资源利用率：多个操作系统环境可以共存于同一台计算机上，彼此隔离；server consolidation
    * 容错：fault and migrate
    * 轻便：可以使用各种OS
    * 易于管理

  * 虚拟化的方法

    ![1554608224031](Pictures/Operating_System/1554608224031.png)

*  

------

#### 第二讲 OS Structures

* OS Design and Implementation

  * Worse is Better design 设计原则
  * User goal 和 System goal
    * 用户会希望操作系统方便使用，容易学，可靠，安全，还快
    * 系统开发者希望操作系统容易设计/实现，可靠，可扩展，容错，高效

* Kernel 分类：Monolithic, Microkernel, Exokernel, Hybrid

  * Monolithic 宏内核：OS在kernel space运行，在supervisor mode 运行 （Linux BSD)
  * Microkernel 微内核：low-level address space management, thread management, and inter-process communication (IPC)等技术，（Mach  L4 kernel）
  * Hybrid kernel 复合内核：Windows ，NT kernel

  ![1554882220939](Pictures/Operating_System/1554882220939.png)
  * DOS：没有模块的划分，接口和实现没有很好的分离。DOS以后开始有一些Layered Approach，将OS分为若干level来实现

  ![1554882284901](Pictures/Operating_System/1554882284901.png)

  * UNIX：UNIX OS包括System program和kernel部分

   ![1554882436070](Pictures/Operating_System/1554882436070.png)

* Microkernel 系统架构

  * 思想：将尽可能多的功能从kernel态移到user态
  * 优势：易于扩展；易于将OS移植到其他体系结构；因为kernel代码更少，所以更可靠，更安全
  * 缺点：kernel和user之间频繁通信的overhead

  ![1554883036112](Pictures/Operating_System/1554883036112.png)

* 微内核相较于宏内核的改变

  * Task and thread management
  * Interprocess communication
  * Memory object management
    * 主要是virtual memory
  * System call redirection
    * 通过trap来切换mode；
  * Device support
  * User multiprocessing
  * Multicomputer support

* L3 - > L4

* 暂时鸽一会

*  

------

#### 第三讲 PC Programming & Booting

* x86架构 (32-bit)
  * EIP随着指令增加；指令是不定长的；EIP会被call, ret, jmp, cond. jmp修改

##### 五种CPU工作模式 (modes) {

* 定义：Real Mode, Protected Mode, Virtual-8086 Mode, IA-32e Mode, System Management Mode
* 名词解释：
  * PE，Protection Mode的开关
  * SMI，System Management Interrupt，系统管理中断，使系统进入SMM的特殊中断
  * SCI，System Control Interrupt，系统控制中断，专门用于ACPI电源管理的一个IRQ，需要OS支持
* Real-Address Mode是在bootloader阶段的运行模式，存在时间很短。内存寻址方式和8086相同，没有虚拟地址，由16位段寄存器（CS/SS/DS/ES）乘以0x10当做基地址，再加上16位偏移地址形成20位的物理地址，最大寻址空间1MB，最大分段64KB。
* Protected Mode是最常用的模式，内存寻址采用32位段和偏移量（现在64位），最大寻址4GB，最大分段4GB。它提供了一些增强多工和系统稳定性的设计，比如内存保护，分页系统，虚拟内存等，防止程序随意访问地址，也拥有更大的内存访问空间。
* Virtual-8086 Mode是在保护模式下运行的虚拟实模式环境，寻址方式与实模式相同。
* IA-32e Mode是64位操作系统运行的模式，具有兼容模式和64位模式两种子模式。兼容模式可以运行在32位兼容环境，但不能运行虚拟8086程序；64位模式则完全处理64位指令
* System Management Mode有独立于OS的地址空间，用来执行电源管理或系统安全方面的指令。

![1555892328783](Pictures/Operating_System/1555892328783.png)

##### }

##### x86中的EFLAGS寄存器  {

```
ID: Identifiction Flag - 程序能够设置或清除这个标志指示了处理器对CPUID指令的支持
VIP: Virtual Interrupt Pending - 该位置1以指示一个中断正在被挂起，当没有中断挂起时该位清零
VIF: Virtual Interrupt Flag - 使用这个标志以及VIP标志，并设置CR4控制寄存器中的VME标志就可以允许虚拟模式扩展(virtual mode extensions)
AC: Alignment Check - 该标志以及在CR0寄存器中的AM位置1时将允许内存引用的对齐检查，以上两个标志中至少有一个被清零则禁用对齐检查
VM: Virtual-8086 Mode - 置1以允许虚拟8086模式，清除则返回保护模式
RF: Resume Flag - 控制处理器对调试异常的响应
NT: Nested Task Flag - 这个标志控制中断链和被调用任务。若当前任务与前一个执行任务相关则置1，反之则清零
IOPL: I/O Privilege Level - 指示当前运行任务的I/O特权级，正在运行任务的当前特权级(CPL)必须小于或等于I/O特权级才能允许访问I/O地址空间
IF: Interrupt Enable Flag - 该标志用于控制处理器对可屏蔽中断请求的响应。置1以响应可屏蔽中断，反之则禁止可屏蔽中断
TF: Trap Flag - 将该位设置为1以允许单步调试模式，清零则禁用该模式
```

![1555892720464](Pictures/Operating_System/1555892720464.png)

##### }

##### 控制寄存器 Control Register { 

* CR0中含有控制处理器操作模式和状态的系统控制标志；CR1保留不用；CR2含有导致页错误的线性地址；CR3中含有页目录表物理内存基地址，因此该寄存器也被称为页目录基地址寄存器PDBR（Page-Directory Base address Register）

![1555893043340](Pictures/Operating_System/1555893043340.png)

##### } 

##### 内存管理寄存器 Memory-Management Register {

* 段选择符：32位汇编中16位段寄存器(CS、DS、ES、SS、FS、GS)中不再存放段基址,而 是段描述符在段描述符表中的索引值,D3-D15位是索引值,D0-D1位是优先级(RPL)用于特权检查,D2位是描述符表引用指示位TI,TI=0指 示从全局描述表GDT中读取描述符，TI=1指示从局部描述符中LDT中读取描述符。这些信息总称段选择符(段选择子)

![img](https://img-blog.csdn.net/20160806195439147?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

* 段描述符表：IA-32处理器把所有段描述符按顺序组织成线性表放在内存中，称为段描述符表。分为三类：全局描述符表GDT，局部描述符表LDT和中断描述符表IDT。GDT和IDT在整个系统中只有一张，而每个任务 都有自己私有的一张局部描述符表LDT，用于记录本任务中涉及的各个代码段、数据段和堆栈段以及本任务的使用的门描述符。GDT包含系统使用的代码段、数据段、堆栈段和特殊数据段描述符，以及所有任务局部描述符表LDT的描述符

![img](http://blog.rootk.com/file/cdc5e2064e8f7279d6dabf4aaf3fc0b9.jpg)

![img](http://blog.rootk.com/file/fd20bfcfff3ea81f0640406db9316f83.jpg)

##### }

##### 内存寻址模型 Memory Model {

* 8086寻址适用于16位微处理器，在Real-Address Mode时使用，没有虚拟地址，最大寻址空间64KB。
* External address寻址由16位段寄存器（CS/SS/DS/ES）乘以0x10当做基地址，再加上16位offset形成20位的物理地址，最大寻址空间1MB。
* 80386寻址适用于32位数据和总线地址，在Protected Mode时使用，存在虚拟地址到物理地址的映射关系，有分页系统，最大寻址空间4GB。

* Physical Address Space Layout
  * 1MB以上被称为extended memory；640KB-1MB是一个内存空洞

![1555893901227](Pictures/Operating_System/1555893901227.png)

##### }

* Memory-mapped IO
  * side effect是什么？？
* TODO：IO的直接映射（Port映射）和MMIO哪个更好一点
  * 

##### xv6源码分析 bootasm.S, bootmain.c, entry.S {

* BIOS会将磁盘的第一个扇区load到物理地址0x7c00，并以real mode开始执行
* Intel 8088的地址线只有20根 (A0~A19)，当时计算机的 RAM 只有几百 KB 或不到 1MB 时，20 根地址线已足够用来寻址；其所能寻址的最高地址是0xffff : 0xffff，即0x10ffef，对于超出0x100000 (1MB)的寻址地址，将默认回卷到0x0ffef
* 在机器启动时，默认条件下，A20 地址线是禁止的，所以操作系统必须使用适当的方法来开启它。但是由于各种兼容机所使用的芯片集不同，有键盘控制器，端口0x92，INT 15中断，0xee端口等方法 <refs https://blog.csdn.net/longintchar/article/details/79365928>
* 从实模式进入保护模式：置上CR0的PE位；用ljmp重载cs和eip

```assembly
ljmp    $(SEG_KCODE<<3), $start32
```

* readsect(...) 中用到的I/O端口

```
1F0H　　 0号硬盘数据寄存器 
1F1H　　 0号硬盘错误寄存器 
1F2H　　 0号硬盘数据扇区计数 
1F3H　　 0号硬盘扇区数 
1F4H　　 0号硬盘柱面（低字节） 
1F5H　　 0号硬盘柱面（高字节） 
1F6H　　 0号硬盘驱动器/磁头寄存器 
1F7H　　 0号硬盘状态寄存器 
```

* 在entry.S中，cr4打开PSE大页，cr3设置entrypgdir基地址，cr0置上PG位和WP位
* TODO： 补充一下 实模式到保护模式，开启页表 前后的微操

##### }

* 仿真 PC Emulation：用于OS test和debug；能提高利用率
*  

------

#### 第四讲 Memory init：xv6 & VM

* Core i7的内存结构

![1554458469403](Pictures/Computer_Architecture/1554458469403.png)

* 页表项结构 PTE

![1555921993835](Pictures/Operating_System/1555921993835.png)

```
P: present
R/W: readable / writable
U/S: user / supervisor
WT: write-through (1) / write-back (0) - 写策略：写穿和写回
CD: cache disabled - 该页是否能被放到cache中，有些页可能是外部设备DMA修改的，不能放在cache中 
A: accessed (set by CPU, clear by OS)
D: dirty
PAT: page table attribute index
G: global page (no TLB updating on the address if CR3 is reset) - 一直放在TLB中不会被刷掉的页；比如处理page fault的handler所在的页
```

* 页目录项结构 PDE

![1555922102326](Pictures/Operating_System/1555922102326.png)

```
PS: page size (0=4KB, 1=4MB) - 4MB: super page
大页对data-intensive的workload更好，能减少TLB miss，降低地址翻译的平均时间；小页对CPU-intensive的workload更好，内存使用更精致
```

* PAE：Physical Address Extension
  * x86和x86-64处理器的一个特色，即如果操作系统提供适当支持，则可以在32位的系统中使用超过4G的内存
  * x86的处理器增加了额外的地址线以选择那些增加了的内存地址，所以支持的内存寻址大小从32bit增加到36bit。最大支持内存由4G增加到64G，32位的虚拟地址则没有变，所以一般的应用软件可以继续使用地址为32位的指令
  * 4种页表结构（32bit机器）：未启用PAE, 4 KB的页；未启用PAE, 4 MB的页；启用PAE, 4 KB的页；启用PAE, 2MB的页

##### xv6源码分析 main.c, vm.c {

* 调用顺序：
  * (main.c) main() 
  * -> (vm.c) void kvmalloc() 
  * -> pde_t *setupkvm()，给kernel段申请页表，并做最基本的映射
    * -> int mappages(pde_t *pgdir, void *va, uint size, uint pa, int perm)，对将pa映射到va的size大小perm权限的页，为其创建一个PTE；va和size可能并不是page-align的
    * -> pte_t *walkpgdir(pde_t *pgdir, const void *va, int alloc)，返回va处的PTE，如果alloc不为0就创建一个
  * -> void switchkvm()，通过lcr3切换到kernel页表
  * -> (proc.c) void userinit()，配置第一个用户进程
* 结构体kmap
  * 每个进程只有一个page table，加上CPU不运行任何process时使用的页表(kpgdir)
  * kernel在system call和interrupt期间会直接只用当前进程的页表
  * 页的protection位防止用户代码使用内核的映射

```c++
static struct kmap {
  void *virt;
  uint phys_start;	
  uint phys_end;
  int perm;
} kmap[] = {
 { (void*)KERNBASE, 0,             EXTMEM,    PTE_W}, // I/O space
 { (void*)KERNLINK, V2P(KERNLINK), V2P(data), 0},     // kern text+rodata
 { (void*)data,     V2P(data),     PHYSTOP,   PTE_W}, // kern data+memory
 { (void*)DEVSPACE, DEVSPACE,      0,         PTE_W}, // more devices
};
```

* User VM 映射的接口

```
创建进程：Inituvm : initialized user VM
	Loaduvm: load program segment
上下文切换：switchuvm
增加/减少/释放VM：allocuvm，deallocuvm，freeuvm
Fork：copyuvm
```

##### }

------

#### 第五讲 Process

* 逻辑地址 - 线性地址 - 物理地址的转换

  ![1556339216237](Pictures/Operating_System/1556339216237.png)

  ![1556339247367](Pictures/Operating_System/1556339247367.png)

* Boot阶段的主要工作：

  * 进入Protected Mode，开启Segment，配置GDT (ljmp指令)
  * 打开页表 (CR0_PG)，初始化entrypgdir，将kernel映射到高地址和低地址 (0x80100000, 0x100000)

* 一些概念

  * Process：设计进程的出发点：程序比处理器多；程序并不需要持续占用处理器；因此可以在不用的时候释放资源；进程是资源分配的最小单位，拥有一个地址空间和若干线程；包含program counter, stack, data section等数据块

  * Thread：线程的抽象定义：停止活动并在稍后某个 时刻恢复活动所需要的最小状态，通常是一些程序寄存器；线程是程序运行的最小单位

  * Context：xv6中的数据结构，包含edi、esi、ebx、ebp、eip五个field

  * Address spaces：地址空间，原则上和线程是独立的概念；可以在同一个地址空间从一个线程切换到另一个线程；也可以在不同地址空间切换

  * Process State：进程状态，一般有new，running，waiting，ready，terminated；xv6中为UNUSED, EMBRYO胚胎, SLEEPING, RUNNABLE, RUNNING, ZOMBIE

    * ENBRYO可以理解为到RUNNABLE之前的一个过渡。allocproc会在进程表中找到一个标记为UNUSED的位置。当它找到这样一个没有被使用的位置后，allocproc将其状态设置为EMBRYO，使其标记为被使用并给这个进程一个独有的pid。接下来，它尝试为进程的内核线程分配内核栈。如果分配失败了，allocproc会把这个位置的状态恢复为UNUSED并返回0来标记失败。

    ![1556342655313](Pictures/Operating_System/1556342655313.png)

* Process Control Block，PCB

  * 每个process都会有一个PCB，内容包括Process state, Process counter, CPU registers, CPU scheduling information, Memory management information, Accounting information, I/O status information
  * xv6 中的进程数据结构

  ![1556343005224](Pictures/Operating_System/1556343005224.png)

* Context Switch 上下文切换

  * 调用syscall触发中断 - save当前进程的PCB - reload目标进程的PCB - 继续执行
  * 上下文切换需要保存的内容应该是存在进程对应的kernel stack中的
  * 上下文切换换栈的瞬间

  ![1556343241697](Pictures/Operating_System/1556343241697.png)

* Process Scheduling Queue 进程调度队列

  * Job Queue：系统中所有的process
  * Ready Queue：系统中所有等待执行的process
  * Device Queue：系统中所有等待IO设备的process

* 两种Scheduler
  * Long-term scheduler / job scheduler：调度即将进入ready queue的进程，完成时间在秒/分钟级别，决定了multiprogramming的程度
  * Short-term scheduler / CPU scheduler：调度即将执行的进程，完成时间在微秒级别
  * scheduler对process的分类：IO-bound process和CPU-bound process

* Process的创建：fork，一次执行两次返回；execute，一次执行没有返回；奇妙的机制

  ![1556344453826](Pictures/Operating_System/1556344453826.png)

*  

------

#### 第六讲 IPC 

* Review Questions
  
  * TODO
  
* Threading Model

  ![1557209601573](Pictures/Operating_System/1557209601573.png)

* Process cooperation的优点：information sharing, computation speed-up, modularity, convenience

* IPC的两种模型：如上图，message passing 和 shared memory

  ![1557209792779](Pictures/Operating_System/1557209792779.png)

* xv6中实现IPC的数据结构：struct pipe

  ![1557209952876](Pictures/Operating_System/1557209952876.png)

* IPC - Message Passing

  * 不依赖共享变量的进程间交流方式，提供send和receive两种接口
  * physical comminication link：shared memory，hardware bus
  * logical communication link：logical properties

* Direct Communication

  * 接口：每个进程显示的调用send(P, message), receive(Q, message)
  * Communication link的实现细节：link是自动构建的；link和pair of process是一对一的；link可能是单向的unidirectional，但通常是双向的bidirectional

* Indirect Communication

  * 进程通过mailbox (port) 定位和接受message；每个maibox都有id，只有相互共享mailbox的进程才可以互相通信
  * 接口：每个进程通过mailbox中转通信，send(A, message), receive(A, message)
  * Communication link的实现细节：link仅当进程共享mailbox时才构建；link和pair of process是多对多的；link可以是单向的，也可以是双向的 
  * <Problem> P1/P2/P3共享mailbox A，P1 send，P2/P3 receive，谁收到？
    * 解决方法：link至多连接两个process；只允许同时一个process做receive；允许显示指定receiver

* 同步/异步消息
  * 同步消息 synchronous：block sender直到返回，block receiver直到收到消息
  * 异步消息 asynchronous：sender和receiver都不做block
* Buffering的实现有三种模式：Zero capacity (sender一直等待)，bounded capacity (当link被占满后sender等待)，unbounded capacity (无限长，sender不等待)

##### LRPC - Lightweight Remote Procedure Call

* Unix IPC 的方式：
  * 管道 pipes，信号 signals，Unix-domain sockets (用于同一主机)
  * 信号量 POSIX semaphores，FIFOS nmaed piped，共享内存 Shared memory segments，POSIX message queues
  * System V semaphore sets, System V message queues
* Unix IPC的问题
  * 比较重量级 heavyweight
  * 通常会使用polling

* Lightweight RPC Basic concepts
  * 简单的控制传输：client线程在server domain执行
  * 简单的数据传输：共享参数栈，增加寄存器
  * 简单的stub：highly optimized marshalling
  * 并发性设计：避免共享数据结构
  * 统计性结果：大多数message都比较短，几百byte的占到90%+
* IPC之前设计高开销的地方
  * stub会复制大量数据
  * message buffer会通过内核复制内容，4次
  * 访问验证
  * 消息传输 (队列)
  * scheduling，程序员看到线程跨域，系统实际上在不同的域中汇合两个线程
  * context switch，2次
  * dispatch，找一个接收线程来interpret消息，然后分派另一个线程，或者让另一个线程等待更多消息
* LRPC Binding：connection setup phase
  * 为调用接口中的每个procedure在内核中注册过程描述符(PDs)
  * 对于每个PD，参数栈(A‐stack)都在两个域中预先分配和映射读/写
  * 内核预先分配linkage record，以便从A‐stack返回
  * 将A‐stack列表作为绑定对象返回给客户端

* client thread上的调用顺序

  ![1557212448931](Pictures/Operating_System/1557212448931.png)

*  

------

第七讲 Exception

* Review

  * 两种IPC模型：shared memory，message passing
  * POSIX中的IPC方式：pipe，message passing，signal，shared memory，semaphore，etc.
* 辨析：Exception，Interrupt，System call

  * Exception：一种非法程序操作，能复现
  * Interrupt：由硬件设备产生的信号，不能复现
  * System call：用户程序可以请求OS操作，能复现

##### Exception

* Intel CPU上的Exception簇

  ![1557213531390](Pictures/Operating_System/1557213531390.png)

* IDT / Trap Vector in xv6

  * IDT是exception table的别称；有256个entry，每个entry都是handler；在处理相对应的interrupt时，需要给出 %cs 和 %eip
  * 可以通过 `int n` 调用System call

* Exception Handler

  * 处理器在栈上push return address的时候，可能是当前指令(page fault指令)，或者下一条指令(硬件中断)
  * 处理器还会在栈上push一些额外的处理器状态，当handler返回的时重启中断程序的必要内容，比如当前的condition code
  * 在user向kernel切换的时候，所有item都是被push到kernel stack，而不是user stack
  * exception handler在kernel mode运行，可以完全访问所有系统资源
  * 要往kernel stack中push的内容

  ![1558168046512](Pictures/Operating_System/1558168046512.png)

  * 为什么一定要push到kernel stack？

* 会触发user到kernel的几种事件 

  * Device interrupt：来自外部的中断，输入引脚 NMI引脚上 (nonmaskable interrupt)，输入引脚 INTR
  * Software interrupt：中断指令的执行，INT
  * Program fault：程序错误，执行出现错误的情况，除零错误

  ![1558168902842](Pictures/Operating_System/1558168902842.png)

* 硬件中断和软中断

  * 硬件中断是由与系统相连的外设(比如网卡 硬盘 键盘等)自动产生的. 每个设备或设备集都有他自己的IRQ(中断请求), 基于IRQ, CPU可以将相应的请求分发到相应的硬件驱动上(注: 硬件驱动通常是内核中的一个子程序, 而不是一个独立的进程).处理中断的驱动是需要运行在CPU上的, 因此, 当中断产生时, CPU会暂时停止当前程序的程序转而执行中断请求.
  * 软中断不会直接中断CPU, 也只有当前正在运行的代码(或进程)才会产生软中断. 软中断是一种需要内核为正在运行的进程去做一些事情(通常为I/O)的请求
  * 硬件中断和软中断的区别
    * 硬件中断是由外设引发的, 软中断是执行中断指令产生的.
    * 硬件中断的中断号是由中断控制器提供的, 软中断的中断号由指令直接指出, 无需使用中断控制器.
    * 硬件中断是可屏蔽的, 软中断不可屏蔽.
    * 硬件中断处理程序要确保它能快速地完成任务, 这样程序执行时才不会等待较长时间, 称为上半部.
    * 软中断处理硬中断未完成的工作, 是一种推后执行的机制, 属于下半部.

* Exception 发生的时候，有哪些必须满足的条件

  * 必须保存处理器的寄存器，用来恢复
  * 必须set成在kernel中执行
  * 必须要从kernel中挑一个位置来开始执行
  * 必须能够获取事件的各种信息，比如说system call argument
  * 必须能够安全的完成
  * 必须保证用户进程和kernel的隔离

* kernel中的interrupt函数的返回

  * iret指令：需要恢复上下文，从kernel切回user mode，继续执行用户程序

------

### 第八讲 Interrupt

* Intel 中的不同术语
  * Interrupt 异步的，设备生成
    * maskable：device生成，与IRQs相关联，可以被暂时禁用
    * nonmaskable：一些关键的硬件故障
  * Exception 同步的，来自软件
    * Processor-detected
      * Fault 故障，可纠正，可重新启动，如page fault
      * Traps 陷阱，不需要重新执行，例如断点
      * Aborts 中止，严重错误，进程通常会通过signal终止
    * Programmed exception 软件中断
      * int (system call), int3 (breakpoint)
      * into (overflow), bounds (address check)
* 一些术语
  * Vector, Interrupt vector, Trap number
  * IRQ: Interrupt Request
  * Interrupt, trap, fault, exception
  * Software interrupt / system call
  * IDT: Interrupt Descriptor Table 中断描述符表
  * ISP: Interrupt Service Procedure 中断服务程序

* 中断号有256个可能的值，Intel为 exception保留了前32个，剩下的可以用于自己的目的，例如处理device服务请求，或者处理system call

* Interrupt 概念

  * 中断有点像system call，但设备可以在任何时候产生中断
  * 主板上的硬件在device需要被 ”注意到“ 的时候，向cpu发乎信号，比如键盘信号；所以要对设备编程生成中断，并安排cpu 接受中断

* Interrupt 执行的顺序

  * push FLAGS 寄存器
  * 清除 IF 和 TF，EFLAGS中的interrupt able flag和trap flag
  * push CS
  * push IP
  * 获取interrupt vector的内容，置上IP和CS，开始执行ISP

* Interrupt hardware

  * IO 设备有唯一的/共享的 IRQ，IRQ由特殊的硬件映射到interrupt vector，然后传递给CPU，这种硬件叫做PIC programmable interrupt controller

  ![1558170109870](Pictures/Operating_System/1558170109870.png)

* APIC，IO-APIC 和 LAPIC

  * APIC，Advanced PIC，用于SMP系统 (对称多处理器，UMA架构)
    * 适用于所有现代系统，中断通过system bus路由到cpu
  * LAPIC 和 前端 IO-APIC
    * device是连接到 IO-APIC的，IO-APIC通过bus和LAPIC相连
  * interrupt路由
    * 有一点像网络的实现，允许广播或者选择性的route 中断，能够分配中断处理负载，路由到最低优先级的进程，如果同等优先级就仲裁或round robin

  ![1558170439701](Pictures/Operating_System/1558170439701.png)

* 为设备分配IRQ 

  * IRQ的分配因硬件不同为不同，有的是hardwire硬连线，有的是物理设置，有的是可编程的，PCI总线就是在引导分配IRQ
  * 一些IRQ的设计是由架构决定的：IRQ0:间隔计时器，IRQ2: 8259A级联引脚
  * Linux设备驱动程序在设备打开时请求IRQ
  * 一些硬件IRQ是预设定的
    * 系统定时器(IRQ0)，键盘控制器(IRQ1)，软盘控制器(IRQ6)，实时时钟(IRQ8)和数学协处理器(IRQ13)
  * 其他大部分IRQ是通过user决定的，可以通过硬件/跳线，也可以通过软件，如可安装的驱动程序和固件PNP
  * 还有一些可用于附加设备的IRQ
    * 调制解调器(IRQ5)，打印机(IRQ7)，声卡(IRQ9/IRQ10)，视频卡(IRQ11)和PS/2鼠标(IRQ12)，IRQ3和IRQ4通常用于串行端口，IRQ14和IRQ15用于IDE (primary和secondary)
  * interrupt vector中为IRQ所做的分配：32以下是不可屏蔽的 interrupt和exception，128 是system call，251-255用于IPI inter-processor interrupt 处理器间中断，IRQ的编号都是 IRQ# + 32

* Interrupt Priority

  * NMI：Non Maskable Interrupt 不可屏蔽中断

  ![1558176908532](Pictures/Operating_System/1558176908532.png)

* EOI：End of Interrupt

  * 在一个基于IRQ的中断程序结束时，会给PIC芯片发送EOI信号
  * 如果IRQ来自Master PIC，那么只向主PIC发出这个命令就足够了；如果IRQ来自Salve PIC，则需要向两个PIC芯片发出命令

* OS设计原则：Maximizing Parallelism

  * 让所有IO设备尽可能繁忙
  * 通常IO中断表示某项操作的结束，另一项要求应尽快发出
  * 大多数device是互不干扰彼此的数据结构的，没有屏蔽其他device的理由

* Handle Nested Interrupt

  * 尽快 unmask global interrupt
  * 只要reasonable，就re-enable来自该IRQ的中断；但这可能会导致重新进入相同的处理程序
  * 中断处理期间不启用 IRQ-specific的掩码

* Nested Execution

  * 中断可以被中断
    * 对于不同的不断，handler并不需要要重入reentrant；一小部分需要在禁用中断的情况下handle
  * 异常也可以被中断
    * 通过中断 (需要服务的设备)
  * 异常最多嵌套两层
    * 异常表示编码错误，可以exception - page fault，两层肯定到kernel了，这时候的代码不应该有bug，否则就是一个triple fault
    * 当发生故障时，CPU调用exception handler。如果此时发生错误，则称为double fault，CPU将尝试使用另一个exception handler处理该错误。如果该调用也导致错误，则系统将因为triple fault 而 reboot

* Interrupt Masking

  * mask的两种不同类型：global，selective
    * global就是延迟所有interrupt，selective就是mask掉单个IRQ，因为通常来自同一类型的几个中断的干扰最常见

* 有关 interrupt 和 exception 的三个关键数据结构

  * GDT，The global descriptor table
    * 定义系统的内存段及其访问特权，CPU有义务强制执行这些特权
  * IDT, The interrupt descriptor table
    * 为处理所有“中断”和“异常”的各种代码例程定义入口点
  * TSS，The task-state segment
    * 保存寄存器SS和ESP的值，CPU将在进入内核模式时加载这些值

* CPU 如何找到 GDT/IDT 存在哪里

  * 有两个专用的寄存器：GDTR和IDTR，两者都有相同的48位格式
  * 内核必须在系统启动期间设置这些寄存器(set-and-forget)
  * 特权指令:LGDT和LIDT用于设置这些寄存器值；非特权指令:用于读取寄存器值的SGDT和SIDT


  ![1558179202556](Pictures/Operating_System/1558179202556.png)

* CPU 如何找到 TSS 存在哪里

  * 专用系统段寄存器TR将描述符的偏移量保存到GDT中

  ​	![1558179309176](Pictures/Operating_System/1558179309176.png)

##### Bottom Half

* 中断处理的哲学/核心思想
  * 在interrupt handler中尽可能少地执行操作，把不重要的行动推迟到后面做，就形成了top和bottom上下两半

    * 上半部分：完成最小的工作量并返回 (ISR, interrupt service routines 中断服务程序)
    * 下半部分：延迟处理 (四种方法：softirqs, tasklets, workqueues,
      kernel threads，软中断，微线程，工作队列，内核线程)

    ![1558179662316](Pictures/Operating_System/1558179662316.png)

* Top Half 中做的事 ：Do it Now !
  * 只执行最小的公共函数：保存寄存器，unmask其他中断，最后撤销此次操作：恢复寄存器，返回到以前的上下文
  * 通常为了快，使用汇编写的；然后调用device driver中的合适的interrupt handler (用C写的)
  * IRQ在上半部分通常是被屏蔽的
  * 不要试图在top half中做太多工作，因为IRQ是被屏蔽的，让可能会让stack涨的太大；通常会在下半部分对request进行一个派对，并为延迟处理设置一个flag
* Top Half 如何找到handler
  * 在现代的硬件设备中，多个IO设备可以共享一个IRQ，因此可以共享interrupt vector
  * 多个ISR可以和一个vector相关联
  * Each device's ISR for that IRQ is called
  * Device determines whether IRQ is for it
* Bottom Half : Do it Later !
  * 中断 (与异常相反) 不与特定instruction相关联，也不和process相关联
  * 当前运行的process，在中断发生的时候，和这个中断没有任何关系
  * interrupt handler不能sleep ！
* interrupt handler不能sleep 所意味的事情
  * 不能 sleep 或 做任何可能导致sleep的事
  * 不能应用 current
  * 不能用 GPF_KERNEL 申请内存，它可能会sleep；只能用GPF_ATOMIC，它会失败
  * 不能调用schedule
  * 不能执行down的信号量操作，但可以使用up
  * 不能和user space进行数据通信，比如copy_to_user, copy_from_user
* Interrupt stack
  * 中断发生时使用的stack是哪一个
    * exception，当前process的kernel stack
    * interrupt，hard IRQ stack，1 per processor
    * softirqs：soft IRQ stack，1 per processor
  * 这些stack都会在boot的时候被kernel设置进IDT和TSS
* Softirqs
  * 静态分配:在内核编译时指定
  * 优先级从高到低：High-priority tasklets 高优先级微线程，Timer interrupts 定时器中断，Network transmission 网络传输，Network reception 网络接受，Block devices 块设备，Regular tasklets 正则微线程
* Softirqs 在什么时候运行
  * 在kernel 的一些行为之后：system call后，exception后，interrupt后 (上半部分，IRQs，定时器intr)，当scheduler运行ksoftirqs的时候
  * 软中断可以在多个CPU上同时执行，代码必须是可重入的
  * 当软中断运行时，硬件中断一直是enable的
  * 软中断可以重新安排自己的时间，这可能会饿死用户级process
  * 软中断调度一次只能运行有限数量的请求
  * 其余的由内核线程ksoftirqd执行，它与用户进程争夺CPU时间

* Tasklets
  * 建立在软中断之上，可以动态创建和销毁
  * 在schedule它的cpu上运行 (cache affinity 缓存关联)
  * 单个tasklets在执行期间会被lock，没有重入性的问题
  * tasklets可以在多个cpu上同时运行，同一个tasklet只能在一个cpu上运行
  * tasklets的问题
    * 比较难get right，要谨慎提防sleep，比系统中的其他task有更高的优先级，如果编码不好会产生无法控制的延迟，正在进行是否要消除tasklet的讨论
* Work Queue
  * 始终在kernel stack运行，是由scheduler调度的
  * softirqs和tasklets运行在中断上下文，work queue在伪进程上下文
    * 即一个有内核上下文，但没有用户上下文的进程
  * 因为这是一个伪流程上下文所以可以sleep
    * work queue可以被多个device共享，因此sleep会延迟队列中的其他工作
  * work queue是kernel-only的，没有user mode跟它相关联，所以不要尝试把数据复制到user space
* Kernel threads
  
  * 总是在kernel mode运行，也没有user context

![1558247236987](Pictures/Operating_System/1558247236987.png)

* 为什么interrupt handler不能sleep：防止死锁出现

![1558247436538](Pictures/Operating_System/1558247436538.png)

------

### 第九讲 System call

* 部分system call 列表

  ![1558247787338](Pictures/Operating_System/1558247787338.png)

* 跟踪system call的执行

  * Linux可以使用ptrace 和strace来跟踪syscall，每次执行syscall时都会打印输出，包括参数和返回代码

  ![1558248471000](Pictures/Operating_System/1558248471000.png)

*  调用syscall的方法
  * 从代码角度来看：application层通过library层，调用lib函数；application层直接写汇编 “int 0x80”
  * 从机器角度来看：int 0x80；SYSENTER；SYSCALL
* 库函数和syscall 的返回代码
  
  * 库调用在出错时返回-1，并在全局变量errno中放置特定的错误代码，系统调用返回特定的负值来指示 %eax 中存放的错误
* 传递syscall的参数
  * 第一个参数总是 syscall #
  * Linux允许最多6个附加参数，ebx，ecx，edx，esi，edi，ebp
  * 需要更多参数的syscall会把剩下的参数打包在一个struct中，并将该struct的指针作为第六个参数传递
  * Problem，必须要验证指针的合法性，可能是invalid的，如果NULL就会导致OS崩溃
* 如何验证user指针的合法性
  * 做一次彻底的检查cost太大了，要完全检查指针是否处于调用进程的所有有效区域之内
  * 解决方法是做一个不完全的检查：Linux对地址指针做一个简单的检查，并且只确定指针变量是否在用户内存的最大可能范围内(在用户空间里就可以了)，即使指针值通过此检查，特定值仍然可能无效
  * 在内核代码中取消对无效指针的引用通常会被解释为内核bug，并在控制台上生成Oops消息，然后杀死出错的进程。Linux做了一些非常复杂的事情来避免这种情况


* 处理user pointer带来的fault

  * 内核必须要用一段奇怪的代码 (paranoid) 来访问用户指针，比如 copy_from_user ，kernel知道哪些地址会抛出无效的内存访问异常
  * 当page fault的时候，kernel的page fault handler会检查出错的eip
  * 如果eip在一段 paranoid routines中，kernel就不会报错，相反就会调用 fixup代码
  * 这些paranoid的核心理念是：不直接访问用户的内存，用户都是危险的

  ![1558250163187](Pictures/Operating_System/1558250163187.png)

* 新的指令 SYSENTER/SYSEXIT 和 SYSCALL/SYSRET

  * int 0x80已经过时了
  * SYSENTER/SYSEXIT是intel先提出的，SYSCALL/SYSRET是AMD先提出的
  * 在32位kernel中，只兼容SYSENTER/SYSEXIT；64位kernel只兼容SYSCALL/SYSRET
  * SYSCALL/SYSRET 的延迟更低，大概快个25%
    * 简化了OS的调用和返回，消除了不必要的检查，加载预先确定的值到CS和SS两个段寄存器

* System call的执行流

  * 找到IDT中对应的第n个描述符
  * 检查%cs中的CPL是否 <= DPL，DPL是描述符中的特权级别，0是kernel，3是user
  * 将%esp和%ss保存在cpu内置的寄存器中，仅当目标段选择器的PL < CPL时才这样做
  * 从task segment descriptor加载%ss和%esp (TSS结构)
  * 按照%ss，%esp，%eflags，%cs，%eip的顺序，push到kernel stack上
  * 清除%eflags的一些位，IF和TF吧
  * 将%cs和%eip设为描述符中的值

##### VDSO 

##### Virtual Dynamic Shared Object 虚拟动态共享对象

* VDSO的动机
  * syscall造成的延迟不能忽略 (negligible)，比如说在syscall gettimeoftoday中，一点延迟的影响就特别大
  * 如何降低syscall的延迟？大部分的时间都用来save/restore上下文，如果没有mode switch，就不需要save/restore状态了
* gettimeofday的具体实现
  * 函数由kernel定义，在编译过程中作为kernel代码的一部分
  * 但运行的时候是在user space运行，代码被load到用户共享的页面中，称为VDSO，time通过只读的方式映射到了用户控件，只能在kernel mode下更改
* vsyscall 和 VDSO
  * vsyscall：用来执行特定的系统调用，减少系统调用的开销。某些系统调用并不会向内核提交参数，而仅仅只是从内核里请求读取某个数据，例如gettimeofday()，内核在处理这部分系统调用时可以把系统当前时间写在一个固定的位置(由内核在每个时间中断里去完成这个更新动作)，mmap映射到用户空间。这样会更快速，避免了传统系统调用模式INT 0x80/SYSCALL造成的内核空间和用户空间的上下文切换。
  * vsyscall的局限：分配的内存较小；只允许4个系统调用；Vsyscall页面在每个进程中是静态分配了相同的地址；
  * VDSO：提供和vsyscall相同的功能，同时解决了其局限；vDSO是动态分配的，地址是随机的；可以提供超过4个系统调用；vDSO是glibc库提供的功能

##### FLEX-SC

##### Flexible System Call Scheduling with Exception-Less System Call

* FLEX-SC的动机

  * 如何进一步降低syscall的延迟？延迟的来源主要在于state switch，要save/restore和check privilege，还有一些cache pollution

* Flexible System Call

  * 新的syscall机制，介绍了用户和内核共享的system call page
  * 用户线程可以把syscall请求push到system call page
  * 内核线程用轮询syscall到system call page
  * 通过将调用和执行解耦来消除同步

  ![1558253754026](Pictures/Operating_System/1558253754026.png)

*  

------

### 第十讲 IO

* 为什么需要 IO 子系统
  * device的种类特别多，每一种都不同，我们需要为他们设计标准化的设备接口
  * device都是 unreliable 的，会产生媒体错误和传输错误，我们要想办法让他们可靠
  * device都是 unpredictable 的，有的时候还比较 slow，我们要有合适的办法去管理他们
* IO 子系统的设计目标
  * 为不同种类的device提供统一的接口
  * 提供IO硬加的抽象层，用于管理和硬件的交互，隐藏硬件和操作的具体细节

* 三种类型的Device Interface

  * Character devices；Block devices；Network devices

  ![1558272791435](Pictures/Operating_System/1558272791435.png)

* Character Device 字符设备

  * 比如：键盘鼠标，串口，USB设备
  * 顺序访问，每次一个字符；经常使用开放的文件接口
  * IO command：get()，put()

* xv6 中的IO指令：inb(port)，outb(port, data)

* Block Device 块设备

  * 比如：disk driver，tape driver，DVD-ROM
  * 通过统一的块IO接口访问数据块；用原始的IO或者文件系统访问；通过memory-mapped的方式访问是可能的

* Network Device 网络设备

  * 比如：以太网，无线，蓝牙
  * 不同于block/character device，network device是有自己的接口的，不需要用文件接口；它提供特殊的网络接口，支持各种网络协议，可以收发网络数据包

* user 如何处理device带来的timing问题

  * Blocking IO：Wait

    * read/write时都将进程置于waiting状态，直到数据就绪

  * Non-blocking IO：Don‘t Wait

    * 从read/write请求立即返回，并成功传输字节数，但read可能什么都不返回，write也可能什么都没写进去

  * Asynchronous IO：Tell Me Later

    * read/write都会访问用户缓冲区的指针然后立即返回，稍后内核将填充缓冲区/接受数据，然后通知user

  * 同步和异步IO

    ![1558273730595](Pictures/Operating_System/1558273730595.png)

* DMA transfer的步骤

* DMA响应、DMA传输、DMA结束4个步骤

  * 请求：CPU对DMA控制器初始化，并向I/O接口发出操作命令，I/O接口提出DMA请求
  * 响应：DMA控制器对DMA请求判别优先级及屏蔽，向总线裁决逻辑提出总线请求。当CPU执行完当前总线周期即可释放总线控制权。此时，总线裁决逻辑输出总线应答，表示DMA已经响应，通过DMA控制器通知I/O接口开始DMA传输。
  * 传输：DMA控制器获得总线控制权后，CPU即刻挂起或只执行内部操作，由DMA控制器输出读写命令，直接控制RAM与I/O接口进行DMA传输；在DMA控制器的控制下，在存储器和外部设备之间直接进行数据传送，在传送过程中不需要中央处理器的参与。开始时需提供要传送的数据的起始位置和数据长度。
  * 结束：当完成规定的成批数据传送后，DMA控制器即释放总线控制权，并向I/O接口发出结束信号。当I/O接口收到结束信号后，一方面停 止I/O设备的工作，另一方面向CPU提出中断请求，使CPU从不介入的状态解脱，并执行一段检查本次DMA传输操作正确性的代码。最后，带着本次操作结果及状态继续执行原来的程序。
  * 由此可见，**DMA传输方式无需CPU直接控制传输，也没有中断处理方式那样保留现场和恢复现场的过程**，通过硬件为RAM与I/O设备开辟一条直接传送数据的通路，使CPU的效率大为提高。

* IO设备通知 (notifying) OS的方式
  * OS必须要被notify的情况：IO设备完成操作或出现错误
  * 两种notify method：polling，interrupt-driven
  * polling轮询：IO设备将完成/错误的信息放入device-specific的状态寄存器中，OS定期检查状态寄存器
    * 优点：低开销
    * 缺点：如有不频繁或者不可预测的IO操作，可能要浪费很多轮询周期
  * Interrupt-driven 中断驱动：优点：能很好地处理不可预知的事件；缺点：中断的开销相对较高
  * 有的设备融合了polling和interrupt，高带宽网络对第一个传入的包interrupt，之后就一直polling，知道hardware为空
* Device Driver
  * 定义：内核中与device直接交互的device-specific的代码
    * 支持标准的内部接口
    * 相同的kernel IO系统可以轻松地与不同的device driver交互
    * 使用 ioctl() syscall，支持特定于device的特殊配置

* IDE 端口

  * 端口 0x1F0-0x1F7
    * 0x1f0: write/read port
    * 0x1f2: number of sectors 
    * 0x1f3-0x1f5: sector number
    * 0x1f6: diskno and sector number
    * 0x1f7: command registers, status bit

  * 端口 0x3F6 interrupt control line   

*  

------

#### 第十一讲 File System：xv6 ~ ext4

* Virtual File System Interface
  * 现实中存在的问题：OS可能挂载了不同底层文件系统的多个分区，如果进程针对不同的文件系统还要提供不同的API的话就很麻烦
  * Linux使用虚拟文件系统接口（VFS)，向进程暴露POSIX的api，将请求转发到低层文件系统特定的驱动程序；windows的也差不多
  * 文件系统有ext2-4，NTFS，FAT32等
* xv6 FS design
  * xv6的文件系统实现了最低限度的Unix fs interface，包括`superblock，inode，dentry`
  * 缺点：设计不是很注重文件系统的layout，没有磁盘调度，cache策略是write-through，简化了磁盘数据一致性的麻烦，但性能不好
  * xv6的block size是512 byte

* xv6 FS disk layout

  * block 0是不用的，block 1是superblock，block 2之后分别是inode，bitmap，data block和log block

  ![1560002634798](Pictures/Operating_System/1560002634798.png)

* 概述：Free-space list bit vector

  * 就是in-use bitmap的意思，将空闲块列表表示为位向量
  * 2TB磁盘-> 512M块（block size 4M byte？？？）-> 64MB位 （1B=8bit）

* 概述：Multi-level Indexed Allocation
  * 主要是在描述inode的direct和indirect

  * ```
    [fs.h]
    #define NADDRS    (NDIRECT+1)
    #define NDIRECT   12
    #define INDIRECT  12
    #define NINDIRECT (BSIZE / sizeof(uint))
    #define MAXFILE   (NDIRECT  + NINDIRECT)
    ```

  * 文件大小，不用indirect最多12个块，用了的话最多12+128个块，每个块又512byte了

    * inode中的最后一个地址作为128个磁盘地址(512 / 4)的块的磁盘地址

  * 目录 directory，是特殊的文件，包含多个dirent结构

    * dirent是目录内的文件，field有 inode-num和filename

##### EXT File system

* inode 的优点
  * 优化了有很多小文件的文件系统的性能：每个inode都可以直接指向48KB的数，4MB文件只需要一个layer
  * 更快的文件访问：metadata的局部性更好，随机访问的时间会更少，因为都放在一起，不需要遍历FAT那样的链式结构
  * 更容易的自由空间管理：bitmap可以缓存在内存中，以便快速访问；inode和date space可以分开处理

* ext file system 概况
  * Ext文件系统是使用inode的：inode是数据块的imbalaneced tree，针对小文件很多这个常见情况进行了优化
  * 问题：ext的locality较差：inode与它们对应的数据离得很远，这将导致长时间的磁盘搜索
  * 问题：ext容易出现碎片，ext为新数据选择第一个可用块，并不尝试保持文件块的连续

* Fast File System (FFS) and Ext2

  * FFS的主要贡献：又花了spinning disk的性能
  * 发现：进程倾向于访问相同目录中的文件，有空间局部性
  * 关键思想：将directory groups和它的文件都放在cylinder group中，这个设计引入到了ext2中，称为block group

* block group

  * 在ext中，只有一组关键数据结构
    * 一个data bitmap，一个inodebitmap
    * 一个inode table，一个data block array
  * 在ext2中，每个block group都包含自己的关键数据结构

  ![1560003578547](Pictures/Operating_System/1560003578547.png)

* ext2的分配策略：ext2尝试将相关文件和目录保存在同一个block group中

* ext2的优点和缺点
  * 优点：ext2支持所有其他ext的特性，甚至还能做的很好，因为在空间局部性上做的很ok
  * 缺点：大文件必须跨block grooup；随着文件系统变得越来越复杂，文件系统损坏的几率也会增加；例如无效的inode、不正确的directory entry等，就是说有点脆

* 数据块寻址的文件大小上限

  ![1560003810728](Pictures/Operating_System/1560003810728.png)

* Extent 概述

  * 问题：对于大文件来说，indirect实际上非常低效，每1024个块读取(并查找)一个额外的块，这一点在删除大的CD/DVD图像文件时非常明显
  * extent用单一的descriptor描述了是一组连续的/相邻的块
    * 这是一种表示大文件的有效方法，更好的CPU利用率，更少的元数据IO，就是多了一个length的参数
  * 现代文件系统尽量减少碎片，因为它导致了很多的seek，性能低下；entent更适合于连续文件

  ![1560004008079](Pictures/Operating_System/1560004008079.png)

* 实现extent特性
  * ext4和NTFS都用了extent
  * ext4 inode包含4个extent，而不是块指针
    * 每个extent最多可以处理128MB的连续空间(假设为4KB块)
    * 如果需要更多区段，则分配一个data block；这就类似于一个indirect了

* Revisiting Directories
  * 在ext、ext2和ext3中，每个目录都是一个包含很多entry的文件
    * entry不是顺序存储的；有些被删除的entry还在，只是它们可能是空的
  * 问题：在大目录中搜索文件需要O(n)时间
    * 实际上，不能在目录中存储>10K文件，不然查找和打开文件花费的时间太长了（10k？）
* From Lists to B-Trees，目录entry的优化
  * ext4和NTFS将目录编码为b树，以将查找时间提高到O(log N)
  * b树是一种平衡树，它为磁盘上的存储进行了优化，项目以块的顺序存储

* ext4的优点和缺点
  * ext4的两个改变：使用extent，目录存储用b树
  * 优点：ext4(和NTFS)支持所有基本的文件系统功能，改进了ext3 block group的性能，extent和b树目录文件性能很好
  * 缺点：下一代文件系统有更好的特性，写时复制语义 copy-on-write semantics (btrfs和ZFS)
* 

------

#### 第十二讲 Crash Consistency

##### File System Durability & Crash Recovery

* Durability：耐用性
* 为什么 fs crash recovery比较困难
  * 这里举了一个文件系统crash的例子

##### Sync Metadata Update + fsck

* FS必须确保它可以恢复它的元数据(对实际FS的最低需求)：
  * 内部一致性，没有悬空的引用  dangling references，Inode和block free list 只包含used的item，一个目录中的名称要唯一等等
  * 弱语义FS提供了有限的保证：create、rename、delete的原子性，通常任何东西都没有持久性

* 应用怎么handle 弱语义？weak semantics
  * Fsync和rename(shadow copy技术)
  * Fsync强制持久性，仅当文件实际写在磁盘上时才return
  * rename是一个原子操作，只有旧名称或新名称，而不是半旧半新
  * Mac OS集中使用rename来确保原子性

* FSCK会做什么
  * check superblock：如，确保文件系统大小大于分配的块数，如果出现错误就使用superblock的另一个副本
  * check free blocks：扫描inode、indirect block、double indirect block，生成正确的bitmap
  * check inode state：检查类型，常规文件、目录、symbolic link等，清除可疑inode并清除inode bitmap
  * check inode links：通过扫描整个fs树来检查链接数是否对的上，如果count不匹配，修复inode；如果分配了inode，但没有dir包含它，则lost+found
  * check duplicate：两个inode指向同一个块
  * check bad block：指向某个超出范围的地址，fsck应该会移除指针
  * check directory：唯一一个fsck知道更多语义的文件，确保`. 和 ..`没问题，确保没有dir link超过一次，在一个目录中没有相同的文件名

* fsck的问题：太慢了！！

* Xv6-rev0策略：谨慎地安排磁盘写操作，以避免挂起引用

  ```
  1. initialize a new inode before creating dirent 
  2. delete dirent before marking inode free 
  3. mark block in-use before adding it to inode addrs[] 
  4. remove block from addrs[] before marking free  
  5. zero block before marking free 
  ```

* app-visible syscall semantics
  * durable：使用写穿缓存，同步I/O, O_SYNC
  * atomic：通常，Mkdir是一个例外
  * ordered：如果所有写入都是同步的

* Sync I/O vs. Async I/O
  * 异步I/O是一个很差的抽象，在很多方面：Reliability，Ordering，Durability，Ease of programming

  * 同步I/O更好，但是速度慢100倍，调用者被阻塞，直到操作完成


* Barrier: Flush the Disk
  * 磁盘的write buffer，磁盘将通知OS写入完成时，可能只是简单地放在write buffer里，数据没有在磁盘上，不durable，不ordered
  * 一种方案是禁用buffer，另一种方案是flush，强制将数据写入磁盘媒体
*  

------

#### 第十三讲 Journaling and ext3

* 概述：Recovery approach
  * 同步元数据更新 Synchronous meta-data update + fsck：用于xv6-rev0，在检查期间，同步元数据，比如文件大小
    * 同步元数据更新的要点在于有一个commit point
  * 日志(ext 3/4)、xv6-rev6和以下版本：在进行实际的元数据更新之前先写log，崩溃后，从日志中恢复
  * 软更新soft update(在FFS上修改FreeBSD fs)

* JFS：Journaling FS
  * 主要功能：加速崩溃后的恢复时间；大磁盘上的fsck可能非常慢，“消除崩溃后文件系统恢复时间非常长”
  * 使用JFS，只需在崩溃后从最后一个checkpoint重新阅读日志

* JFS 和 log-structured file system，LFS 论文读过
  * LFS只包含一个日志，所有内容都append到末尾
  * LFS指定了数据如何存储在磁盘上，JFS没有规定数据如何存储在磁盘上（是指layout吗）
* JFS的工作原理
  * 原理一：每一次disk update都看做是一个事务(原子更新)
    * 将新数据写入磁盘(日志)；在update commit之前，更新都不是最终的
  * 原理二：每一次block write的commit都是原子的（通过log保证）
    * 提交块是磁盘上的一个数据块；不一定要刷新到磁盘!

* 如何从日志中获取数据呢
  * commit之后，新的数据就会出现在日志中
    * 它需要被写回磁盘上的home location（先写log再写data）
    * 在将数据重新同步到磁盘之前，无法回收该日志空间（保证原子性）
* checkpoint
  * 关闭transaction，所有后续的文件系统操作都将进入另一个事务
  * 将事务刷新到磁盘(日志)，锁定缓冲区
  * 将所有内容刷新到日志后，更新journal header block
  * 只有在缓冲区同步到磁盘之后，才能在日志中解开缓冲区的锁定（缓冲区中是新更新的log部分）
  * 在日志中释放空间（相当于打了一个checkpoint）
* ext3 和 JFS 的对比
  * ext3相对ext2的一个主要改变就是增加了log，ext2是以前类似于xv6的无日志文件系统
  * 两者在两个独立的层
    * /fs/ext3，只是添加了事务的文件系统；/fs/jdb，记录日志的stuff(JFS)
  * ext3根据需要调用JFS：启动/停止事务，在unclean reboot（通常是crash发生了）之后请求日志恢复
  * 做复合事务：具有多个更新的事务

* Ext3 Structures
  * 在内存中：write-back block cache，per-transaction info
  * 在磁盘中：fs，circular log

* ext3的log中有什么
  * log superblock，记录starting offset and starting seq 
  * descriptor blocks
  * data block
  * commit block
  * 大概的结构就是：|super: offset+seq #|... |Descriptor 4|...blocks...|Commit 4| |Descriptor 5|... 

* ext3 如果实现比较好的性能

  * 方法一：批处理，每隔几秒提交一次，而不是在每次系统调用之后，因此每个事务都包含许多系统调用
  * 解释一：为什么批处理有助于性能?
    * 将固定事务成本分摊到多个事务中，包括描述符和data block
    * “写吸收” write absorbtion，批处理中的许多系统调用其实修改的都是相同的块，批处理就一起写了，省了一部分写(i-node、bitmap、dirent)
    * 更好的并发性，等待前一个系统调用完成了再继续做别的事，这样的情况会少一点
  * 方法二：Ext3允许并发事务和系统调用
    * 和批处理有一点细微的区别
    * 可能同时有多个事务状态：有些已经完全提交到磁盘日志中，有些人日志写入才做了一部分，还比如有的刚刚接收新系统调用的“open”
    * ext3每隔几秒提交一次当前事务 (或者用fsync())

* 一个事务完全提交到disk的整个过程

  ```
    1. block new syscalls，阻塞别的syscall
    2. wait for in-progress syscalls to stop()
    3. open a new transaction, unblock new syscalls
    4. write descriptor to log on disk w/ list of block #s
    5. write each block from cache to log on disk
    6. wait for all log writes to finish
    7. write the commit record
    8. wait for the commit write to finish
    9. now cached blocks allowed to go to homes on disk (but not forced)
    # log commit以后其实就好了，现在data cache里的内容允许被写进磁盘home了，但它是不是现在写都没事
  ```

* ext3 log体系在并发的时候能否保持正确性呢？

  * 没问题的，还会有lock保护，比如在同一个目录同时创建两个相同名字的文件是做不到的，因为第一个开始create的进程会拿到目录锁
  * 但也有其他东西是可以真正并发的(缓存中的不同块)，或者事务组合了两个系统调用的update也是在并发


* ext3 log体系有没有可能出现因乱序导致的脏读或者更新没读到呢？
  * 看ppt的意思好像是会的
  * 比较重要的一点，commit顺序必须与系统调用读/写状态的顺序一致，不然问题很大（如果顺序不对），Ext3牺牲了一些性能来获得正确性（也没办法吧？）
*  ext3 log体系允不允许 其他事务T2写T1事务要写的block？
  * ext3 allows T2 to start before T1 finishes committing -- 允许有一定程序的交错
    * T1: |-syscalls-|-commitWrites-|
    * T2:            |-syscalls-|-commitWrites-|
  * 好像有点危险，可能会破坏原子性
  * 解决方案：当T1关闭时，ext3向T1提供block cache的私有副本，T1从缓存的这个快照提交，使用copy-on-write是有效的；当T1提交时，副本允许T2中的系统调用继续进行（？？？）
  * 要点：正确性需要崩溃后+恢复状态，就好像syscalls是按原子顺序执行的一样，Ext3使用各种技巧来允许一些并发

* ext3 log体系什么时候可以重用之前事务使用的log space呢
  * 重用是肯定要有的，因为ext3是circular的
  * 一旦在日志中释放了T1之前的所有事务，并且T1缓存的块都被写到磁盘上的FS中，T1的部分就可以重用（这是一个check条件吧）；好像是有一个指针在维护当前最新的可以被重用的block在哪的
* ext3 log体系如何应对syscall的时候已经没有足够的空间的呢
  * 场景：假设我们把syscall的block添加到T2事务，到一半的时候，意识到T2不适合放在磁盘上（太大了之类的），我们不能提交T2，因为系统调用还没有完成；我们也不能退出这个系统，无法撤消系统扫描，T2中的其他系统调用程序可能已经阅读了它的修改（问题很大
  * 解决方法：reservation 预留
  * syscall提前声明一下它要用多少log space，不够就算了，panic掉返回一点信息

* ext3的性能测试案例
  * 测试1：在一个目录中创建100个小文件，xv6需要超过10秒(每个系统调用需要很多磁盘写操作)
  * 测试2：重复修改缓存中相同的direntry、inode、bitmap，因为批处理写吸收的存在好像问题不大
  * 测试3：然后提交几个元数据块和100个文件块
* ext3 crash了以后怎么recovery
  * 第一步，找到日志的开头——第一个non-free的描述符，可能可以根据日志“superblock”中的offset和seq#找
  * 第二步，找到日志的末尾，扫描到坏magic或没有出现预期的seq号，返回到上次提交记录
  * 第三步，replay第一步和第二步框定的所有块通过最后一个完整的事务（就是被crash整崩的那个）
* Durability of ext3
  * 综述，ext3不像xv6那样立即耐久稳定，
    * creat()返回 -> 可能数据还不在磁盘上，这时候crash事务就被撤销
    * 需要fsync(fd)强制提交当前事务，然后wait
    * 如果在每次系统调用之后都提交ext3，它的性能是否会很好?
      * 会log更多的块，但没有写吸收了
      * 每个系统调用均摊10毫秒，而不是0毫秒
* Ordered Mode vs Journaled Mode
  * Journal file content比较慢，每个数据块写两次，写log，写data
    * 那不这样做会更好吗？并没有；log肯定要先写，如果先更新metadata，crash可能会让文件指向带有其他人数据的块
  * 简单来说，journal mode的写顺序应该是：log meta，log data，home meta，不知道什么时候home data **（这个可能写错了，等我之后看笔记check一下）**
  * ext3 ordered mode
    * 不要将file content写入日志
  * 简单来说，ordered mode 的写顺序是log meta，home meta，不知道什么时候home data，log data省略了
  * 这样当然也是可能带来一些问题的
    * 问题：rmdir, re-use block for write() to some file, crash before rmdir or write committed
    * 解决：re-use 超危险，一定要syscall commit 以后才行，别还没commit就自说自话开始reuse了
* checksum
  * ext4相对于ext3的一点优化
  * 问题：在编写提交块之前，事务的日志块必须位于磁盘上，ext3在启动提交块写入之前等待磁盘显示“done”；为了提高性能，磁盘通常有write caches和re-order writes
  * 解决：提交块包含所有数据块的校验和
* xv6 和 ext3 比较
  * 咦这个还没比过吗
  * ext3修复了xv6日志的许多性能问题
    * 一次只有一个事务，现在可以并发
    * 同步写入磁盘日志，但是5秒窗口
    * 微小更新->整个块写入——yes(间接)
    * 提交后同步写入到home
  * ext3的log系统非常成功，但是没有checksum，ext4加上了
  * 但是对于使用fsync()的应用程序不是很有效

##### Virtual Disk & VMRAM

* 虚拟磁盘的特性 feature
  * 动态增长的image size，snapshot，de-duplication
  * 这些特性可以显著地简化VM部署、备份等任务
  * 虚拟磁盘在主要的云基础设施中得到了广泛的应用，例如OpenStack

------

#### 第十四讲 FS：FAT32 & NTFS

##### FAT File system

* cluster 和 sector

  * sector是磁盘上最小的存储单元，512 byte
  * cluster是可以用来保存文件的最小磁盘空间：**data cluster位于分区的元数据后面，不同的cluster大小取决于volume大小**

  ![1560078775928](Pictures/Operating_System/1560078775928.png)

* FAT的结构

  ![1560077093726](Pictures/Operating_System/1560077093726.png)
  * boot sector：卷volume的layout，fs structure，boot code
  * reserve sector：描述分区根目录中的文件和文件夹
  * FAT 1，original FAT，File allocation table 
  * FAT 2,dupliacte
  * root folder，描述root的file和folder
  * other folders and all files：主要就是data部分

* 结构：FAT boot sector

  * 位于每个分区的第一个逻辑扇区，在格式化volume时创建，以2字节扇区标记结束(总是0x55AA)


  * 组件 component：
    * 一个基于x86的CPU跳转指令
    * 原始设备制造商标识(OEM ID)
    * BIOS参数块(BPB)
    * Extented BPB
    * 可执行的启动代码

* 结构：FAT 1 and FAT 2

  * 将所有cluster标识为这样几种状态：unused, cluster in use by a file, bad cluster, last cluster in a file

  * FAT 2用于一致性检查程序

  * FAT是一种链式结构，这样一个个块块就是cluster

    ![1560077885407](Pictures/Operating_System/1560077885407.png)

* 结构：FAT root folder

  * FAT Root Folder Structure的entry：name，attribute byte，create time/date，last access date，last modification time/date，first cluster，file size

  * file naming：支持长文件名，main folder entry存8.3 short file name，secondary folder entry存long file name

    ![1560078444246](Pictures/Operating_System/1560078444246.png)

  * 短文件名要保证长度最多就那么长，THEQUI~1FOX，如果重了就THEQUI~2FOX，最后可以搞到T~999999FOX，再conflict就error

* ExFAT 的 file name search
  
* 首先按照hash搜索名称，通过比较哈希值来搜索目录中的每条记录；当找到匹配项时，将对文件名进行比较，以确保在发生冲突时找到了正确的文件
  
* FAT的优点和缺点
  * FAT的优点：
    * 目录和文件的层次树 Hierarchical tree
    * 可变长度的文件
    * 基本文件和目录元数据
  * FAT的缺点：
    * FAT32最多支持2TB磁盘（还好吧？不过FAT是u盘用的多）
    * 定位free chunk需要扫描整个FAT（这个太坑了
    * 容易出现内部和外部碎片，大文件的时候
    * 因为链式结构，读需要大量的随机搜索

##### NTFS

* NTFS Cluster
  * cluster：smallest allocated disk space to hold file，跟上面FAT一样的定义
  * 从分区开始按顺序排列逻辑集群号
  * 集群从扇区0开始(与FAT不同)
  * 软盘floppy disk不使用NTFS
  * 不同的集群大小取决于卷大小
  * ![1560079372934](Pictures/Operating_System/1560079372934.png)

* NTFS的结构

  ![1560079412908](Pictures/Operating_System/1560079412908.png)
  * NTFS boot sector：卷volume的layout，fs structure，boot code
  * Master File Table，这个是最重要的，包含file和folder的attribute
  * File System Data，Data no contained within MFT
  * Master File Table Copy， a copy of MFT

* 结构：Master File Table，MFT

  * 包含的属性：一个关系型数据库；rows：文件记录；columns：文件属性；每个文件至少包含一个条目entry

  * MFT的metadata file：master file table, master file table, log file, volume file, attribute definitions, root file name index, cluster bitmap .... 太多了不想写了我也没仔细看
  * MFT Zone
    * 作用有防止碎片，默认情况下占有12.5%的volume，按需分配额外的MFT区域

* NTFS File Record Attributes

  * File attribute 的定义：将每个文件和文件夹视为一组文件属性
  * Resident Attributes vs. Nonresident Attributes 常驻属性和非常驻属性
    * 小文件和文件夹完全包含在文件的MFT记录中(通常小于900字节)
  * File attribute 的类型：标准信息（访问模式，时间戳，link cnt），属性列表，文件名，data/index，object ID

* NTFS File naming

  * 如何生成简短的文件名：删掉不支持的字符（空格等），删掉多余的间隔符（逗号句号什么的），把文件名截断成6个字符，然后加~和数字
  * 这不就是FAT的操作吗

* NTFS Compression（file and folder）

  * NTFS压缩：在NTFS中实现，仅在磁盘中压缩，在将数据移动到内存之前解压
  * 移动和复制文件或文件夹：改变压缩状态，增加系统开销

* NTFS hard link
  * 在不复制原始文件的情况下为硬链接添加目录项
  * 应用程序可以使用任何硬链接修改文件
  * 不能在每个硬链接的基础上为文件提供不同的安全描述符

* NTFS Sparse Files 稀疏文件？？：该文件包含由零组成的大量数据

##### MBR & MOUNT

* Master Boot Record：MBR
  * 我印象中是一个磁盘分区的时候要用到的东西
  * ![1560081984823](Pictures/Operating_System/1560081984823.png)

* 磁盘分区最多可以分四个，第四可以弄成extended partitions，就可以继续加

* Mounting a File System 安装文件系统
  * 读取目标文件系统的superblock，包含关于文件系统的元数据，版本、大小、磁盘上关键结构的位置等
  * 确定安装点 mount point
    * Windows操作系统：选择一个驱动器字母
    * 在Linux上：将新文件系统挂载到特定目录下

* 为什么要“安全地弹出”一个设备?
  * 刷新缓存到该设备的写入
  * 干净地卸载该设备上的文件系统

------

#### 第十五讲 File System Flash FS

* xv6中的Transaction Semantics 

  * begin_trans, log_write, commit_trans, recovery

* 事务提交到磁盘的完整步骤

  * 为syscall开启一个transaction -> 把transaction标记为done -> 等待正在进行的syscall stop/return -> 写描述符对于要写的block s，写log -> 把每个块的内容从cache写到log上 -> 等待log写完 -> 添加commit记录 -> （可选）把块的内容写到home disk

* NV-RAM 中存在的一些问题

  * NV-RAM是被当disk用的，cpu的cache被视为memory，crash会丢失还没有write back的cache内容；层次结构已经发生变化了
  * CPU拥有cache flush 到 memory的指令

  ![1560125796756](Pictures/Operating_System/1560125796756.png)

##### Intro to flash file system

* 定义：flash file system

  * Flash文件系统是为在闪存设备上存储文件而设计的；传统的文件系统不能在flash文件系统上使用吗

* 闪存盘和普通磁盘的区别
  * flash disk organization：A chip (e.g. 1GB) => blocks (e.g. 512KB) =>    pages (e.g. 4KB) => cells（有点像体系结构那个）

  ![1560125994143](Pictures/Operating_System/1560125994143.png)

  * flash cell：是一个浮动栅晶体管，分为SLC和MLC
    * 浮栅上的电子数决定了阈值电压V，阈值电压表示逻辑位值(0或1)

  * SLC和MLC flash的区别：SLC一个cell存一个bit，性能好，耐久，容量小；MLC一个cell存两个bit，性能差，不耐久，容量大

* 闪存盘的特点

  * 不对称的读写，以及擦除erase特性
    * 读/写的unit是page，8-16KB
    * erase的unit的block，4-8MB
  * 物理限制，每次write都要erase一块block，erase-before-write的限制，以及每个block可以被erase的次数应该是有限的
  * 随机存取 random access：优化磁盘文件系统，尽可能避免磁盘查找；Flash设备没有机械盘那个寻道时间
  * wear leaving，当一个块被反复erase时，闪存设备就会磨损；所以写的block要设计的比较均匀
  * Heterogeneous cells：指MLC和SLC两种cell

* 用flash进行file storage 需要注意什么
  * naive的操作，直接1:1映射，适用于read-only，没有wear levelling，容易写穿block，不是很安全（在电源损耗方面）
  * Flash Translation Layer (FTL)，增加了一层manager抽象，适用于可写的file system，磨损比较平整，But, one journalling FS on top of the other

* 实例学习，真实的flash file system，flexFS

  * 目标：高性能，高容量，高耐久（什么都要
  * 方法：flexiable cell programming，SLC和MLC平衡着用，各取其长
    * MLC通过将数据同时写入LSB和MSB位，使用单元格的所有四个值
    * SLC通过将数据写入LSB位(或MSB位)，只使用单元格的两个值
  * 具体操作：利用flexible cell programming，提供高性能的SLC和高容量的MLC，提供一种处理MLC磨损特性差的机制

* flexFS的架构分析

  ![1560126923254](Pictures/Operating_System/1560126923254.png)
  * flash manager：管理不同的cell
  * performance manager：利用I/O特性，实现高性能、高容量
  * wear manager：保证合理的使用寿命，均匀分布erase

* 架构：flash manager

  * 有三种类型的block：SLC, MLC, free

  ![1560127426694](Pictures/Operating_System/1560127426694.png)

* 架构：performance manager

  * 关键技术：hot-and-cold，把经常读写的东西放在耐久性更好的SLC中

    * dynamic allocation, background migration, locality-aware data management

  * ![1560128158554](Pictures/Operating_System/1560128158554.png)

  * migration 的过程通常是放在background执行的，为了防止一整块出现IO request的response time delay，做一个切片

    ![1560128370190](Pictures/Operating_System/1560128370190.png)

  * dynamic allocation的算法
    * 有一个参数 α，![1560128480827](Pictures/Operating_System/1560128480827.png)
    * α 越大表示性能越好，迁移时间越短，SLC的页数少，写时间长，可以往SLC多放一点内容
    * copy is the time required to copy a single page from SLC to MLC
    * Np is the number of pages in SLC
    * Tpredict is the idle time of next time window predicted

* 架构：wear manager

  * wearing rate跟α的值是直接相关的，α比较大的话，涉及到的block数也会比较多
  * 尽量保证当前的wearing rate和expect rate相同（虽然不知道为什么要这样做），如果当前rate过低可以适当上调α，rate过高可以降低一点α

* 架构结论：提出了一种新的MLC NAND闪存文件系统，利用灵活的单元编程实现SLC性能和MLC容量，同时确保合理的wearing/lifetime

* 另一个可以的架构：SLC/MLC hybrid storage

  ![1560128889479](Pictures/Operating_System/1560128889479.png)

  * 由单片SLC芯片和多片MLC芯片组成
  * 使用SLC芯片作为MLC芯片的写缓冲区
    * 将经常访问的小数据重定向到SLC芯片
    * 将大量数据重定向到MLC芯片

##### Log-based File Systems，LFS

* 背景：

  * 计算机硬件一直在发展，RAM变得又便宜又大，但随机存取还是很慢
  * 这让我们希望改变磁盘的使用方式，把更多的数据缓存的放在RAM里，就可以做更少的磁盘读取
  * 可以做一个针对顺序写操作进行优化的文件系统，LFS

* LFS 概述

  * key idea：buffer内存中的所有写操作(包括元数据)，将这些segment按顺序写入磁盘，将磁盘视为循环缓冲区，陈旧的数据不会被覆盖（而是替换）
  * 优点：所有的写操作都是大的、连续的
  * 问题：如何在这种设计中管理元数据和维护结构?

  ![1560129246728](Pictures/Operating_System/1560129246728.png)

* LFS 具体一些问题的解决

  * buffering write，每一个inode指向自己文件中所包含的block

  * 如何找到inode：甚至要找的inode还可能有很多个副本

    * 解决方法，增加一个inode map的间接影射

  * inode映射分散在整个log中，怎么找到最新的inode map呢

    * 解决方法，加一个checkpoint模块指向最新的inode map，CR固定，总是cache在内存中，定期写入磁盘，例如30秒之类的

* LFS 读取文件实例分析

  ```
  1. Look up inode 1 in the checkpoint region
  	inode map containing inode 1 is in sector X
  2. Read the inode map at sector X
  	inode 1 is in sector Y
  3. Read inode 1
  	File data is in sectors A, B, C, etc.
  ```

* LFS的directory

  * LFS中的目录和普通文件存的方法也没什么不一样，由inode指向
  * 目录包含 name 到 inode 的一个 map

* LFS 垃圾回收

  * 每一个cluster都会有一个summary block（跟checkpoint好像不是一个东西），这个块中包含 block-inode的一个反向映射
  * garbage collector就读取summary block中的信息，查找过期的块

* LFS failure recovery
  * 主要还是依赖checkpoint
  * 整个恢复过程貌似很快，这里没有fsck（这应该是ext2，xv6里有的东西）
  * 恢复最后一个checkpoint，并查看在checkpoint之后可以恢复多少数据，可能会丢掉一部分

* LFS 总结
  * 这是一个很奇怪的设计，跟传统的文件系统结构都不太一样，不能很好地映射目录层次的关系，不是很清晰；但现在LFS被广泛接受了
  * 回顾一下SSD磁盘对file system的要求，要实现wear leveling，写最好分散一点；要定期进行垃圾收集，防止写放大；LFS看起来是SSD的理想文件系统
  * write amplification 和 write absorbtion
    * write absorbtion 是 ext3的批处理特性
    * write amplification体系结构里提过，写入放大（WA）是闪存和固态硬盘之间相关联的一个属性，因为闪存必须先删除才能改写，在执行这些操作的时候，移动（或重写）用户数 据和元数据(metadata)不止一次。这些多次的操作，不但增加了写入数据量，减少了SSD的使用寿命，而且还吃光了闪存的带宽（间接地影响了随机写 入性能）

* 新型的文件系统特性：copy-on-write
  * 现代文件系统吸收了LFS的思想，实现了copy-on-write
  * 更新后的数据被写入磁盘上的空空间，而不是覆盖原始数据，防止数据损坏，提高顺序写性能
  * 由LFS开创，现在用于ZFS和btrfs；btrfs可能是Linux中的下一个默认文件系统
  * 另外，默认情况下，LFS保存数据的旧副本，旧版本的文件可能有用，例如:意外删除文件

------

#### 第十六讲 File System GFS

##### Intro to GFS

- Flash的特点：读写不对称；读可以随便读，写最小是一个block而且要擦除原先的内容；所以要做一些load balance，加一层抽象做映射，减少flash的写操作数量

- GFS是基于任何人都可以买到的便宜结点来做的 (commodity)；上层有很多google自己的应用，比如google search，big table等

- GFS需要满足的特性：

  - 性能好，可扩展/可伸缩/scalability，可靠性，availability
  - failure比之前的分布式文件系统更加normal
  - 文件通常会比较大，google做search存的文件类型大多都是网页 (做index/存图片)
  - 文件的操作更多是append而不是overwrite
  - 做一个co-design，去掉文件系统中一些不必要的东西

- GFS的设计假设 design assumption

  - 硬件很容易坏掉；文件的容量都很大
  - 两种类型的读操作：large streaming reads, small random reads，大型流读取，小型随机读取
  - 一种类型的写操作：large sequential writes (大型顺序写入，但是有很高的并发度，因此更重要的是bandwidth)
  - 保证来自多个client的并发写中的原子性
  - 高持续带宽比低延迟更有价值

- 典型的workload类型

  - 读操作：large streaming reads, small random reads
    - 大型流读取通常要读1MB或更多，可能还是连续区域
    - 小的随机读取通常只是在任意偏移量上的几个KBs
  - 写操作：sequential writes，主要是append
    - 文件一旦写好，就很少再修改了
    - 在任意偏移量上的小的写并不是很高效的操作
  - 多个client(例如~100)并发地写一个文件，append操作
    - 例如，生产者-消费者队列，多路合并

- GFS 的 interface

  - 常见API：不是POSIX兼容的，create, delete, open, close, read, write
  - 特殊API：
    - snapshot 很快的构建文件/目录的tree，操作很快因为数据根本不改
    - record append 允许多个client同时向一个文件进行写操作

- 架构：design architecture

  - **组件：GFS client，GFS master，GFS chunkserver**

  ![1560143214322](Pictures/Operating_System/1560143214322.png)

  - GFS client, GFS master（一个，元数据）, GFS chunkserver（多个，数据）
  - chunkserver的size是fix的（对比于file），每个chunkserver都有一个64-bit的handle/类似于id
  - master存有file到chunk的映射，chunk的位置
  - **Important principle：**
    - **data flow和control flow分开，分别和master/chunkserver交互**；client直接与chunkserver交互所有文件操作，意味着可以通过基于网络拓扑的昂贵数据流调度来提高性能
    - **chunkserver和client都不会cache数据，因为数据太大了**；工作集通常太大而无法缓存，chunkserver可以使用Linux的缓存

- Single Master node

  - client不通过master进行读写，master将相关的chunkserver位置信息传递给client；client临时缓存chunkserver数据并直接访问chunkserver

  - master中只存着metadata，大概只是做一个分发
  - 有shadow master做容错 / 类似fat

- Metadata on Master

  - 三种meta：chunk namespace, map file - chunk, location of chunk replica
  - Master通过每个块的心跳消息监视chunkserver是不是还活着
  - GFS中没有inode，也没有symbolic link 和 hard link，每个文件和目录都表示为查找表中的一个节点，将路径名映射到元数据，使用前缀压缩有效地存储
    - `/foo/bar`就是文件名，所以删目录/改目录名很慢，但google本身就没这种操作

- The operation log

  - operation log是用来记录metadata的变化的（元数据是persistent存储的），要保证order以便于做恢复
  - master的恢复操作时通过operating log来做的
    - 为了最小化启动时间，主节点定期检查日志
    - 检查点以b树形式表示，可以直接映射到内存中，但是存储在dis中

- Chunkserver node

  - 通过心跳消息与master对话
  - **chunkserver对它自己的磁盘上有什么块或没有什么块拥有最终决定权——而不是master**

- Chunk size：chunk size是fix的，64 MB

  - 缺点：内部碎片造成空间浪费；小文件很少，大文件很多，所以浪费不算太过分（没看懂）；GFS的每个数据要存三备份；小文件由几个块组成，然后这些块从并发客户机获得大量流量3 ， 
  - 优点：client和master通信次数会变少；减少master上存储的metadata数量；由于客户机很可能对给定块执行许多操作，因此保持到chunkserver的持久TCP连接可以减少网络开销
  - chunk和master之间会有heartbeat

- Single master 采用这种设计的原因是什么？

  - 可以在master上有global knowledge，因为就一个
  - master不会成为瓶颈，client不会在master这里做读写操作，只是问chunk的location
  - master崩了以后，client会很快发现，会启动新的master，然后做一个新的DNS
    - 使用操作log和checkpoint，还可以在多台机器上复制主状态，以保证可靠；如果主进程失败，GFS可以在这些副本中的任何一个启动一个新的主进程，并相应地修改DNS别名
  - master和shadow之间的一系列问题
    - 一致性的问题？shadow master其实一直都可以提供读文件的能力，几乎是同步的
    - 可以先读shadow，写稍微等一会，等到master恢复
    - shadow会读master的operation log和checkpoint，master崩了的时候还可以先暂时对外提供master的服务
    - shadow不是master的镜像：它们比primary master慢了几分之一秒
  - 为什么不把shadow直接变成primary呢？
    - 因为有很多shadow，为了一致性还是等primary恢复比较好

- System interactions

  - mutation：几乎都是append的写操作，要写三备份
    - write，append，acts on all of the chunk’s replicas
  - lease：60秒，类似cse的lab 3，有renew和revoke
  - data flow，与control flow 分离
    - 线性push数据以避免瓶颈和高延迟link

- read/write algorithm

  - 如果写操作的时候secondary挂了，选择client重试，而不是primary重试；读操作没事(没看懂)

  ```
  Read algorithm
  1. 应用程序发出读取请求。
  2. GFS客户机从(文件名，byte range)->(文件名，chunk index)转换请求，并将其发送给master。
  3. master响应块chunk和replica位置(即存储副本的chunkserver)。
  4. 客户端选择一个位置并将(chunk handle、byte range)请求发送到该位置。
  5. chunkserver将请求的数据发送到client。
  6. client将数据转发给应用程序。
  ```

  ```
  Write algorithm
  1. 应用程序发出写请求。
  2. GFS客户机从(文件名，byte range)->(文件名，chunk index)转换请求，并将其发送给master。
  3. master响应chunk handle和(primary+secondary)复制位置。
  4. client将写数据推送到所有位置。数据存储在chunkserver的内部缓冲区中。
  5. client向primary发送写命令。
  6. primary确定存储在其缓冲区中的数据实例的串行顺序，并将该顺序的实例写入块。
  7. primary向secondary发送串行命令，并告诉它们执行写操作。
  8. seconary对primary有反应。
  9. primary response 返回client。
  
  注意:如果其中一个块服务器上的写操作失败，则通知客户机并重试写操作。
  ```

- master operation，职能范围：

  - replica placement;
  - creation, re-replication, rebalancing; 
  - garbage collection; 
  - stale replica detection

- Fault tolerance 和 diagnose 诊断

  - 快速恢复，Master和chunkserver的设计目的是恢复它们的状态并在几秒钟内启动
  - chunk replica，3-way mirror，可以跨多机器，跨多机架
  - 主要的机制 Master Mechanisms：有一个进程一直在后台扫，观察有DK的chunk
    - 记录对元数据所做的所有更改
    - log定期设置checkpoint
    - 在多台机器上复制log和checkpoint
    - 在多台机器上复制master state
  - 数据完整性 data integrity
    * chunk会分成64 KB的block，还有32 bit的checksum（多一层保护），还有read/write times校验，还可以对很少使用的数据进行background scan

- GFS 总结

  - 这是可以工业应用的强大文件系统，可以跑在商用的硬件上，比较scalable
  - 对于前面提到的指定任务和假设，性能良好
  - GFS的创新
    - 文件系统API是为程式化工作负载而定制的
    - single-master设计，简化协调
    - 元数据适合内存
  - flat namespace
  - 对组件故障有专门的处理：硬盘故障、数据损坏、网络断开等
  - 吞吐量很高：
    - 最小化master干涉操作，chunkserver本身发送和接收客户机数据

##### Intro to NFS

* 如何访问远端的文件

  * ftp，telnet等，都是很明确的访问远程资源的用户定向连接
  * 我们希望这个过程具有更高的透明度，允许用户像访问本地资源一样的访问远程资源
  * NAS，network attached storage

* file service typrs

  * upload/download model	
    * 优点当然是很简单
    * 缺点：浪费，可能用户只需要文件的一小部分；如果用户没有足够的空间把文件下载下来呢；如果其他人修改了要读到的文件呢
  * remote access model
    * 就像是api一样，提供远程的功能接口，比如create, delete, read, write
    * 优点是client可以只得到他们需要的部分东西，server可以管理文件系统的一致性
    * 缺点：可能server和network会出现拥塞，部分data可能会反复不停的被要求访问

* remote file service

  * file service：为client提供文件访问的接口
  * directory service，将文件的textual name（文本名称）映射到文件服务可以使用的内部位置（不是很懂）
  * client module，文件和目录服务的客户端接口
    * 如果操作正确，有助于提供访问透明性；例如在VFS层下实现FS

  ![1560148495444](Pictures/Operating_System/1560148495444.png)

* Server，stateful和stateless，有状态和无状态
  * stateful，server需要维护client-specific的状态
    * 更短的请求，处理request的时候性能更好
    * 维持cache coherence，因为server掌握了谁在做什么的信息
    * file locking是可能的（这是什么
  * stateless，server并没有client的任何信息
    * 每个request都要识别file和offset
    * server/client 可以崩溃后恢复
    * 不需要open/close
    * 如果在server上删除文件，则会出现问题
    * 不可能做file locing

* 应对repeat access的方法：cache
  
  * data在很多地方都有replica：server buffer cache，client buffer cache，client disk
* 实现cache的若干种策略
  * write-through：将数据缓存在客户机上，但将修改发送到服务器
  * delayed writes，write-behind/write-back：数据在本地缓存(注意一致性——其他数据不会看到更新)，定期(立即)更新远程文件，一次批量写入比多次少量写入更有效
  * read-ahead，prefetch：在需要数据之前请求数据块，在实际需要的时候最小化等待
  * write on close，承认我们有会话语义
  * centralized control，跟踪谁在每个节点上打开和缓存了什么，有状态文件系统，signaling traffic
* NFS，network file system 的设计目标
  * 任何机器都可以是client或server
  * 必须支持diskless工作站
  * 必须支持异构系统，因为会有不同的HW, OS，底层文件系统
  * 访问透明性
  * 从failure中恢复：无状态，UDP，客户端重试
  * 高性能，使用cache和prefetch

* NFS一些问题的解决
  * mount，Request access to exported directory tree
  * access，Access files and directories (read, mkdir, …)

* NFS的性能
  * 通常比本地慢一点，也正常吧
  * 通过在client上cache来改进
    * 目标:减少远程操作的数量
    * 缓存:read, readlink, getattr, lookup, readdir
      * Cache file data at client (buffer cache)
      * Cache file attribute information at client
      * Cache pathname bindings for faster lookup
  * server side
    * cache是通过buffer cache“自动”进行的
    * 所有NFS写操作都是直接写到磁盘的，write through

* NFS的问题

  * 文件的一致性
  * NFS假设了时钟是同步的
  * 不能保证能用使用append打开
  * lock不能工作，因为无状态，可以添加单独的锁管理器(有状态的)
  * 没有打开文件的引用计数，就可以删除自己/别人打开的文件
  * 假设有全局UID空间

  * 怎么看起来问题很多的样子....

------

#### 第十七讲 Scalable locking

##### Scalability tutorials

- scalability受限于阿姆达定律，取决于并行和串行的比例是多少

- 一些可能需要有点概念的常数（单位是访问时间）

  - LLC，最末级缓存

  ![1560151830992](Pictures/Operating_System/1560151830992.png)

  ![1560151846751](Pictures/Operating_System/1560151846751.png)

- 三种内存模型：共享cache，共享mem，私有mem

  ![1560151791370](Pictures/Operating_System/1560151791370.png)

- fd是有POSIX语义的，第一个打开的fd一定是3

##### Non-Scalable locking are dangerous

- spinlock是non-scalable的，在竞争很激烈的时候表现出的性能就不好

- 具体危险的地方在：当添加更多内核时，会导致性能崩溃；即使是很小的临界区也会导致性能崩溃

- xv6代码分析

  - `xchg`，类似`TestAndSet`，acquire锁之后第一件事是关中断 `pushcli()`；release最后 `popcli()`；放锁后下一个拿锁应该是随机的，但这建立在每个core访问那一块mem的时间都一样 (这个假设不一定成立) 
  - `xadd`，类似`TicketLock`，解决了公平性的问题；在保持cache coherence上开销很大

- Directory-based cache coherence

  ![1560152046256](Pictures/Operating_System/1560152046256.png)

- cache coherence维持的方法

  - 这个在体系结构中讲的更多
  - directory和snooping是常用的两种方式
  - 即使经过了cache coherence的修正，ticket lock的开销还是太大了，每一次更新ticket后，所有想要锁的人都会来问他要新的ticket值，几百几千个cycle就过去了

##### Scalable locking

- while太快了，在while中稍微做一些loop延长时间；通过wait减少等待lock的数量

  - 但这个提议被Linux否决了，没什么实质性的作用

- 问题的核心：大量的程序在等single cache中的`curr_ticket`这个成员

- MCS Lock：这是一个全局变量

  - waiting 只有0和1两个值，next是下一个要锁的，MCS结构体就两个成员

  - release 只有一次写操作，holder 改掉自己 next 的 wait值（从1改成0），程序都 spin 在 wait 这里

  - `fetch_and_store` 的作用是确定前一个是谁，返回他，并让它的 next 指向自己

  - `compare_and_swap`

    ```c++
    int compare_and_swap (int* reg, int oldval, int newval) 
    {
      ATOMIC();
      int old_reg_val = *reg;
      if (old_reg_val == oldval) 
         *reg = newval;
      END_ATOMIC();
      return old_reg_val;
    }
    ```

- 具体实现的一些边界情况

  - lock函数中，predecessor == NULL表示前面没人占着锁，如果 !=NULL就进if去排队
  - unlock函数中，如果还有下一个在等的，就要让拿走锁，改他的is_lock，他就从while loop出来了；如果没有在等了，还要再判断一遍...可能刚刚那个判断又过期了

```c++
mcs_node{
  mcs_node next;
  int is_locked;
}
mcs_lock{
  mcs_node queue;
}
function lock(mcs_lock lock, mcs_node my_node){
  my_node.next = NULL;
  mcs_node predecessor = 
        fetch_and_store(lock.queue, my_node);
  if(predecessor != NULL){
    my_node.is_locked = true;
    predecessor.next = my_node;
    while(my_node.is_locked){};
  }
}
```

```c++
function unlock(mcs_lock lock, mcs_node my_node){
  if(my_node.next == NULL){
    if(compare_and_swap(lock.queue, my_node, NULL){
      return;
    }else{
      while(my_node.next == NULL){};
    }
  }
  my_node.next.is_locked = false;
}
```

* 

------

#### 第十八讲 Synchronization Constructs 

- scalable locking：随着资源增长性能也线性增长
- non-scalable locking的危险性：会有cache coherence
- 上节课讲的两种scalable locking：MCS lock
  - 基本原理：链表，用wait来选择下一个
  - MCS锁比Ticket好的地方：core越多的情况下，吞吐量下降幅度比较小；MCS锁在core少的情况下，因为要新建node，所以开销比ticket大一些

##### Synchronization constructs 同步构造

##### Read-Write Lock 

- Example：OS网站的Calendar
- 互斥锁到读写锁
  - 四个接口：readerStart, readerFinish, writerStart, writerFinish
  - 有shared data，numreader，numwriter 标识读者写者的数量；但实际上writer number只可能是0或者1
  - 不能同时有读写，首先尝试用condition variable来实现
- 读写锁的实现

```
readerStart
	lock(metalock)
	while (numwriter != 0) wait(readcv, metalock)
	numreader++
	unlock(metalock)
	
readerFinish
	lock(metalock)
	numreader--
	if (numreader == 0) broadcast(writecv, metalock)
	unlock(metalock)
```

* 原子指令是锁住cache line，所有CPU拥有这个cache line都会被lock住，直到这条指令完成。这是在体系结构层面的，所以开销很大

- 读写锁存在的问题
  - 需要等待消息(当前#reader)
  - 需要发送消息(下一个阅读器)
  - 消息序列化获取，会占用大量的消息带宽
  - 解决方法：减少等待消息的时间 GOLL，减少消息数量 BR lock
- 经典问题
  - 初始情况 x=0, y=0
  - T1： x=1; if (y==0) print("a");
  - T2： y=1; if (x==0) print("b");
  - 有可能同时输出a和b，因为乱序执行或者write buffer；指令执行后不一定真的写进cache里了，可能还在write buffer里面
  - 怎么避免这种事情：加一条fence()，这条指令是等待直到write buffer刷进cache中，并不会直接催write buffer
  - 和原子指令的联系：原子指令自带fence效果，一定是cache层面顺序执行的

##### RCU Synchronization

- 原则上不想让读者没有任何block和metadata，对写者没有感知，在任何时候都可以直接读
- 由体系结构决定，8 bytes以下的读写都是原子的，所以对指针的修改是原子的
- 增加写者的cost，每次写的时候都copy一份，read-copy-update；但这样就会增加很多旧的资源（每次写都会有旧资源）
- 什么时候删除旧的资源：换完pointer以后，标识所有reader，当他们都结束以后就可以删了；（naive的实现方法）

##### Lock-free Synchronization

* 使用无锁的“乐观”同步，不受约束地执行临界区，并在最后检查是不是只剩自己一个（？？？）

------

#### 第十九讲 Bug survey

- Review：Read-Write Lock
  - 实现中存在的问题：writer被饿死的概率会比较大
  - 优化，当读者没有的时候再唤醒写者

##### Concurrency Bug Characteristics

- LOC： line of code
- Non-Deadlock Bug Pattern
  - atomicity violation：before-or-after，有的操作一定要用lock保护
  - order violation：执行有严格的先后顺序，malloc struct初始化一般是memset成0
- 如何触发bug
  - 要使用多少个thread？
  - 要使用多少个变量会参与进来？
  - 要访问多少次变量？
  - 统计结果，66%的bug只包含一个变量，Multi-Variable Concurrency Bug不是很多
  - 统计结果，触发bug大概3次访存左右就够了
  - 统计结果，96%的bug只有两个thread参与就够了
- other finding
  - 70%的concurrency bug导致程序crash或者hang
  - 重现bug是critical的
  - 程序员缺少debug工具
  - 60%的patch都包含了bug

##### Bugs in Exception Handler

- 不是很大的bug，但因为handler处理的不好，问题变得更大了
- other finding
  - 触发一个bug大概三个node够用了
  - failure大多数可以通过unit test触发，大多数可以看system log看出来的
- OS Bugs
  - belief set：MUST set，MAY set