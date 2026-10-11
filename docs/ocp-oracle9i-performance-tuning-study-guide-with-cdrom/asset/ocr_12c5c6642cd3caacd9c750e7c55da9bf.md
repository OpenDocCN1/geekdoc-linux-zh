TABLE 10.4 Common Server Architectures

| Architecture | Description |
| :--- | :--- |
| Uniprocessor | Servers with a single CPU and memory area. I/O, bus, and disk resources are used exclusively by this server. |
| Symmetric Multiprocessor (SMP) | Servers with two or more CPUs, but one memory area. I/O, bus, and disk resources are used exclusively by this server. |
| Massively Parallel Processor (MPP) | Two or more servers connected together. Each server has its own CPU, memory area, I/O bus, disk drives, and a copy of the OS. |
| Non-Uniform Memory Access (NUMA) | Two or more SMP systems connected together. Each server has its own CPU, but the memory areas for each server is shared as one large memory area across all servers. A single copy of the OS is run across all servers. |

Oracle is also a very CPU-aware product. If new CPUs are added to a database server, Oracle will dynamically change the default settings for several CPU-related parameters. Examples of some of these parameters are shown in Table 10.5.

TABLE 10.5 CPU-related init.ora Parameters

| Parameter | Description |
| :--- | :--- |
| CPU_COUNT | Specifies the number of CPUs in the server. |
| PARALLEL_THREADS_ PER_CPU | Used to establish the default degree of parallelism when using Oracle’s parallel execution features. |
| FAST_START_ PARALLEL_ROLLBACK | The number of parallel rollback processes is derived from this value (HIGH, LOW, FALSE) and the number of CPUs. |