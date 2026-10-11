# Introduction

This chapter focuses on tools that initially help monitor the overall performance of the system. After the overall system performance characteristics of a workload are understood, the same tools can be useful in identifying which particular processes are bottlenecks to the overall workload. In many cases, the system monitoring tools can help drive system tuning such that the key bottlenecks can be substantially reduced or eliminated. In other cases, these tools simply pinpoint applications or processes that need tuning, reconfiguration, or, in the most extreme case, algorithmic changes to improve overall workload performance and throughput.

In particular, this chapter examines tools that provide insights into the following:

+   - Overall system CPU utilization

+   - Memory utilization

+   - Disk I/O utilization and latency

+   - Network utilization

Several of the tools provide information about different aspects of system utilization; however, to simplify the organization of this chapter, tools are discussed in the section that is most appropriate to the majority of their monitoring capabilities. These tools are often the first, and sometimes the only, means used for understanding and improving the performance of a given workload. However, there are cases where these high-level tools point to a single application or set of tasks that are a bottleneck that cannot be resolved by global system tuning. In those cases, future chapters discuss tools that allow a performance analyst to zoom in on a problem application to better understand the operation of the application and its interaction with the underlying operating system.