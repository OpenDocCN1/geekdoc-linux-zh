# 5.3.6 Address Space Management

The Solaris kernel is implemented with a central address management subsystem that other parts of the kernel call into. The address space module is a wrapper around the segment drivers, so that subsystems need not know what segment driver is used for a memory range. The address space object shown in Figure 5.7 is linked from the process's address space and contains pointers to the segment space.

![](bbox=[0.125, 0.26, 0.933, 0.725])

Figure 5.7 The Address Space

The address space subsystem manages the following functions:

+   - Duplication of address spaces, for fork ()
- Destruction of address spaces, for exit )
- Creation of new segments within an address space
- Removal of segments from an address space
- Setting and management of page protection for an address space
- Page fault routing for an address space
- Page locking and advice for an address space
- Management of watchpoints for an address space