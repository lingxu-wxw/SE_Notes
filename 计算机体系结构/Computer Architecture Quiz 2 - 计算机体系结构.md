#### 计算机体系结构 Quiz 2

------

##### 单选题

* Which one of the following concepts discussed in our lectures is not time-saving driven?

  * A. write propagation	B. multi-lane	C. workload reduction

  * D. queueing analysis 	E. DSM

* Chose one that is not a source of multicore resource contention

  * A. LLC		B. power budget 	C. memory controller	D. TLB	E. bus

* Select one that is not hardware-based technique

  * A. SMT		B. MSI		C. vector chaining	D. strip mining	E. speculation

* The concept of SIMT is related to:

  * A. NUMA	B. CUDA	C. Hyper-threading	D. MESI	E. Vector

* Compared with SATA, what are the advantages of SCSI？

  * A. Highly reliable	B. Shorter cable length 	C. Cheap

  * D. Low power		E. Not suitable for server system

##### 判断题

* Analytic modeling allows one to quickly estimate system running states
* A CMP is asymmetric if its cores have unequal access time to local memory
* Without appropriate design, direct memory access may read stale value
* Reads to a location are sometimes not serialized in a cache-coherent system
* A shared-cache system does not have cache coherency problem
* CUDA thread blocks are mapped to different streaming multiprocessors
* Snoopy protocol maintains register coherence using processor-side controller
* Only the cache picks up the block then the MSI write-back protocol flushes its data
* For a single-issue processor, fine-grained multithreading and SMT are equivalent
* Typically, multicores do not focus on throughput computing
* MVL is determined by the architecture of the processor
* CMPs can be designed to support different ISAs on the same chip
* Multicore solution is not suitable for embedded systems
* Vector instructions can be processed by a single deeply pipelined FUs
* The active threads in a warp always take the same execution path
* Execution-driven simulation is well suited for multicomputer systems
* Write-through cache is unpopular for SMPs
* Dynamic warp formation can lead to out of order warp execution
* A bus only supports a single transaction at a time
* Massage passing is the major way for communication on a DSM system

##### 问答题

##### Performance Analysis

Consider a processor that has an idle power demand of 60W. It has been measured that the CPU consumes  about 100W power when running a CPU-intensive benchmark at 1.0GHz

* Assume an average utilization rate of 60% under a memory-intensive workload, what is the estimated average power demand of the CPU running at the same frequency? (1.0GHz)
* Consider another case, if the given power budget (maximum allowable power) is 185W, can we run the same CPU-intensive benchmark under 2.0GHz? Why?

##### Thread-Level Parallelism

* For a simple write-through invalidation-based no-allocate cache, what would happen if a processor read operation incurs a miss?
* Why MSI is believed to be more efficient than the above simple write through protocol?

##### Data-Level Parallelism

* Describe how vector processor improves memory access efficiency
* How do you compare SIMD and SIMT
