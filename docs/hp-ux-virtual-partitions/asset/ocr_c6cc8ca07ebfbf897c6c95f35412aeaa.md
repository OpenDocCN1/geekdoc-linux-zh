![](bbox=[0.06, 0.06, 0.21, 0.21])

Although this is a simple example showing how a Virtual Partition can be modified, it also demonstrates the power of vPars. While both vPars on the system are running, a processor can be added to one or both without interruption of the programs running in the vPars.

Note that the `-a option to **vparmodify** changed the number of CPUs *relative* to the current number. In our case the current number of CPUs was one and using `-a cpu:1` added one CPU to the current number of one resulting in two CPUs. This is true also when we use the `-d option to **vparmodify** to remove processors. The following example shows running **vparstatus** to see (this two CPUs, using **vparmodify** to change the number of CPUs back to one (this is also relative to the current number of CPUs, which is two), and a **vparstatus** to confirm that this change has taken place:

```
# vparstatus -p cabiel -v
# vparstatus -p cabiel -v

[Virtual Partition Details]
Name:                  cabiel
State:                 Up
Attributes:            Dynamic,Manual
Kernel Path:           /stand/vmunix
Boot Opts:

[CPU Details]
Min/Max:               1/3
Bound by User [Path]:  33      <-- bound CPU @ 33
Bound by Monitor [Path]:
Unbound [Path]:        97      <-- unbound CPU @ 97

[IO Details]
  0-0
  0.0.0.0
  0.0.1.1.2.0 BOOT
  0.0.4.0  CONSOLE

[Memory Details]
Specified [Base /Range]:
             (bytes) (MB)
Total Memory (MB):  1024
# vparmodify -p cabiel -d cpu:1
# vparstatus -p cabiel -v

[Virtual Partition Details]
Name:                  cabiel
State:                 Up
Attributes:            Dynamic,Manual
Kernel Path:           /stand/vmunix
Boot Opts:

[CPU Details]
Min/Max:               1/3
```

![](bbox=[0.06, 0.22, 0.21, 0.37])