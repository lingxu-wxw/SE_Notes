#### 计算机体系结构 Quiz 1

------

##### 单选题

* 1. Choose one that is not related to the physical design of processors.

  * A. Wafer	B. Die	C. Polysilicon	D. Ingot	E. PDU

* 2. Select the one that may not solve the scale-out problem in a power-limited datacenter.

  * A. Use low-power CPU chip	B. Improve Instr Level parallelism
  * C. Improve server energy efficiency 	D. Scale up power deliver system
  * E. Depoly modular data center (container)

* 3. Which of the following is not a solution for resolving data hazard ?

  * A. Bypassing 	B. Interlock 	C. Pipeline Stall 
  * D. Forwarding     E. Speculation

* 4. Which one of the following concepts is not micro-architecture-level ILP design ?

  * A. Superpipeline 	B. EPIC 	C. Branch prediction
  * D. Multiple issue     E. Dynamic scheduling

* 5. For a dual-channel, DDR2 memory with 200 MHz memory bus, its peak speed is:

  * A. 6.4 GB/s 	B. 3.2 GB/s 	C. 1.6 GB/s 	D. 400 MB/s 	E. 200 MB/s

------

##### 多选题

* 1. As we follow the Moore's Law, we can actually:

  * A. Improve CPU energy efficiency 	
  * B. Increase transistor density on the chip
  * C. Increase CPU frequency 	
  * D. Lower the cost of wafer
  * E. Improve chip yield rate

* 2. Consider a k-issue OOO, select the wrong statements:

  * A. It has k FUs. 	
  * B. It requires k instr/cycle to maximize utilization.
  * C. It is basically a k-stage superpipeline. 	
  * D. It supports VLIW.
  * E. Its IPC can be large than 1.

* 3. In terms of CISC, RISC and VLIW, select all the wrong statements:

  * A. VLIW uses reduced instruction set.
  * B. No direct memory operation in CISC
  * C. RISC-V does not use condition codes.
  * D. VLIW needs fewer physical GPR.
  * E. CISC use fixed-length instr.

* 4. Select all the correct statements about Victim Cache:

  * A. A piece of fully associative memory
  * B. Has better performance than the Miss Cache.
  * C. Favors temporal locality.
  * D. Decrease cold misses.
  * E. None of the above.

* 5. Consider a x8 DIMM DRAM system, select all the statements that are not correct

  * A. Ranks are selected by the MC.
  * B. Banks can be accessed simultaneously.
  * C. A DRAM page has 8 bits.
  * D. 16 DRAM devices.
  * E. Double data rate.

------

##### 判断题

* 1. The energy and power cost are typically part the CapEx.
* 2. If the pipeline has many independent operations, we can actually unify instruction types.
* 3. Adding function units in a processor can be seen as a type of scale-out design.
* 4. Instructions that performs operation on GPR are generally "User ISA".
* 5. The data stored in the ROB are processor states that are visible to programmers
* 6. Statically scheduled processor uses in-order-execution
* 7. In Tomasulo's Algorithm, the renaming mechanism is provided by the RS.
* 8. Precise exception requires in-order-execution.
* 9. The size of ROB and RS often affects the parallelism of the processor.
* 10. Good locality often indicated predictable data/instruction behaviors.
* 11. We need to dynamically check the write buffer to get updated data from the backing store.
* 12. The  1T1C DRAM cell needs to be pre-charged before read.

* 13. Row buffer conflict can lead to significant latency issue.
* 14. Only a specific row of data is locked and inaccessible during refresh cycle.
* 15. No hazards due to output dependences (WAW) can occur in a typical pipeline.

------

##### 简答题

* 1. Name at least two challenges of designing a 10-nm class processor chip.
* 2. Why adding too many pipeline stages could reduce processor throughput ?

* 3. What are the differences between Tomasulo's algorithm and Scoreboarding ?
* 4. Why dynamically managing the sense amplifier can reduce DRAM energy ?
* 5. What is the memory wall ? What is the difference between the memory wall and the memory bandwidth wall ?









