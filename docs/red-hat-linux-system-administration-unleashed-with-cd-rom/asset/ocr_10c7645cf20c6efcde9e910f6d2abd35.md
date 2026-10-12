```
(time stamp counter) register.
'Pentium' for the Intel Pentium/Pentium MMX, AMD K5, K6 and K6-3D.
'PPro' for the Cyrix/IBM/National Semiconductor 6x86MX, MII and Intel Pentium II/Pentium Pro.
```

Memory type range register (MTRR) support may optionally be included on Pentium II and Pentium Pro systems. These registers are typically used to control processor access to memory ranges. Saying yes to this option enables write-combining, allowing bus write transfers to be combined into larger transfers before bursting over the PCI/AGP bus. This can increase performance of the video image writes substantially. You should set this option if you have a Pentium Pro or faster system, especially if you also enable SMP support, since setting this options also fixes a problem with some SMP BIOSes.

Another processor feature that you may now set through the configurator is support for multiple CPUs or SMP. With the 2.2 kernel, Linux is capable of supporting up to 16 processors on Intel systems. This limitation may soon change, however, and by the time you read this, support for up to 64 processors may be available.

The SMP support in the 2.2 kernels is not considered experimental and is the result of a significant development effort that began with the 1.3 development branch of the kernel. This support continues to improve with each kernel revision and now that the Intel SMP support has reached this level of stability, the other architectures supported by Linux are adding support for SMP systems as well. The maturest support among the other architectures is for the Sparc and Sparc64 architectures.

> **Tip**
> 
> If you enable SMP support, you will also need to enable the Enhanced Real Time Clock Support option. This is required so that the Real Time Clock in your system is read and set in an SMP safe manner. Please also note that by specifying support for SMP, you disable support for Advanced Power Management features.

Although kernels compiled with SMP support may run on a single processor system, it will usually be at the cost of performance. It is therefore best to not run SMP kernels on single processor systems. Also note that enabling SMP support in your kernel may require that you change your BIOS settings. It is highly recommended that you read and follow the advice given in the SMP FAQ, which can be found on your Red Hat system in /usr/doc/FAQ/txt/SMP-FAQ.