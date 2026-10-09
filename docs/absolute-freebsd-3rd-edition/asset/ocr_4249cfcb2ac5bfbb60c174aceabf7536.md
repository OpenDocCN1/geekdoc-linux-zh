the system. The boot messages dance between showing too much detail and obscuring details that might be critical. For example, it’ll also show all the information it can about the CPU in the system:

```
CPU: Intel(R) Xeon(R) CPU E5-1620 v2 @ 3.70GHz (3700-0M-8H K8-class CPU
      Origin=\"GenuineIntel\"  Id=0x306e4  Family=0x6  Model=0x3e  Stepping=4
❱
      Features=0xbfbebfbf<FPU,VME,DE,PSE,TSC,MSR,PAE,MCE,CX8,APIC,SEP,MTRR,PGE,MCA,
      CMOV,PAT,PSE36,CLFLUSH,DTS,ACPI,MMX,FXSR,SSE,SSE2,SS,HTT,tm,PBE>
      Features2=0x7fbbe3ff<SSE3, PCLMULQDQ,DTES64,MON,DS_CPL,VMX,SMX,EST,TM2,SSSE3,CX16,
      xTPR,PDCM,PCID,DCA,SSE4.1,SSE4.2,x2APIC,POPCNT,TSCDLT, AESNI, XSAVE, OSXSAVE, AVX, F16C, RDRAND>
      AMD Features=0x2c100800<SYSCALL,NX,Page1GB,RDTSCP,LZ>
      AMD Features2=0x1c<LAHF>
      Structured Extended Features=0x281<fSGSBASE,SMEP,ERMS>
      XSAVE Features=0x1<XSAVEOPT>
      VT-x: PAT,HLT,MTF,PAUSE,EPT,UG,VPID,VLD,PostIntr
      TSC: P-state invariant, performance statistics
```

You probably didn’t know that a simple CPU could have so many details and features, did you? But when you file a trouble report that advanced features don’t work, a developer might respond by asking whether your CPU has a particular feature.

Here’s why I’m not worried about the performance hit caused by the WITNESS option shown earlier: this box is pretty darn fast 1 and supports a whole bunch of features important to modern CPUs 2. While I certainly want all the performance I paid for, I also want to catch any problems when they happen. I want to be able to file good bug reports on those problems, so the developers will listen to my problem report. That’s why I’m running a development version of FreeBSD that ships with WITNESS enabled, after all!

```
FreeBSD/SMP: Multiprocessor System Detected: 8 CPUs
```

Here, the kernel announces that it’s found all eight CPU cores and is ready to manage them. I have CPU power to spare and a fair amount of memory as well.

+   1. real memory = 34359738368 (32768 MB)
+   2. avail memory = 33207656448 (31669 MB)