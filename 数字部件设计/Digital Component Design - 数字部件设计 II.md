

## 数字部件设计

------

### 第0讲 概述

* 单周期CPU

  ![1554129621526](http://ww3.sinaimg.cn/large/006tNc79ly1g4bau80dzqj30fe08zq47.jpg)

* 流水线CPU

  ![1554129639762](http://ww3.sinaimg.cn/large/006tNc79ly1g4bats3gowj30fe09tdhd.jpg)

------

### 第1讲 电路逻辑

* 运算器：能进行加减乘除等算术和逻辑运算的器件

* 图灵机：

  ![1554129719155](http://ww3.sinaimg.cn/large/006tNc79ly1g4bbn4mftej30b404gq3n.jpg)

![1554129724147](http://ww2.sinaimg.cn/large/006tNc79ly1g4ba9omgqsj30cg06wjsz.jpg)

* 冯诺依曼结构（普林斯顿结构）：是一种将程序执行存储器和数据存储器合并在一起的电脑设计概念结构，描述了一种实际通用的图灵机计算装置。结构提出了将储存装置与中央处理器分开的概念，依该架构设计出的计算机又称存储程序计算机

  ![1554129752616](http://ww3.sinaimg.cn/large/006tNc79ly1g4ban5pd5jj305b04x749.jpg)![1554129758937](http://ww4.sinaimg.cn/large/006tNc79ly1g4bd23huv7j309d04m0sx.jpg)

* 哈佛结构：将程序执行储存和数据储存分开的存储器结构。数据和指令的储存可以同时进行，可以使指令和数据有不同的数据宽度，程序需要由操作者加载，处理器无法自行初始化

  ![1554129786226](http://ww3.sinaimg.cn/large/006tNc79ly1g4bd5sdlhtj309t05taa4.jpg)

* Machine Structure

  ![1554129802006](http://ww1.sinaimg.cn/large/006tNc79ly1g4baaanpnnj30cd05zwfa.jpg)

* FPGA(Field Programmable Gate Array现场可编辑逻辑门阵列)

  * FPGA作为特殊应用集成电路领域中的一种半定制电路而出现

  ![1554129888286](http://ww1.sinaimg.cn/large/006tNc79ly1g4bd1isrptj30cx06g3zr.jpg)

  * FPGA的基本逻辑单元：查找表LUT-look up table，触发器Flip-flop，多路器

  ![1554129916214](http://ww1.sinaimg.cn/large/006tNc79ly1g4ban2gdidj30bz053aa3.jpg)

* HDL(hardware description language硬件描述语言)

  * 定义：能够描述description硬件结构的一种语言，不是设计design

  * 硬件描述的目的：刻画表达出所设计的硬件逻

  ![1554129937055](http://ww4.sinaimg.cn/large/006tNc79ly1g4b9h4vlf1j30b706n3yu.jpg)

* Verilog

  ![1554129954374](http://ww1.sinaimg.cn/large/006tNc79ly1g4bcwh3ve0j30b006cwf1.jpg)

* 逻辑门

  ![1554129963496](http://ww4.sinaimg.cn/large/006tNc79ly1g4ban1mudhj302h02dq2q.jpg)![1554129968164](http://ww3.sinaimg.cn/large/006tNc79ly1g4bat71cdgj302202cmwy.jpg)![1554129972252](http://ww2.sinaimg.cn/large/006tNc79ly1g4bauejybej302i02fa9v.jpg)![1554129977765](http://ww4.sinaimg.cn/large/006tNc79ly1g4baas17pqj302h02fglf.jpg)![1554129983056](http://ww2.sinaimg.cn/large/006tNc79ly1g4bd6euui8j302n02gt8j.jpg)

* 逻辑电平

  ![1554130000726](http://ww2.sinaimg.cn/large/006tNc79ly1g4bbn6p2otj309x053wet.jpg)![1554130004068](http://ww2.sinaimg.cn/large/006tNc79ly1g4b9h1lkgnj309p05saa7.jpg)

* **数字器件动态功率和静态功率**

  ![1554130032396](http://ww3.sinaimg.cn/large/006tNc79ly1g4bd5ojgg0j30bt01uq2w.jpg)

  ![1554130043153](http://ww1.sinaimg.cn/large/006tNc79ly1g4bcvrs06ej305h01bdfo.jpg)

  ![1554130077044](http://ww1.sinaimg.cn/large/006tNc79ly1g4bd84q7p1j309h074mxk.jpg)

* MOS场效应管

  * nMOS: gate = 0, OFF; gate = 1, ON
  * pMOS: gate = 0, ON; gate = 1, OFF

  ![1554130111881](http://ww3.sinaimg.cn/large/006tNc79ly1g4b9h4egy2j308t066aag.jpg)![1554130118287](http://ww2.sinaimg.cn/large/006tNc79ly1g4ban9jt5xj307v06vjrl.jpg)

  ![1554130136582](http://ww1.sinaimg.cn/large/006tNc79ly1g4bamt3adjj308k06pmxe.jpg)

* **用场效应管构造逻辑门**

  * nMOS: gate = 0, OFF; gate = 1, ON

  * pMOS: gate = 0, ON; gate = 1, OFF

  ![1554130168184](http://ww4.sinaimg.cn/large/006tNc79ly1g4baawrytfj305h05q74b.jpg)![1554130172629](http://ww3.sinaimg.cn/large/006tNc79ly1g4bd5pysh1j307104aq2x.jpg)

* 用场效应管构造传送门 transmission gates

  ![1554130203240](http://ww1.sinaimg.cn/large/006tNc79ly1g4bd3vhju2j302j03sq2r.jpg)![1554130206916](http://ww3.sinaimg.cn/large/006tNc79ly1g4ban949jsj307o02mwek.jpg)

* 用逻辑门构造多路选择器 multiplex

  ![1554130221511](http://ww4.sinaimg.cn/large/006tNc79ly1g4bd6w3oobj304i03wglj.jpg)![1554130226018](http://ww1.sinaimg.cn/large/006tNc79ly1g4bat6mjlyj303f03sq2r.jpg) 

* 用多路器实现查找表

  ![1554130242393](http://ww2.sinaimg.cn/large/006tNc79ly1g4b9h853dcj303i03uglh.jpg)![1554130247356](http://ww2.sinaimg.cn/large/006tNc79ly1g4b9hcu1ewj303x03owec.jpg)

* 译码器

  ![1554130261302](http://ww1.sinaimg.cn/large/006tNc79ly1g4bd2uiawdj305i062gln.jpg)![1554130264866](http://ww1.sinaimg.cn/large/006tNc79ly1g4bd5phr76j305w064jrc.jpg)

* SR锁存器

  ![1554130279010](http://ww1.sinaimg.cn/large/006tNc79ly1g4bd837ut9j304q03gzk5.jpg)![1554130282943](http://ww1.sinaimg.cn/large/006tNc79ly1g4bamro7d0j3065033gln.jpg)

* D锁存器

  ![1554130304766](http://ww3.sinaimg.cn/large/006tNc79ly1g4bd83o2muj309302umx4.jpg)![1554130308504](http://ww2.sinaimg.cn/large/006tNc79ly1g4b9gw2ii9j309302y3yi.jpg)

  ![1554130313755](http://ww2.sinaimg.cn/large/006tNc79ly1g4baug0062j308k04mdg1.jpg)

* **D触发器**

  ![1554130362108](http://ww1.sinaimg.cn/large/006tNc79ly1g4bd4iwccqj305j03v3yg.jpg)![1554130366566](http://ww4.sinaimg.cn/large/006tNc79ly1g4bbn4tjchj307a03u74f.jpg)

  ![1554130372062](http://ww1.sinaimg.cn/large/006tNc79ly1g4bd3icygvj305d02i747.jpg)![1554130376485](http://ww1.sinaimg.cn/large/006tNc79ly1g4ba9jyq90j305t02jq2v.jpg)

* **寄存器**：本质就是触发器

  ![1554130404912](http://ww3.sinaimg.cn/large/006tNc79ly1g4bd5rf7v7j30a106cdg3.jpg)

  ![1554130411038](http://ww4.sinaimg.cn/large/006tNc79ly1g4bcwyhe52j30fe09mt94.jpg)

* 

------

### 第2讲 电路器件

* 电阻

  * 在高频应用和某些场合，电阻的寄生电容和寄生电感不容忽视
  * 电阻的种类和封装形式众多，还有功率、精度等表征参数

  ![1554130505318](http://ww4.sinaimg.cn/large/006tNc79ly1g4batk7ob4j30c107xq44.jpg)

* 忆阻器

  * 忆阻器具有电阻的量纲，但他的阻值由流经他的电荷确定
  * 纳米忆阻器件的出现，有望实现非易失性随机存储器

* 电容

  * 定义式：C=Q/V

    ![1554130546090](http://ww3.sinaimg.cn/large/006tNc79ly1g4bd3u4nllj30dm0463yl.jpg) 

  ![1554130550373](http://ww2.sinaimg.cn/large/006tNc79ly1g4bau6k3npj30ec023jrr.jpg)

  ![1554130554083](http://ww2.sinaimg.cn/large/006tNc79ly1g4baud42zwj30d403vq3i.jpg)

  *  超级电容的功率密度大（W/kg），但能量密度小（Wh/kg）

  ![1554130572294](http://ww2.sinaimg.cn/large/006tNc79ly1g4bd5r0jz0j30fe07ujsc.jpg)

  * 电容的电压和能量计算

    ![1554130605241](http://ww1.sinaimg.cn/large/006tNc79ly1g4b9gwzmtkj302s018jr6.jpg)![1554130612040](http://ww2.sinaimg.cn/large/006tNc79ly1g4b9h6qgwhj302s01egle.jpg)

  * 低通滤波器以及容抗计算式：低通滤波器是容许低于截止频率的信号通过， 但高于截止频率的信号不能通过的电子滤波装置

    ![1554130633209](http://ww3.sinaimg.cn/large/006tNc79ly1g4bams9vgaj30910463yo.jpg)![1554130637300](http://ww1.sinaimg.cn/large/006tNc79ly1g4bd6fpx91j303l01ta9v.jpg)

*  电感

  * 定义式 L = φ/i

    ![1554130670516](http://ww2.sinaimg.cn/large/006tNc79ly1g4bamslqjfj303h01z3yb.jpg)![1554130677002](http://ww2.sinaimg.cn/large/006tNc79ly1g4bbn8p0q7j303f01y3yb.jpg)

  * 反电动势、能量

    ![1554130682385](http://ww3.sinaimg.cn/large/006tNc79ly1g4baar3hp5j30dr03674u.jpg)

    ![1554130689187](http://ww4.sinaimg.cn/large/006tNc79ly1g4bau755v7j30c704et91.jpg)

* 四种电路基本元件之间的关系

  ![1554130709634](http://ww1.sinaimg.cn/large/006tNc79ly1g4bd4jth08j3080082jrs.jpg) 

* 电容、电感的基本用途小结

  * 滤波（包括电容的去耦作用，电感的隔离作用）
  * 储能
  * 构成振荡器（包括谐振天线等）或者选频网络

* 二极管

  * P型半导体：空穴是多子，自由电子是少子

    ![1554130759215](http://ww4.sinaimg.cn/large/006tNc79ly1g4b9haz169j309703qaam.jpg)

  * N型半导体：自由电子是多子，空穴是少子

    ![1554130786272](http://ww3.sinaimg.cn/large/006tNc79ly1g4ba9va15wj309004474y.jpg)

  * PN结的原理

    ![1554130822093](http://ww2.sinaimg.cn/large/006tNc79ly1g4bd4jgbl4j30eb08sq57.jpg)

    ![1554130829471](http://ww2.sinaimg.cn/large/006tNc79ly1g4baaioraqj30eb051t9j.jpg)

  * 晶体二极管

    ![1554130840664](http://ww1.sinaimg.cn/large/006tNc79ly1g4ban4fppkj30do05g3ys.jpg)

  * 常用二极管 

    ![1554130859426](http://ww4.sinaimg.cn/large/006tNc79ly1g4bd5p2urxj30ek08vac2.jpg)

* 三极管

  * 三极管的工作原理：工艺上保证发射结的面积比集电结的面积小

    ![1554130888456](http://ww2.sinaimg.cn/large/006tNc79ly1g4baax5ckij30dl0810ty.jpg)

  * 晶体三极管的放大作用

    ![1554130909554](http://ww3.sinaimg.cn/large/006tNc79ly1g4bab6xzfcj30dv0843zj.jpg)

    ![1554130915567](http://ww1.sinaimg.cn/large/006tNc79ly1g4batkm6m6j30ao040mxb.jpg)

  * 特性曲线

    ![1554130926570](http://ww1.sinaimg.cn/large/006tNc79ly1g4b9ha1fzej30ek06fjrs.jpg)

  * 3种放大电路：

    * 共射电路是放大电路中应用最广泛的三极管接法，信号由三极管基极和发射极输入，从集电极和发射极输出。因为发射极为共同接地端，故命名共射极放大电路。
    * 共集电极放大电路，输入信号是由三极管的基极与发射极两端输入的（在原图里看），再在交流通路里看，输出信号由三极管的发射极两端获得。因为对交流信号而言，（即交流通路里）集电极是共同端，所以称为共集电极放大电路

    ![1554130973151](http://ww3.sinaimg.cn/large/006tNc79ly1g4ban5a2pfj30dq06x0ub.jpg)

* MOS管

  * 原理

    ![1554130987545](http://ww1.sinaimg.cn/large/006tNc79ly1g4baufjhllj30dy098ac5.jpg)

  * 图标

    ![1554131010101](http://ww4.sinaimg.cn/large/006tNc79ly1g4bcwy2ck4j30ea04uq3d.jpg)

  * 特性曲线

    ![1554131015962](http://ww1.sinaimg.cn/large/006tNc79ly1g4ba9xjyycj30de06274m.jpg)

  * 漏极电流Id的计算

    ![1554131020346](http://ww4.sinaimg.cn/large/006tNc79ly1g4bd3ulnz9j30ar066q3d.jpg)

  * 场效应管与三极管的对比

    ![1554131036422](http://ww4.sinaimg.cn/large/006tNc79ly1g4ba9rfywpj30c10590tl.jpg)

* 集成运算放大器

  * 定义

    ![1554131054843](http://ww2.sinaimg.cn/large/006tNc79ly1g4bat1v7raj30bi078q3p.jpg)

  * 运算放大器

    ![1554131060321](http://ww2.sinaimg.cn/large/006tNc79ly1g4bab2uywjj309u05fdg1.jpg)

  * 跟随器，缓冲器

    ![1554131079915](http://ww1.sinaimg.cn/large/006tNc79ly1g4bau8fgbdj308l06ejro.jpg)

  * 反相放大器 

    ![1554131083766](http://ww4.sinaimg.cn/large/006tNc79ly1g4ba9kyjghj306r057jrc.jpg)

*  

------

### 第3/4/5讲 课本内容

* Art of managing complexity

  ![1554131136736](http://ww3.sinaimg.cn/large/006tNc79ly1g4bat3d4snj306c033dfv.jpg)

* Binary Value (基带信号，波特率，调制)

* 组合逻辑和时序逻辑

  * 组合逻辑是memoryless的，输出由当前输入的值决定

  * 时序逻辑有memory，输出由当前和先前输入的值决定

   ![1554131163903](http://ww4.sinaimg.cn/large/006tNc79ly1g4bd24v0s4j30b502adfu.jpg) 

* SOP form / POS form 与或式

* 卡诺图：由真值表向与或式转变的方法

  ![1554131192486](http://ww4.sinaimg.cn/large/006tNc79ly1g4bd3vyl85j30a3052weo.jpg) 

*  

------

### 第6讲 单周期

* MIPS指令的功能分类

  ![1554288280029](http://ww3.sinaimg.cn/large/006tNc79ly1g4bd82dtesj308905vwem.jpg)

* MIPS指令的三种格式

  ![1554288301497](http://ww1.sinaimg.cn/large/006tNc79ly1g4bd2u1nirj30ag06y0t7.jpg)

* Datapath element 和 program counter

  ![1554288318075](http://ww4.sinaimg.cn/large/006tNc79ly1g4baai8s0gj30fe02c0t8.jpg)

* 双读端口的寄存器堆实现原理

  *  信号的两个读端口的寄存器号

  ![1554288336826](http://ww2.sinaimg.cn/large/006tNc79ly1g4bat9b0y7j30au0ae3yu.jpg)

* 寄存器堆写端口的实现原理

  * 信号：写使能，写寄存器号，写寄存器内容

  ![1554288357517](http://ww1.sinaimg.cn/large/006tNc79ly1g4bd6gby6lj30ch09qdg9.jpg)

* ALU中aluc的实现

  ![1554288373628](http://ww1.sinaimg.cn/large/006tNc79ly1g4bd3hzl8nj30c406rq35.jpg)

* 单周期CPU+指令寄存器+数据存储器

  ![1554288387937](http://ww3.sinaimg.cn/large/006tNc79ly1g4bbn68i3aj30cq07n755.jpg)

* MIPS的部分指令

  ![1554288401331](http://ww3.sinaimg.cn/large/006tNc79ly1g4bd3iv0iwj30ej088t9t.jpg) 

* MIPS部分指令编码

  ![1554288416454](http://ww1.sinaimg.cn/large/006tNc79ly1g4baasg19cj30ef08fabc.jpg)

*  

------

### 第7/8讲 流水线

* 流水线不会改善每一个任务的执行时间，但它能够提升整个系统任务执行的**吞吐率**。吞吐率取决于最慢的那个流水环节。 

* 指令流水线的吞吐量定义为单位时间里流出的完成指令数，其取决于指令流出流水线的速度

* 如果每一步都得到了最佳的平衡，那么每条指令在流水线上的平均时间的理想情况下等于

  ![1554288459423](http://ww4.sinaimg.cn/large/006tNc79ly1g4ba9p7hzqj307z01n3yg.jpg)

* 流水线的分段

  ![1554288483192](http://ww1.sinaimg.cn/large/006tNc79ly1g4bd6dxflyj30ae03mt91.jpg)

* 流水线寄存器的重要作用

  * 每个时钟周期结束后，该段的所有执行结果都保存在流水线寄存器中，在下一个时钟周期作为下一个段的输入；通过流水线寄存器，后段流水段可以向前级反馈数据和控制信息

  ![1554288501572](http://ww1.sinaimg.cn/large/006tNc79ly1g4bd5qf1zyj30aq02ddg1.jpg)

* 流水线的启示

  ![1554288512535](http://ww4.sinaimg.cn/large/006tNc79ly1g4b9harjq8j30aj06d3zc.jpg)

* 衡量指令速度的指标 CPI 

  *  Cycles per instruction，每条指令的平均时钟周期数；流水线可以减少指令的平均执行时间，可以认为是减少了每条指令的平均时钟周期数CPI，也可以认为是减少了时钟周期长度，还可以认为在这两方面都减少了

* 数据通路

  ![1554288537556](http://ww2.sinaimg.cn/large/006tNc79ly1g4bd540hbpj309g01z0sw.jpg)

* 在流水线中参与流水的包括：指令流（代码），数据流，控制流

* 流水线冒险

  * 结构冒险：也叫结构冲突，当硬件在指令重叠执行中不能支持指令所有可能的组合的时候，所发生的资源冒险
  * 数据冒险：在同时执行的几条指令中，一条指令依赖于前一条指令的结果数据，却得不到时发生的冒险
  * 控制冒险：流水线中的转移指令或其它改写PC的指令所造成的冒险

* 【习题1】

  ![1554288585895](http://ww3.sinaimg.cn/large/006tNc79ly1g4bd2t43hwj30a504h3z9.jpg)

  ![1554288591863](http://ww2.sinaimg.cn/large/006tNc79ly1g4bat2aisdj309o068dgd.jpg)

* 实现指令流水的两个最基本问题

  *  分段，为了重叠起来并行执行
  *  流动，能够向前同步推进执行和流水

* 结构冒险：结构冒险的问题出在指令集上

  ![1554288639829](http://ww1.sinaimg.cn/large/006tNc79ly1g4bd3hilkij30b201uweq.jpg)

  ![1554288650508](http://ww3.sinaimg.cn/large/006tNc79ly1g4baak0d8gj30ar02caae.jpg)

* 【习题2】

  ![1554288661362](http://ww3.sinaimg.cn/large/006tNc79ly1g4ba9qtbdwj30bl03fwf6.jpg)

  ![1554288667700](http://ww1.sinaimg.cn/large/006tNc79ly1g4bau68et2j30bo0493yw.jpg)

  * 数据引用会导致结构冒险，因为存储器只有一个，但是指令和数据可能都要用存储器，所有通常会把指令存储器和数据存储器分开

  ![1554288678444](http://ww4.sinaimg.cn/large/006tNc79ly1g4bat8wx3ej30d401w74l.jpg)

* 数据冒险

  ![1554288693849](http://ww1.sinaimg.cn/large/006tNc79ly1g4ba9mqjqej30au02074l.jpg)

  ![1554288697735](http://ww4.sinaimg.cn/large/006tNc79ly1g4bd1j8kfaj30au02074l.jpg)

* 数据直通技术 

  * 代码样例： DADD R1,R2,R3;  DSUB R4,R1,R5， R1发生数据冒险

    ![1554288739866](http://ww1.sinaimg.cn/large/006tNc79ly1g4bd5t9fljj30af025mxg.jpg)                                                

  * 到ALU的数据来源：EX段末尾的ALU输出（e_valA），MEM段末尾的ALU输出端（M_valA, W_valA），MEM段末尾的存储器输出端（m_valM）

    ![1554288757482](http://ww1.sinaimg.cn/large/006tNc79ly1g4ba9kjiffj30a901tdfy.jpg)  

* 数据冒险的检测方法（可以用数据通路解决的部分）

  *  需要注意的问题：由于有一些指令不写寄存器，所以可能导致一些不必要的转发；对0号寄存器要特别对待

  ![1554288827314](http://ww1.sinaimg.cn/large/006tNc79ly1g4bd8llbtwj30b605d74s.jpg)

  ![1554288831271](http://ww1.sinaimg.cn/large/006tNc79ly1g4bd23t0k8j30eu03wjrq.jpg)

  ![1554288848966](http://ww1.sinaimg.cn/large/006tNc79ly1g4bat9si09j30a804wq3b.jpg)

  *  除了要判断有regwrite，不是0号寄存器，还要保证不是上一条指令用的，不然就会转发一个过时的数据过去，这里rd是输出端口 

  ![1554288867174](http://ww1.sinaimg.cn/large/006tNc79ly1g4bd24d88gj30el04t74v.jpg)

* 不能用数据通路解决的数据冒险

  * Load/use hazard: 因为rt是访存最后的输出端口

    ![1554288897281](http://ww3.sinaimg.cn/large/006tNc79ly1g4bd2tlmr0j30b8027mx8.jpg)

  * 数字部件中会有预测分支错误吗？

* 控制冒险，几种简单的编译时调度方法

  ![1554288917632](http://ww4.sinaimg.cn/large/006tNc79ly1g4bd1jo0i7j309p02hmxd.jpg)

* 动态分支预测

  ![1554288928735](http://ww3.sinaimg.cn/large/006tNc79ly1g4bcwyxj7qj30c107cmxh.jpg)

* 由各操作组件花费时间计算出来各条指令的执行时间 

  ![1554288938164](http://ww1.sinaimg.cn/large/006tNc79ly1g4b9gxfknjj30fe03xq3m.jpg)

* 流水线CPU

  ![1554288948052](http://ww3.sinaimg.cn/large/006tNc79ly1g4b9gzq8h8j30fe09emyq.jpg)

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

  ![1554289010208](http://ww1.sinaimg.cn/large/006tNc79ly1g4bamu0dnlj309803umx9.jpg)

* Cache的工作原理是基于局部性原理（时间局部性和空间局部性）

* 【习题1】

  ![1554289041728](http://ww2.sinaimg.cn/large/006tNc79ly1g4bau7jp9yj30a901lmx4.jpg)

  解答过程如下：

  ![1554289056403](http://ww2.sinaimg.cn/large/006tNc79ly1g4baaj2srlj30at05lgm7.jpg)

  ![1554289061802](http://ww3.sinaimg.cn/large/006tNc79ly1g4bd6vmovxj30am03taaa.jpg)

  ![1554289066962](http://ww1.sinaimg.cn/large/006tNc79ly1g4baaop7vhj30at04tt95.jpg)

  ![1554289070665](http://ww1.sinaimg.cn/large/006tNc79ly1g4ba9wpn5vj30am04zmxi.jpg)

* 存储器层次结构的四个问题

  *  块的位置：一个从主存来的块，可以被放置在cache的哪里？
  *  块的标记：如何找到放在cache中的块？
  *  块的替换：如果块发生缺失，cache中哪个块应该被替换出去？
  *  写时策略：CPU执行写操作时，该怎么处理

* 块的位置

  ![1554289132048](http://ww3.sinaimg.cn/large/006tNc79ly1g4baaxkk9bj30a5044gm9.jpg)

  *  直接映射需要建立一个将主存中的每一个块对应到cache中的唯一位置的一个映射方法，通常是用“块地址 mod cache的块数”，方法简单，但是容易冲突
  *  全相联映射是哪里空就可以放哪里，按照某种算法来映射，这不容易冲突，但是映射方法和很复杂
  *  组相联：一个块首先被映射到一个组中，然后它可以被 放置到组中的任何一个块中；如果一个组中有n块，那么这种映射方法就称为n路组相联

  ![1554289169778](http://ww4.sinaimg.cn/large/006tNc79ly1g4bd6ee2ozj30dg09at9w.jpg)

* 块的标记

  *  Cache中的每一个块结构都有一个地址标记给出该块的贮存块地址信息
  *  需要在标志中加入一个有效位来标明该块是否有效

  ![1554289192137](http://ww2.sinaimg.cn/large/006tNc79ly1g4bcvrbdlmj30dk0a4mxv.jpg)

  *  这是一个两路组相连，一共512组的cache，一共1024个块，每个块大小64字节 

  ![1554289209756](http://ww2.sinaimg.cn/large/006tNc79ly1g4bd844hdlj309k042gm4.jpg)

  *  这是一个2路组相连，一共4组，总共能放8个块的cache，而主存大小是32个块

  ![1554289243932](http://ww1.sinaimg.cn/large/006tNc79ly1g4bab3afn2j30a3071gmt.jpg)

  ![1554289247746](http://ww2.sinaimg.cn/large/006tNc79ly1g4b9gzdbb9j30dj01x0so.jpg)

* 替换策略

  *  因为直接映射的话要是在cache中肯定是在固定位置的，所以不用考虑，如果这个位置不是想要的东西，就替换掉

  ![1554289263370](http://ww1.sinaimg.cn/large/006tNc79ly1g4ba9xzdp8j30a203it9a.jpg)

  ![1554289267602](http://ww4.sinaimg.cn/large/006tNc79ly1g4b9h77wgcj30ah068758.jpg)

  *  对于大容量cache来说，LRU和随机替换算法几乎没有什么差别
  *  对于小容量cache，LRU替换算法最优，FIFO也比随机算法稍微好一点

* 写回策略

  *  Amdahl定律：高性能的设计不能忽视写操作速度对系统性能的影响

  ![1554289299929](http://ww4.sinaimg.cn/large/006tNc79ly1g4baamuoquj30aq05zwfi.jpg)

  ![1554289315299](http://ww2.sinaimg.cn/large/006tNc79ly1g4bbn5revqj309l04r750.jpg)

  ![1554289318731](http://ww3.sinaimg.cn/large/006tNc79ly1g4baa36qt1j30ap05k754.jpg) 

  ![1554289323286](http://ww1.sinaimg.cn/large/006tNc79ly1g4ban4tvzvj30am064jsk.jpg)

* cache性能评价

  *  对存储器层级结构较合理的评价方法是采用平均存储器访问时间  

  ![1554289349592](http://ww1.sinaimg.cn/large/006tNc79ly1g4bbn5aphlj30av00r0sn.jpg)

  *  【习题】

  ![1554289361262](http://ww4.sinaimg.cn/large/006tNc79ly1g4bcwglffvj30av067myf.jpg)

  ![1554289365806](http://ww3.sinaimg.cn/large/006tNc79ly1g4bd1kcym0j30cz05m3yy.jpg)

  ![1554289370517](http://ww3.sinaimg.cn/large/006tNc79ly1g4babb60lyj30c206rq3r.jpg) 

  ![1554289375057](http://ww3.sinaimg.cn/large/006tNc79ly1g4bana352fj30bp06f74v.jpg) 

  ![1554289391013](http://ww4.sinaimg.cn/large/006tNc79ly1g4b9gv2padj30c707zwfi.jpg)

* Cache性能优化

  *  Cache性能优化的方向有减少缺失次数/提高命中率，也可以是降低缺失代价，比如使用多级cache 

  ![1554289405000](http://ww4.sinaimg.cn/large/006tNc79ly1g4bd5rweoej30bm058mxw.jpg)

  ![1554289409346](http://ww4.sinaimg.cn/large/006tNc79ly1g4bautz8bdj30c106paam.jpg)

* 核心公式

  ![1554289433968](http://ww4.sinaimg.cn/large/006tNc79ly1g4baazfs2sj30fe06gwf6.jpg)

  - 这个代表1000条指令有多少次缺失

  ![1554289447258](http://ww4.sinaimg.cn/large/006tNc79ly1g4ba9j5vozj30d400zmx4.jpg)

  ![1554289450695](http://ww3.sinaimg.cn/large/006tNc79ly1g4bamtki2oj30dr00w749.jpg)

  ![1554289457502](http://ww2.sinaimg.cn/large/006tNc79ly1g4bd53kar8j309g01ejra.jpg) 

  *  缺失率 = 1000条指令有几次data缺失/1000条指令有几条data指令，单位：次/条

  ![1554289467032](http://ww1.sinaimg.cn/large/006tNc79ly1g4ba9qzybzj30b5021mxc.jpg)

  *  多级cache中

  ![1554289479026](http://ww3.sinaimg.cn/large/006tNc79ly1g4bd4kaoogj30b9010glj.jpg)

  ![1554289482727](http://ww1.sinaimg.cn/large/006tNc79ly1g4bd4kw5laj30dr020dfw.jpg)

  ![1554289495915](http://ww1.sinaimg.cn/large/006tNc79ly1g4bd3uzsjmj308802udfy.jpg)

  ![1554289501214](http://ww3.sinaimg.cn/large/006tNc79ly1g4bat2s2qaj30d9089js8.jpg)

  ![1554289505288](http://ww3.sinaimg.cn/large/006tNc79ly1g4bab9a03tj30dw086401.jpg)

  ![1554289510424](http://ww4.sinaimg.cn/large/006tNc79ly1g4baa4mrmcj30fe06bt9q.jpg)

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

  ![1554289628610](http://ww1.sinaimg.cn/large/006tNc79ly1g4bd2uz2i2j30bl06t74l.jpg)

  ![1554289632757](http://ww3.sinaimg.cn/large/006tNc79ly1g4bd6faqf6j30b907pjrt.jpg)

* 虚拟存储器

  *  一个磁盘上的块可以放在内存中的什么位置：全相连
  *  如何在内存中查找一个块：页表
  *  当发生虚拟存储器缺失时，应该替换哪个块：LRU
  *  写操作时会发生什么：写回法

* 虚拟存储器

  ![1554289667979](http://ww4.sinaimg.cn/large/006tNc79ly1g4bd5sry6gj30dl08dgm1.jpg)

  ![1554289672593](http://ww3.sinaimg.cn/large/006tNc79ly1g4bd1kl84qj30ag053jrv.jpg)

  ![1554289677764](http://ww4.sinaimg.cn/large/006tNc79ly1g4baaswukuj30fe0ci75h.jpg)

* 





 

