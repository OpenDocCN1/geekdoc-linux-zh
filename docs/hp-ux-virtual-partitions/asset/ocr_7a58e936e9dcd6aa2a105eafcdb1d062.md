# Steps to Create Virtual Partitions

Boot Cpts:  
[CPU Details]  
Min/Max: 1/3  
Bound by User [Path]:  
Bound by Monitor [Path]: 37 <!-- one CPU in use at 37 -->  
Unbound [Path]:  
[IO Details]  
0.8.0.0.8.0.5.0.0.0 BOOT  
3.0.0.0.0  
[Memory Details]  
Specified [Base /Range]:  
(bytes) (MB)  
Total Memory (MB): 1024  
#

![](bbox=[0.87, 0.34, 0.94, 0.45])

The output of these two **vparstatus** commands shows that `cable1` has one *bound* CPU and `cable2` has one *bound* CPU. On the L-Class system on which these vPars were created there are a total of four CPUs. This means that two CPUs should be available. Let’s run **vparstatus -A** to view the available components on a system:

```
# vparstatus -A
[Unbound CPUs (path)]: 97 101
[Available CPUs]: 2

[Available I/O devices (path)]: 0.1 0.2 0.3 0.4 0.5 0.9 0.12 32 36 96 100
[Unbound memory (Base /Range)]: 0x0/64 0xC000000/1856 (bytes) (MB)
[Available memory (MB)]: 2048
#
```