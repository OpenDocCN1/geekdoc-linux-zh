# The Linux Symmetrical Multiprocessing (SMP) Model

# Types of Multiprocessing

A multiprocessoring system consists of a number of processors communicating via a bus or a network. There are two types of multiprocessoring systems: loosely coupled and tightly coupled.

Loosely coupled systems consist of processors that operate stand-alone. Each processor has its own bus, memory, and I/O subsystem, and communicates with other processors through the network medium. Loosely coupled systems can be either homogeneous or heterogeneous.

Tightly coupled systems consist of processors that share the memory, bus, devices, and sometimes cache. Tightly coupled systems run a single instance of the operating system. Tightly coupled systems can be classified into symmetric and asymmetric systems. Asymmetric systems are configured so that each processor is assigned a specific task. Asymmetric systems have a single "master" processor that controls all others. Symmetric systems treat all processors the sameway processes have equal access to all system resources. In the symmetric model, all tasks are spread equally across all processors.

Symmetric systems are subdivided into further classes consisting of dedicated and shared cache systems. Symmetrical Multiprocessing (SMP) systems have become very popular and have become the default choice for many large servers.

# Concurrency and Data Serialization

In an ideal world, an SMP system with $n$ processors would perform $n$ times better than a uniprocessor system. In reality, this is not the case. The main reason that no SMP system is 100% scalable is because of the overhead involved in maintaining additional processors.

# Locks, Lock Granularity, and Locking Overhead

Locks basically protect multiple threads from accessing or modifying a piece of critical information at the same time. Locks are especially used on SMP systems where multiple processors execute multiple threads at the same time. The problem with locking is that if two or more processors are competing for the same lock at the same time, only one is granted the lock, and the other waits, spinning, for the lock to be released. In other words, the other processors are not really doing any useful work. Locking, therefore, must be limited to the smallest amount of time possible.

Another common technique used to address this problem is to employ finer-grain locking. With finer-grain locking, instead of using a single lock to protect 100 things,