# Benchmark Environment and Workload Profiles

All of the benchmarks used to gathar results for this chapter were run in a Linux 2.6.4 environment. For this study, the CFI/O scheduler was backported from Linux 2.6.5 to 2.6.4. The benchmarks were run on the following systems:

+   - 16-way 1.7GHz Power4+ IBM p690 SMP system configured with GB memory. 28 15,000-RPM SCSI disk drives configured in a single RAID-0 setup that uses Emulex LP9802-2G Fiber controllers (one in use for the actual testing). The system is configured with the Linux 2.6.4 operating system.

+   - 8-way NUMA system. IBM x440 with Pentium IV Xeon 2.0GHz processors and 512KB L2 cache subsystem. Configured with four qla2300 fiber cards (only one is used in this study). The I/O subsystem consists of two FAST700 I/O controllers and utilized 15,000-RPM SCSI 18GB disk drives. The system is configured with GB of memory, set up as a RAID-5 (five disk) configuration, and uses the Linux 2.6.4 operating system.

+   - Single CPU system. IBM x440 (8-way; only one CPU is used in this study) with Pentium IV Xeon 1.5GHz processor, and a 512k L2 cache subsystem. The system is configured with an Adaptec aic7899 Ultra160 SCSI adapter and a single 10,000-RPM 18GB disk. The system uses the Linux 2.6.4 operating system and is configured with 1GB of memory.

The benchmarks we used for this study are the following:

+   - ***Web Server Benchmark***. This benchmark utilizes four worker threads per available CPU. In the first phase, the benchmark creates several hundred thousand files ranging from 4KB to 64KB. The files are distributed across 100 directories. The goal of the create phase is to exceed the size of the memory subsystem by creating more files than what can be cached by the system in RAM. Each worker thread executes 1,000 random read operations on randomly chosen files. The workload distribution in this benchmark is derived from Intel's Iometer benchmark.

+   - ***File Server Benchmark***. This benchmark utilizes four worker threads per available CPU. In the first phase, the benchmark creates several hundred thousand files ranging from 4KB to 64KB. The files are distributed across 100 directories. The goal of the create phase is to exceed the size of the memory subsystem by creating more files than what can be cached by the system in RAM. Each worker thread executes 1,000 random read or write operations on randomly chosen files. The ratio of read to write operations on a per-thread basis is specified as 80% to 20%, respectively. The workload distribution in this benchmark is derived from Intel's Iometer benchmark.