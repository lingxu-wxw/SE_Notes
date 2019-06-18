

## 数字部件设计

------

### 第0讲 概述

* 单周期CPU

  ![1554129621526](Pictures/Digital_Component_Design/1554129621526.png)

* 流水线CPU

  ![1554129639762](Pictures/Digital_Component_Design/1554129639762.png)

------

### 第1讲 电路逻辑

* 运算器：能进行加减乘除等算术和逻辑运算的器件

* 图灵机：

  ![1554129719155](Pictures/Digital_Component_Design/1554129719155.png)

![1554129724147](Pictures/Digital_Component_Design/1554129724147.png)

* 冯诺依曼结构（普林斯顿结构）：是一种将程序执行存储器和数据存储器合并在一起的电脑设计概念结构，描述了一种实际通用的图灵机计算装置。结构提出了将储存装置与中央处理器分开的概念，依该架构设计出的计算机又称存储程序计算机

  ![1554129752616](Pictures/Digital_Component_Design/1554129752616.png)![1554129758937](Pictures/Digital_Component_Design/1554129758937.png)

* 哈佛结构：将程序执行储存和数据储存分开的存储器结构。数据和指令的储存可以同时进行，可以使指令和数据有不同的数据宽度，程序需要由操作者加载，处理器无法自行初始化

  ![1554129786226](Pictures/Digital_Component_Design/1554129786226.png)

* Machine Structure

  ![1554129802006](Pictures/Digital_Component_Design/1554129802006.png)

* FPGA(Field Programmable Gate Array现场可编辑逻辑门阵列)

  * FPGA作为特殊应用集成电路领域中的一种半定制电路而出现

  ![1554129888286](Pictures/Digital_Component_Design/1554129888286.png)

  * FPGA的基本逻辑单元：查找表LUT-look up table，触发器Flip-flop，多路器

  ![1554129916214](Pictures/Digital_Component_Design/1554129916214.png)

* HDL(hardware description language硬件描述语言)

  * 定义：能够描述description硬件结构的一种语言，不是设计design

  * 硬件描述的目的：刻画表达出所设计的硬件逻

  ![1554129937055](Pictures/Digital_Component_Design/1554129937055.png)

* Verilog

  ![1554129954374](Pictures/Digital_Component_Design/1554129954374.png)

* 逻辑门

  ![1554129963496](Pictures/Digital_Component_Design/1554129963496.png)![1554129968164](Pictures/Digital_Component_Design/1554129968164.png)![1554129972252](Pictures/Digital_Component_Design/1554129972252.png)![1554129977765](Pictures/Digital_Component_Design/1554129977765.png)![1554129983056](Pictures/Digital_Component_Design/1554129983056.png)

* 逻辑电平

  ![1554130000726](Pictures/Digital_Component_Design/1554130000726.png)![1554130004068](Pictures/Digital_Component_Design/1554130004068.png)

* **数字器件动态功率和静态功率**

  ![1554130032396](Pictures/Digital_Component_Design/1554130032396.png)

  ![1554130043153](Pictures/Digital_Component_Design/1554130043153.png)

  ![1554130077044](Pictures/Digital_Component_Design/1554130077044.png)

* MOS场效应管

  * nMOS: gate = 0, OFF; gate = 1, ON
  * pMOS: gate = 0, ON; gate = 1, OFF

  ![1554130111881](Pictures/Digital_Component_Design/1554130111881.png)![1554130118287](Pictures/Digital_Component_Design/1554130118287.png)

  ![1554130136582](Pictures/Digital_Component_Design/1554130136582.png)

* **用场效应管构造逻辑门**

  * nMOS: gate = 0, OFF; gate = 1, ON

  * pMOS: gate = 0, ON; gate = 1, OFF

  ![1554130168184](Pictures/Digital_Component_Design/1554130168184.png)![1554130172629](Pictures/Digital_Component_Design/1554130172629.png)

* 用场效应管构造传送门 transmission gates

  ![1554130203240](Pictures/Digital_Component_Design/1554130203240.png)![1554130206916](Pictures/Digital_Component_Design/1554130206916.png)

* 用逻辑门构造多路选择器 multiplex

  ![1554130221511](Pictures/Digital_Component_Design/1554130221511.png)![1554130226018](Pictures/Digital_Component_Design/1554130226018.png) 

* 用多路器实现查找表

  ![1554130242393](Pictures/Digital_Component_Design/1554130242393.png)![1554130247356](Pictures/Digital_Component_Design/1554130247356.png)

* 译码器

  ![1554130261302](Pictures/Digital_Component_Design/1554130261302.png)![1554130264866](Pictures/Digital_Component_Design/1554130264866.png)

* SR锁存器

  ![1554130279010](Pictures/Digital_Component_Design/1554130279010.png)![1554130282943](Pictures/Digital_Component_Design/1554130282943.png)

* D锁存器

  ![1554130304766](Pictures/Digital_Component_Design/1554130304766.png)![1554130308504](Pictures/Digital_Component_Design/1554130308504.png)

  ![1554130313755](Pictures/Digital_Component_Design/1554130313755.png)

* **D触发器**

  ![1554130362108](Pictures/Digital_Component_Design/1554130362108.png)![1554130366566](Pictures/Digital_Component_Design/1554130366566.png)

  ![1554130372062](Pictures/Digital_Component_Design/1554130372062.png)![1554130376485](Pictures/Digital_Component_Design/1554130376485.png)

* **寄存器**：本质就是触发器

  ![1554130404912](Pictures/Digital_Component_Design/1554130404912.png)

  ![1554130411038](Pictures/Digital_Component_Design/1554130411038.png)

* 

------

### 第2讲 电路器件

* 电阻

  * 在高频应用和某些场合，电阻的寄生电容和寄生电感不容忽视
  * 电阻的种类和封装形式众多，还有功率、精度等表征参数

  ![1554130505318](Pictures/Digital_Component_Design/1554130505318.png)

* 忆阻器

  * 忆阻器具有电阻的量纲，但他的阻值由流经他的电荷确定
  * 纳米忆阻器件的出现，有望实现非易失性随机存储器

* 电容

  * 定义式：C=Q/V

    ![1554130546090](Pictures/Digital_Component_Design/1554130546090.png) 

  ![1554130550373](Pictures/Digital_Component_Design/1554130550373.png)

  ![1554130554083](Pictures/Digital_Component_Design/1554130554083.png)

  *  超级电容的功率密度大（W/kg），但能量密度小（Wh/kg）

  ![1554130572294](Pictures/Digital_Component_Design/1554130572294.png)

  * 电容的电压和能量计算

    ![1554130605241](Pictures/Digital_Component_Design/1554130605241.png)![1554130612040](Pictures/Digital_Component_Design/1554130612040.png)

  * 低通滤波器以及容抗计算式：低通滤波器是容许低于截止频率的信号通过， 但高于截止频率的信号不能通过的电子滤波装置

    ![1554130633209](Pictures/Digital_Component_Design/1554130633209.png)![1554130637300](Pictures/Digital_Component_Design/1554130637300.png)

*  电感

  * 定义式 L = φ/i

    ![1554130670516](Pictures/Digital_Component_Design/1554130670516.png)![1554130677002](Pictures/Digital_Component_Design/1554130677002.png)

  * 反电动势、能量

    ![1554130682385](Pictures/Digital_Component_Design/1554130682385.png)

    ![1554130689187](Pictures/Digital_Component_Design/1554130689187.png)

* 四种电路基本元件之间的关系

  ![1554130709634](Pictures/Digital_Component_Design/1554130709634.png) 

* 电容、电感的基本用途小结

  * 滤波（包括电容的去耦作用，电感的隔离作用）
  * 储能
  * 构成振荡器（包括谐振天线等）或者选频网络

* 二极管

  * P型半导体：空穴是多子，自由电子是少子

    ![1554130759215](Pictures/Digital_Component_Design/1554130759215.png)

  * N型半导体：自由电子是多子，空穴是少子

    ![1554130786272](Pictures/Digital_Component_Design/1554130786272.png)

  * PN结的原理

    ![1554130822093](Pictures/Digital_Component_Design/1554130822093.png)

    ![1554130829471](Pictures/Digital_Component_Design/1554130829471.png)

  * 晶体二极管

    ![1554130840664](Pictures/Digital_Component_Design/1554130840664.png)

  * 常用二极管 

    ![1554130859426](Pictures/Digital_Component_Design/1554130859426.png)

* 三极管

  * 三极管的工作原理：工艺上保证发射结的面积比集电结的面积小

    ![1554130888456](Pictures/Digital_Component_Design/1554130888456.png)

  * 晶体三极管的放大作用

    ![1554130909554](Pictures/Digital_Component_Design/1554130909554.png)

    ![1554130915567](Pictures/Digital_Component_Design/1554130915567.png)

  * 特性曲线

    ![1554130926570](Pictures/Digital_Component_Design/1554130926570.png)

  * 3种放大电路：

    * 共射电路是放大电路中应用最广泛的三极管接法，信号由三极管基极和发射极输入，从集电极和发射极输出。因为发射极为共同接地端，故命名共射极放大电路。
    * 共集电极放大电路，输入信号是由三极管的基极与发射极两端输入的（在原图里看），再在交流通路里看，输出信号由三极管的发射极两端获得。因为对交流信号而言，（即交流通路里）集电极是共同端，所以称为共集电极放大电路

    ![1554130973151](Pictures/Digital_Component_Design/1554130973151.png)

* MOS管

  * 原理

    ![1554130987545](Pictures/Digital_Component_Design/1554130987545.png)

  * 图标

    ![1554131010101](Pictures/Digital_Component_Design/1554131010101.png)

  * 特性曲线

    ![1554131015962](Pictures/Digital_Component_Design/1554131015962.png)

  * 漏极电流Id的计算

    ![1554131020346](Pictures/Digital_Component_Design/1554131020346.png)

  * 场效应管与三极管的对比

    ![1554131036422](Pictures/Digital_Component_Design/1554131036422.png)

* 集成运算放大器

  * 定义

    ![1554131054843](Pictures/Digital_Component_Design/1554131054843.png)

  * 运算放大器

    ![1554131060321](Pictures/Digital_Component_Design/1554131060321.png)

  * 跟随器，缓冲器

    ![1554131079915](Pictures/Digital_Component_Design/1554131079915.png)

  * 反相放大器 

    ![1554131083766](Pictures/Digital_Component_Design/1554131083766.png)

*  

------

### 第3/4/5讲 课本内容

* Art of managing complexity

  ![1554131136736](Pictures/Digital_Component_Design/1554131136736.png)

* Binary Value (基带信号，波特率，调制)

* 组合逻辑和时序逻辑

  * 组合逻辑是memoryless的，输出由当前输入的值决定

  * 时序逻辑有memory，输出由当前和先前输入的值决定

   ![1554131163903](Pictures/Digital_Component_Design/1554131163903.png) 

* SOP form / POS form 与或式

* 卡诺图：由真值表向与或式转变的方法

  ![1554131192486](Pictures/Digital_Component_Design/1554131192486.png) 

*  

------

### 第6讲 单周期

* MIPS指令的功能分类

  ![1554288280029](Pictures/Digital_Component_Design/1554288280029.png)

* MIPS指令的三种格式

  ![1554288301497](Pictures/Digital_Component_Design/1554288301497.png)

* Datapath element 和 program counter

  ![1554288318075](Pictures/Digital_Component_Design/1554288318075.png)

* 双读端口的寄存器堆实现原理

  *  信号的两个读端口的寄存器号

  ![1554288336826](Pictures/Digital_Component_Design/1554288336826.png)

* 寄存器堆写端口的实现原理

  * 信号：写使能，写寄存器号，写寄存器内容

  ![1554288357517](Pictures/Digital_Component_Design/1554288357517.png)

* ALU中aluc的实现

  ![1554288373628](Pictures/Digital_Component_Design/1554288373628.png)

* 单周期CPU+指令寄存器+数据存储器

  ![1554288387937](Pictures/Digital_Component_Design/1554288387937.png)

* MIPS的部分指令

  ![1554288401331](Pictures/Digital_Component_Design/1554288401331.png) 

* MIPS部分指令编码

  ![1554288416454](Pictures/Digital_Component_Design/1554288416454.png)

*  

------

### 第7/8讲 流水线

* 流水线不会改善每一个任务的执行时间，但它能够提升整个系统任务执行的**吞吐率**。吞吐率取决于最慢的那个流水环节。 

* 指令流水线的吞吐量定义为单位时间里流出的完成指令数，其取决于指令流出流水线的速度

* 如果每一步都得到了最佳的平衡，那么每条指令在流水线上的平均时间的理想情况下等于

  ![1554288459423](Pictures/Digital_Component_Design/1554288459423.png)

* 流水线的分段

  ![1554288483192](Pictures/Digital_Component_Design/1554288483192.png)

* 流水线寄存器的重要作用

  * 每个时钟周期结束后，该段的所有执行结果都保存在流水线寄存器中，在下一个时钟周期作为下一个段的输入；通过流水线寄存器，后段流水段可以向前级反馈数据和控制信息

  ![1554288501572](Pictures/Digital_Component_Design/1554288501572.png)

* 流水线的启示

  ![1554288512535](Pictures/Digital_Component_Design/1554288512535.png)

* 衡量指令速度的指标 CPI 

  *  Cycles per instruction，每条指令的平均时钟周期数；流水线可以减少指令的平均执行时间，可以认为是减少了每条指令的平均时钟周期数CPI，也可以认为是减少了时钟周期长度，还可以认为在这两方面都减少了

* 数据通路

  ![1554288537556](Pictures/Digital_Component_Design/1554288537556.png)

* 在流水线中参与流水的包括：指令流（代码），数据流，控制流

* 流水线冒险

  * 结构冒险：也叫结构冲突，当硬件在指令重叠执行中不能支持指令所有可能的组合的时候，所发生的资源冒险
  * 数据冒险：在同时执行的几条指令中，一条指令依赖于前一条指令的结果数据，却得不到时发生的冒险
  * 控制冒险：流水线中的转移指令或其它改写PC的指令所造成的冒险

* 【习题1】

  ![1554288585895](Pictures/Digital_Component_Design/1554288585895.png)

  ![1554288591863](Pictures/Digital_Component_Design/1554288591863.png)

* 实现指令流水的两个最基本问题

  *  分段，为了重叠起来并行执行
  *  流动，能够向前同步推进执行和流水

* 结构冒险：结构冒险的问题出在指令集上

  ![1554288639829](Pictures/Digital_Component_Design/1554288639829.png)

  ![1554288650508](Pictures/Digital_Component_Design/1554288650508.png)

* 【习题2】

  ![1554288661362](Pictures/Digital_Component_Design/1554288661362.png)

  ![1554288667700](Pictures/Digital_Component_Design/1554288667700.png)

  * 数据引用会导致结构冒险，因为存储器只有一个，但是指令和数据可能都要用存储器，所有通常会把指令存储器和数据存储器分开

  ![1554288678444](Pictures/Digital_Component_Design/1554288678444.png)

* 数据冒险

  ![1554288693849](Pictures/Digital_Component_Design/1554288693849.png)

  ![1554288697735](Pictures/Digital_Component_Design/1554288697735.png)

* 数据直通技术 

  * 代码样例： DADD R1,R2,R3;  DSUB R4,R1,R5， R1发生数据冒险

    ![1554288739866](Pictures/Digital_Component_Design/1554288739866.png)                                                

  * 到ALU的数据来源：EX段末尾的ALU输出（e_valA），MEM段末尾的ALU输出端（M_valA, W_valA），MEM段末尾的存储器输出端（m_valM）

    ![1554288757482](Pictures/Digital_Component_Design/1554288757482.png)  

* 数据冒险的检测方法（可以用数据通路解决的部分）

  *  需要注意的问题：由于有一些指令不写寄存器，所以可能导致一些不必要的转发；对0号寄存器要特别对待

  ![1554288827314](Pictures/Digital_Component_Design/1554288827314.png)

  ![1554288831271](Pictures/Digital_Component_Design/1554288831271.png)

  ![1554288848966](Pictures/Digital_Component_Design/1554288848966.png)

  *  除了要判断有regwrite，不是0号寄存器，还要保证不是上一条指令用的，不然就会转发一个过时的数据过去，这里rd是输出端口 

  ![1554288867174](Pictures/Digital_Component_Design/1554288867174.png)

* 不能用数据通路解决的数据冒险

  * Load/use hazard: 因为rt是访存最后的输出端口

    ![1554288897281](Pictures/Digital_Component_Design/1554288897281.png)

  * 数字部件中会有预测分支错误吗？

* 控制冒险，几种简单的编译时调度方法

  ![1554288917632](Pictures/Digital_Component_Design/1554288917632.png)

* 动态分支预测

  ![1554288928735](Pictures/Digital_Component_Design/1554288928735.png)

* 由各操作组件花费时间计算出来各条指令的执行时间 

  ![1554288938164](Pictures/Digital_Component_Design/1554288938164.png)

* 流水线CPU

  ![1554288948052](Pictures/Digital_Component_Design/1554288948052.png)

*  

------

### 第9讲 Cache

* 存储器的现状

  *  半导体存储技术相对CPU处理能力及其处理速度的发展来说，相对发展速度严重滞后
  *  人们对存储器的要求是又大又快，这本来就矛盾，而且人们还要求其价格尽可能低廉
  *  CPU的处理速度要远大于存储器响应的速度
  *  存储器的访问速度是制约计算机处理能力的瓶颈

* Cache的定义

  *  cache通常是存储器层次结构中的第一层的名字，是距离处理器最近的存储层次

  ![1554289010208](Pictures/Digital_Component_Design/1554289010208.png)

* Cache的工作原理是基于局部性原理（时间局部性和空间局部性）

* 【习题1】

  ![1554289041728](Pictures/Digital_Component_Design/1554289041728.png)

  解答过程如下：

  ![1554289056403](Pictures/Digital_Component_Design/1554289056403.png)

  ![1554289061802](Pictures/Digital_Component_Design/1554289061802.png)

  ![1554289066962](Pictures/Digital_Component_Design/1554289066962.png)

  ![1554289070665](Pictures/Digital_Component_Design/1554289070665.png)

* 存储器层次结构的四个问题

  *  块的位置：一个从主存来的块，可以被放置在cache的哪里？
  *  块的标记：如何找到放在cache中的块？
  *  块的替换：如果块发生缺失，cache中哪个块应该被替换出去？
  *  写时策略：CPU执行写操作时，该怎么处理

* 块的位置

  ![1554289132048](Pictures/Digital_Component_Design/1554289132048.png)

  *  直接映射需要建立一个将主存中的每一个块对应到cache中的唯一位置的一个映射方法，通常是用“块地址 mod cache的块数”，方法简单，但是容易冲突
  *  全相联映射是哪里空就可以放哪里，按照某种算法来映射，这不容易冲突，但是映射方法和很复杂
  *  组相联：一个块首先被映射到一个组中，然后它可以被 放置到组中的任何一个块中；如果一个组中有n块，那么这种映射方法就称为n路组相联

  ![1554289169778](Pictures/Digital_Component_Design/1554289169778.png)

* 块的标记

  *  Cache中的每一个块结构都有一个地址标记给出该块的贮存块地址信息
  *  需要在标志中加入一个有效位来标明该块是否有效

  ![1554289192137](Pictures/Digital_Component_Design/1554289192137.png)

  *  这是一个两路组相连，一共512组的cache，一共1024个块，每个块大小64字节 

  ![1554289209756](Pictures/Digital_Component_Design/1554289209756.png)

  *  这是一个2路组相连，一共4组，总共能放8个块的cache，而主存大小是32个块

  ![1554289243932](Pictures/Digital_Component_Design/1554289243932.png)

  ![1554289247746](Pictures/Digital_Component_Design/1554289247746.png)

* 替换策略

  *  因为直接映射的话要是在cache中肯定是在固定位置的，所以不用考虑，如果这个位置不是想要的东西，就替换掉

  ![1554289263370](Pictures/Digital_Component_Design/1554289263370.png)

  ![1554289267602](Pictures/Digital_Component_Design/1554289267602.png)

  *  对于大容量cache来说，LRU和随机替换算法几乎没有什么差别
  *  对于小容量cache，LRU替换算法最优，FIFO也比随机算法稍微好一点

* 写回策略

  *  Amdahl定律：高性能的设计不能忽视写操作速度对系统性能的影响

  ![1554289299929](Pictures/Digital_Component_Design/1554289299929.png)

  ![1554289315299](Pictures/Digital_Component_Design/1554289315299.png)

  ![1554289318731](Pictures/Digital_Component_Design/1554289318731.png) 

  ![1554289323286](Pictures/Digital_Component_Design/1554289323286.png)

* cache性能评价

  *  对存储器层级结构较合理的评价方法是采用平均存储器访问时间  

  ![1554289349592](Pictures/Digital_Component_Design/1554289349592.png)

  *  【习题】

  ![1554289361262](Pictures/Digital_Component_Design/1554289361262.png)

  ![1554289365806](Pictures/Digital_Component_Design/1554289365806.png)

  ![1554289370517](Pictures/Digital_Component_Design/1554289370517.png) 

  ![1554289375057](Pictures/Digital_Component_Design/1554289375057.png) 

  ![1554289391013](Pictures/Digital_Component_Design/1554289391013.png)

* Cache性能优化

  *  Cache性能优化的方向有减少缺失次数/提高命中率，也可以是降低缺失代价，比如使用多级cache 

  ![1554289405000](Pictures/Digital_Component_Design/1554289405000.png)

  ![1554289409346](Pictures/Digital_Component_Design/1554289409346.png)

* 核心公式

  ![1554289433968](Pictures/Digital_Component_Design/1554289433968.png)

  - 这个代表1000条指令有多少次缺失

  ![1554289447258](Pictures/Digital_Component_Design/1554289447258.png)

  ![1554289450695](Pictures/Digital_Component_Design/1554289450695.png)

  ![1554289457502](Pictures/Digital_Component_Design/1554289457502.png) 

  *  缺失率 = 1000条指令有几次data缺失/1000条指令有几条data指令，单位：次/条

  ![1554289467032](Pictures/Digital_Component_Design/1554289467032.png)

  *  多级cache中

  ![1554289479026](Pictures/Digital_Component_Design/1554289479026.png)

  ![1554289482727](Pictures/Digital_Component_Design/1554289482727.png)

  ![1554289495915](Pictures/Digital_Component_Design/1554289495915.png)

  ![1554289501214](Pictures/Digital_Component_Design/1554289501214.png)

  ![1554289505288](Pictures/Digital_Component_Design/1554289505288.png)

  ![1554289510424](Pictures/Digital_Component_Design/1554289510424.png)

  *  1000次访存，667条指令，每条指令平均1.5次访存，L1 cache直接命中一次访存需要1个周期
  *  一次访存平均存储器访问时间5.4周期，所以1000次访存要5400个周期，那么一次访存平均耽搁时间就是5.4-1周期，每条指令的平均耽搁时间（停顿时间）就是4.4 * 1.5周期
  *  每条指令的平均存储器停顿周期是6.6周期，那667条指令需要停顿667 * 6.6=4400个周期，总时间是667条*（正常访存1.5个周期 + 平均指令停顿6.6周期）=5400周期

*  

------

### 第10讲 虚存 

* 虚存产生的原因

  *  消除小而受限的主存容量对程序运行及编程造成的影响
     *  允许单用户程序的大小超过主存的容量
     *  程序员能在整个CPU的地址空间范围内自由编程
  *  允许在多个程序间有效而安全的共享内存
     *  主存中只存放各个程序的活跃部分

* 虚拟存储器的本质目的

  * 解决 大的程序寻址空间 和 小的物理主存空间 之间的矛盾

  ![1554289628610](Pictures/Digital_Component_Design/1554289628610.png)

  ![1554289632757](Pictures/Digital_Component_Design/1554289632757.png)

* 虚拟存储器

  *  一个磁盘上的块可以放在内存中的什么位置：全相连
  *  如何在内存中查找一个块：页表
  *  当发生虚拟存储器缺失时，应该替换哪个块：LRU
  *  写操作时会发生什么：写回法

* 虚拟存储器

  ![1554289667979](Pictures/Digital_Component_Design/1554289667979.png)

  ![1554289672593](Pictures/Digital_Component_Design/1554289672593.png)

  ![1554289677764](Pictures/Digital_Component_Design/1554289677764.png)

* 





 

