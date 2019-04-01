## 体系结构复习

------

### 第一讲 概述：从集成电路到数据中心

- 计算机架构：设计、分析、选择和互连硬件部件以制造出满足功能、性能和成本目标的计算机的科学和艺术
- IC (integrated circuit) 集成电路
- 最早的电子通用计算机：ENIAC，by 1946
- 晶体管：替代笨重的真空管和机械继电器，现代计算机的基础

* VLSI (Very Large Scale Integration)：超大规模集成电路

* 抽象层级：Application - Software system - Hardware system - Module - Gates - Circuits - Devices - Physics

* 名词：Silicon Ingot 硅锭，Wafer 晶片,  Naked Die 裸模,  Packaged Die 组合模具

* 半导体：N型（自由电子），P型（空穴）

* 晶体管结构：nMOS晶体管在栅极为低电平时OFF，高电平时ON；pMOS晶体管在栅极低电平时ON，高电平时OFF

  ![avatar](../Pictures/Computer Architecture/1553873703370.png)

* 晶体管Gate宽度：Gate Length = 2λ，feature size

  ![1553872260560](Pictures\Computer Architecture\1553872260560.png)

* 摩尔定律：当价格不变时，集成电路上可容纳的元器件的数目，约每隔18-24个月便会增加一倍，性能也将提升一倍

* Scale out ：横向扩展，往系统中添加更多组件（eg，增加集群中的结点数）

* Scale Up ：纵向扩展，往系统中的单一组件添加更多资源（eg，提升内存）

* HPC Center/supercomputer，高性能计算中心 ：高性能组件，注重吞吐量 throughput

* IDC(Internet Data Centers)，互联网数据中心：价格低廉，商用组件，注重服务延迟 latency

* 一个典型的数据中心

  名词：Server racks 服务器机架, A/C systems 空调系统, Power Distribution Units 配电单元, UPS(Uninterruptible Power System) 不间断电源, Energy Storage Cabinets 储能柜, Switch Gears 开关齿轮

  ![1553872982341](Pictures\Computer Architecture\1553872982341.png)

* 数据中心的三大支柱：power system, cooling facility, ICT Equipment (Information and Communication Technology，信息和通信技术)

* 数据中心TCO (Total Cost of Ownership) 总拥有成本：

  CapEX (Capital Expenditure) 资本支出 + OpEx (Operational Expenditure) 运营支出

* Summary

  * What is computer architecture
  * History of IC
  * Transistor basics
  * Feature length
  * HPC vs IDC
  * Scale up/out
  * Energy/power issues
  * The trend of computer architecture research

* 

------

### 第二讲 指令集架构

* Review

  * ENIAC：使用十进制，每个数字10个真空管，可以存储20个10位数字
  * 从晶体管到集成电路；从单体服务器到数据中心
  * 制造过程 (fabrication process) 的feature size：晶体管的最小横向维度
  * 可扩展性问题 (scale out/up)：指数增长的计算 vs 飞速增长的能源需求

* 计算机设计的层次 aspects

  * 架构 architecture：指令集架构 - instruction set architecture
  * 实现 implementation：微架构 - micro-architecture
  * 物理层设计 physical design：chip realization

* 指令集架构

  * 定义：defines data and control flow
    * 保存数据的存储资源：memory，addressing
    * 转换数据的指令：arithmetic/logic，floating point
  *  另一种定义：defines set of programmer visible state (程序员可见状态集)，instruction format and semantics (指令格式和语义)

* 计算机架构的发展史

  ![1554005252580](Pictures\Computer Architecture\1554005252580.png)

* 四种传统的架构：stack，accumulator（直接操作内存），register-memory（CISC），register-oriented（RISC）

  ![1554004987623](Pictures\Computer Architecture\1554004987623.png)

* 复杂指令集 CISC

  * 80年代中期的主导风格
  * 编译器容易实现，更少的代码
  * stack-oriented instruction set
    * 通过栈传递参数，保存程序计数器 IP
    * 显示地push/pop指令
  * register-memory architecture
    * 算术指令可以访问内存
  * condition codes：设置为算术和逻辑指令的副作用 side effect

* 采用CISC的处理器

  * IA-32：Intel Architecture， 32 bit
    * IA-32 registers：Program registers(eax, ecx, edx, ebx, esi, edi, esp, ebp),  condition codes, PC(eip), Memory
    * Processor State：为下一条指令提供上下文而在指令末尾保存在处理器中的信息
    * Processor Power State
  * X86-64： x86 instruction set, 64 bit
  * IA-64：一个完全新的高性能指令集架构，安腾系列的的Intel 64位微处理器

* 精简指令集 RISC

  - 现代的RISC可以追溯到1980s
  - 更少，更简单的指令
    - 完成相同的task需要更多的指令
    - 可以在small/fast的硬件上执行
  - register-oriented instruction set
    - 有许多提供给参数，返回值的寄存器（32个）
  - load-store architecture
    - 只有load/store指令可以访问内存
  - no condition codes

* 采用RISC的处理器：MIPS

  * 全拼：Microprocessor without Interlocked Pipeline Stages
  * 指令类型：R类型，I类型，J类型

  ![1554006637756](Pictures\Computer Architecture\1554006637756.png)

  ![1554009565424](Pictures\Computer Architecture\1554009565424.png)

* 指令集是硬件软件直接的接口

  * 高级程序语言 high level language - 汇编程序 low level language 指令集 ISA - 数据通路 register level transfer - 逻辑门电路 - CMOS 晶体管

  ![1554006772160](Pictures\Computer Architecture\1554006772160.png)

  ![1554007542882](Pictures\Computer Architecture\1554007542882.png)

* User ISA 和 System ISA

  * User ISA：使应用程序正常工作

    * 这是编译器在将高级语言中指定的算法映射到机器指令时所使用的ISA的子集
    * 指代那些对应用程序可见的指令集：data flow，ALU operations， control flow

    ![1554007424976](Pictures\Computer Architecture\1554007424976.png)

  * System ISA：管理/共享资源

    * 这是为低级O/S子系统用汇编语言精心编写的ISA的子集（eg. scheduler, virtual memory, device drivers）
    * 指代那些助管软件可见的指令集，比如OS，用于管理硬件资源

    ![1554007514074](Pictures\Computer Architecture\1554007514074.png)

* 优秀的指令集的特点 Good interface design

  * 背景：更大的CPU，技术瓶颈改变(power)，编译技术进步 (寄存器分配)，程序风格改变 (汇编，面向对象)，应用程序改变 (多媒体，深度学习)
  * 兼容性：具有多种实现
  * 普遍性：在多种场景使用
  * 提供到higher level的方便功能
  * 允许在lower level做有效的实现

* 组合逻辑和时序逻辑

  * 边缘触发：数据仅在clock edge被采样

* 哈佛架构 Harvard Architecture

  * 将指令和数据的存储和信号通路物理层面地分开

  ![1554008207952](Pictures\Computer Architecture\1554008207952.png)

* 五级流水线：指令级并行

  * 阶段：Instruction fetch -> Instruction decode and Register file Read -> Execute or Address calculation -> Memory access -> Write back

  ![1554008258099](Pictures\Computer Architecture\1554008258099.png)

* 理想的流水线

  * 一致的子过程划分 - 平衡pipeline状态
  * 相同的计算 - 统一的指令类型
  * 独立的计算过程 - 最小化pipeline暂停

* 阶段量化 Stage Quantization

  * 将一些子过程合并：更短的stage间延迟
  * 将一些子过程拆分：子过程的更细粒度

  ![1554009162952](Pictures\Computer Architecture\1554009162952.png)

* 流水线槽 pipeline slots

  * 分类：front-end, back-end, retiring, bad speculation
  * 前端表示处理器核心的第一部分，后端负责获取后面执行的操作
    * 分支预测：预测下一条执行指令的地址
    * cache lines：获取和解析指令
    * 解析成微指令 uOps
  * 前端绑定metric, 表示处理器前端对后端的slot fraction供应不足

* Summay

  * Architecture vs microarchitecture
  * Evolution of instruction sets
  * CISC(IA32) vs RISC(MIPS)
  * Machine interfaces
  * User/System ISA
  * MIPS instruction field
  * Single-cycle MIPS
  * Ideal pipeline
  * Stage quantization
  * Pipeline slot

------

### 第三讲 指令级并行化探索 I

* Review

  * ISA, micro-architecture, physical design
  * Evolution of ISA
  * CISC vs RISC, IA32 and x86
  * MIPS instruction fields
  * Machine interface, user ISA and system ISA
  * Good interface design
  * Hardware elements
  * Simple MIPS pipeline
  * Pipeline speedup and pipeline design challenge

* Dependence and Hazards

  * 依赖关系的定义：反应程序的执行顺序，暗示存在hazard的可能性，决定了parallel的程度

  * Hazard：由乱序指令，重叠执行等引起

  * 三种依赖：

    * data dependence：easy for determine for registers, hard for memory location

      eg.  c = a + b; e = c + d;

    * name dependence

      anti-dependence : eg. a = b + c; b = c + d;

      output dependence：eg. a = b + c; a = d + e;

    * control dependence：分支语句

  * 可能的数据冒险类型：RAW, WAR, WAW

    ![1554102383105](Pictures\Computer Architecture\1554102383105.png)

  * 三种流水线冒险：

    * structural hazard 结构冒险
    * data hazard 数据冒险：通过转发和预测来避免 bypassing or forwarding，但不能规避load/use hazard
    * control hazard 控制冒险

  * pipeline interlock：检测数据冒险、暂停pipeline的硬件机制称为pipeline interlock

    ![1554107402981](Pictures\Computer Architecture\1554107402981.png)

* 动态调度：记分牌算法 Scoreboarding

  * 核心：out-of-order execution, control-centric

  * FU/Function unit：包括Adders, multipliers, ALUs, register files, load/store units

  * 不同类型的FUs![1554104613004](Pictures\Computer Architecture\1554104613004.png)

  * Scoreboarding的四个阶段

    * Issue：检查结构冒险和WAW冒险，可能stall
      * unit是否有空闲
    * Read operands：如果没有RAW冒险，读取operands
    * Execution：遵循记分牌的指示
    * Write result：检查WAR冒险，可能stall
      * 是否有之前的指令读取自己目标寄存器中的值（RO阶段过后就可以了），遍历当前unit的Fi是否在其他unit的Fj，Fk中出现，并且Rj，Rk为Yes

    ![1554104945676](Pictures\Computer Architecture\1554104945676.png)

  * Scoreboarding的九个field

    * Op：unit中正在执行的操作
    * Fi：目标寄存器号
    * Fj, Fk：源寄存器号
    * Qj, Qk：产生Fj，Fk的function unit（Integer, Add等）
    * Rj, Rk：表示Fi，Fj是否ready的flag
    * Busy：表示unit是否busy

  * Scoreboarding执行界面

    * 执行时间是指在RO处停留的时间，贴图是中途的执行截图

    ![1554105118965](Pictures\Computer Architecture\1554105118965.png)

    ![1554106193184](Pictures\Computer Architecture\1554106193184.png)

* 动态调度：Tomasulo‘s Algorithm

  * Tomasulo's Algorithm的要点
    * 保留站 Reservation Station
    * Load/Store Buffers
    * 公共数据总线 Common Data Bus：Data flow approach:，指令可以在操作数available的瞬间开始执行
    * 寄存器重命名 Register Renaming：指令中的寄存被tag/指向保留站的pointer代替，排除了name dependence

  ![1554106061159](Pictures\Computer Architecture\1554106061159.png)

  * Tomasulo's Algorithm的三个阶段

    * Issue：从queue中获取指令（顺序）
    * Execution：执行（可能乱序）
    * Write result：结束执行，写回数据（可能乱序）

  * Tomasulo's Algorithm，保留站的field

    * Op：unit中正在执行的操作
    * Vj, Vk：源操作符的值（不是name）
    * Qj, Qk：产生Fj，Fk的RS
    * Busy：表示RS或FU是否busy

  * Tomasulo's Algorithm执行界面

    * 执行时间是指在EX处停留的时间
    * 值在算出来存进register result status的同时更新保留站的内容

    ![1554106576255](Pictures\Computer Architecture\1554106576255.png)

    ![1554106942583](Pictures\Computer Architecture\1554106942583.png)

* Scoreboard 和 Tomasulo的对比

  * Tomasulo的关键特征
    * 用Reservation Stations (RS) 实现分布式控制
    * 用Common Data Bus (CDB) 广播所有结果
    * 用tags来标识数据的值
  * Tomasulo 与 scoreboard 不同的地方
    * 分布式冒险检测，用RS来控制
    * 数据结果被同时转发到function Unit, 用CDB

* Summary

  * Pipeline stall and bubble
  * Dependency and hazards
  * RAW, WAR, WAW
  * Forwarding and pipeline interlock
  * Functional units
  * Dynamic scheduling and OoO(Out-of-order execution)
  * Scoreboarding
  * Tomasulo's Algorithm

------

###  第四讲 指令级并行化探索 II

* 
