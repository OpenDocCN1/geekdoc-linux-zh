# 2.1.2 How virtualization works

Virtualization deals with enabling basic systems management of multiple, often heterogeneous systems directly out of the box.

As Figure 2-1 shows, partitioning and virtualization involve a shift in thinking from physical to logical by treating IT resources as logical pools rather than as separate physical entities. This involves consolidating and pooling IT resources, and providing a single system illusion for both homogeneous and heterogeneous servers, storage, distributed systems, and networks.

![](bbox=[0.05, 0.25, 0.95, 0.65])

Partitioning of hardware involves separate processors for separate operating systems, each of which runs its specific applications. Software partitioning employs a software-based hypervisor to enable individual operating systems to run on any or all of the processors.

> ¹ z/VM does not run Windows® as a guest operating system because Windows is not a mainframe operating system. Figure 2-1 shows the operating systems that run on z/VM or VMware; it does not show the operating systems that run on both.