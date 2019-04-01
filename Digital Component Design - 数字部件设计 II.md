

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

*  



 

