## 操作系统

------

### 第一讲 Introduction & 8 Important Problems in Modern Operating Systems

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

### 第二讲 OS Structures

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

### 第三讲 PC Programming & Booting

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

### 第四讲 Memory init：xv6 & VM

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

### 第五讲 Process

* 逻辑地址 - 线性地址 - 物理地址的转换

  ![1556339216237](C:\Users\wxw\AppData\Roaming\Typora\typora-user-images\1556339216237.png)

  ![1556339247367](C:\Users\wxw\AppData\Roaming\Typora\typora-user-images\1556339247367.png)

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

    ![1556342655313](C:\Users\wxw\AppData\Roaming\Typora\typora-user-images\1556342655313.png)

* Process Control Block，PCB

  * 每个process都会有一个PCB，内容包括Process state, Process counter, CPU registers, CPU scheduling information, Memory management information, Accounting information, I/O status information
  * xv6 中的进程数据结构

  ![1556343005224](C:\Users\wxw\AppData\Roaming\Typora\typora-user-images\1556343005224.png)

* Context Switch 上下文切换

  * 调用syscall触发中断 - save当前进程的PCB - reload目标进程的PCB - 继续执行
  * 上下文切换需要保存的内容应该是存在进程对应的kernel stack中的
  * 上下文切换换栈的瞬间

  ![1556343241697](C:\Users\wxw\AppData\Roaming\Typora\typora-user-images\1556343241697.png)

* Process Scheduling Queue 进程调度队列

  * Job Queue：系统中所有的process
  * Ready Queue：系统中所有等待执行的process
  * Device Queue：系统中所有等待IO设备的process

* 两种Scheduler
  * Long-term scheduler / job scheduler：调度即将进入ready queue的进程，完成时间在秒/分钟级别，决定了multiprogramming的程度
  * Short-term scheduler / CPU scheduler：调度即将执行的进程，完成时间在微秒级别
  * scheduler对process的分类：IO-bound process和CPU-bound process

* Process的创建：fork，一次执行两次返回；execute，一次执行没有返回；奇妙的机制

  ![1556344453826](C:\Users\wxw\AppData\Roaming\Typora\typora-user-images\1556344453826.png)

*  

------

### 第六讲 IPC 

* Review Questions
  
  * TODO
  
* Threading Model

  ![1557209601573](C:\Users\wxw\AppData\Roaming\Typora\typora-user-images\1557209601573.png)

* Process cooperation的优点：information sharing, computation speed-up, modularity, convenience

* IPC的两种模型：如上图，message passing 和 shared memory

  ![1557209792779](C:\Users\wxw\AppData\Roaming\Typora\typora-user-images\1557209792779.png)

* xv6中实现IPC的数据结构：struct pipe

  ![1557209952876](C:\Users\wxw\AppData\Roaming\Typora\typora-user-images\1557209952876.png)

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

  ![1557212448931](C:\Users\wxw\AppData\Roaming\Typora\typora-user-images\1557212448931.png)

*  

------

#### 第七讲 Exception

* Review

  * 两种IPC模型：shared memory，message passing
  * POSIX中的IPC方式：pipe，message passing，signal，shared memory，semaphore，etc.
* 辨析：Exception，Interrupt，System call

  * Exception：一种非法程序操作，能复现
  * Interrupt：由硬件设备产生的信号，不能复现
  * System call：用户程序可以请求OS操作，能复现

##### Exception

* Intel CPU上的Exception簇

  ![1557213531390](C:\Users\wxw\AppData\Roaming\Typora\typora-user-images\1557213531390.png)

* IDT / Trap Vector in xv6

  * IDT是exception table的别称；有256个entry，每个entry都是handler；在处理相对应的interrupt时，需要给出 %cs 和 %eip
  * 可以通过 `int n` 调用System call

* Exception Handler

  * 处理器在栈上push return address的时候，可能是当前指令(page fault指令)，或者下一条指令(硬件中断)
  * 处理器还会在栈上push一些额外的处理器状态，当handler返回的时重启中断程序的必要内容，比如当前的condition code
  * 在user向kernel切换的时候，所有item都是被push到kernel stack，而不是user stack
  * exception handler在kernel mode运行，可以完全访问所有系统资源
  * 要往kernel stack中push的内容

  ![1558168046512](C:\Users\wxw\AppData\Roaming\Typora\typora-user-images\1558168046512.png)

  * 为什么一定要push到kernel stack？

* 会触发user到kernel的几种事件 

  * Device interrupt：来自外部的中断，输入引脚 NMI引脚上 (nonmaskable interrupt)，输入引脚 INTR
  * Software interrupt：中断指令的执行，INT
  * Program fault：程序错误，执行出现错误的情况，除零错误

  ![1558168902842](C:\Users\wxw\AppData\Roaming\Typora\typora-user-images\1558168902842.png)

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

  ![1558170109870](C:\Users\wxw\AppData\Roaming\Typora\typora-user-images\1558170109870.png)

* APIC，IO-APIC 和 LAPIC

  * APIC，Advanced PIC，用于SMP系统 (对称多处理器，UMA架构)
    * 适用于所有现代系统，中断通过system bus路由到cpu
  * LAPIC 和 前端 IO-APIC
    * device是连接到 IO-APIC的，IO-APIC通过bus和LAPIC相连
  * interrupt路由
    * 有一点像网络的实现，允许广播或者选择性的route 中断，能够分配中断处理负载，路由到最低优先级的进程，如果同等优先级就仲裁或round robin

  ![1558170439701](C:\Users\wxw\AppData\Roaming\Typora\typora-user-images\1558170439701.png)

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

  ![1558176908532](C:\Users\wxw\AppData\Roaming\Typora\typora-user-images\1558176908532.png)

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


  ![1558179202556](C:\Users\wxw\AppData\Roaming\Typora\typora-user-images\1558179202556.png)

* CPU 如何找到 TSS 存在哪里

  * 专用系统段寄存器TR将描述符的偏移量保存到GDT中

  ​	![1558179309176](C:\Users\wxw\AppData\Roaming\Typora\typora-user-images\1558179309176.png)

##### Bottom Half

* 中断处理的哲学/核心思想
  * 在interrupt handler中尽可能少地执行操作，把不重要的行动推迟到后面做，就形成了top和bottom上下两半

    * 上半部分：完成最小的工作量并返回 (ISR, interrupt service routines 中断服务程序)
    * 下半部分：延迟处理 (四种方法：softirqs, tasklets, workqueues,
      kernel threads，软中断，微线程，工作队列，内核线程)

    ![1558179662316](C:\Users\wxw\AppData\Roaming\Typora\typora-user-images\1558179662316.png)

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

![1558247236987](C:\Users\wxw\AppData\Roaming\Typora\typora-user-images\1558247236987.png)

* 为什么interrupt handler不能sleep：防止死锁出现

![1558247436538](C:\Users\wxw\AppData\Roaming\Typora\typora-user-images\1558247436538.png)

------

### 第九讲 System call

* 部分system call 列表

  ![1558247787338](C:\Users\wxw\AppData\Roaming\Typora\typora-user-images\1558247787338.png)

* 跟踪system call的执行

  * Linux可以使用ptrace 和strace来跟踪syscall，每次执行syscall时都会打印输出，包括参数和返回代码

  ![1558248471000](C:\Users\wxw\AppData\Roaming\Typora\typora-user-images\1558248471000.png)

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

  ![1558250163187](C:\Users\wxw\AppData\Roaming\Typora\typora-user-images\1558250163187.png)

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

  ![1558253754026](C:\Users\wxw\AppData\Roaming\Typora\typora-user-images\1558253754026.png)

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

  ![1558272791435](C:\Users\wxw\AppData\Roaming\Typora\typora-user-images\1558272791435.png)

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

    ![1558273730595](C:\Users\wxw\AppData\Roaming\Typora\typora-user-images\1558273730595.png)

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