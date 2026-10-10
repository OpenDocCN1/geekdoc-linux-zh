![](bbox=[0.08, 0.17, 0.13, 0.26])

Since the concept of isolation is very important in the world of Virtual Partitions we would expect to see only the information related to `vPar 1` when working in SAM on this `vPar`. The same is true of `vPar 2`, that is, we'd expect to see only information related to `vPar 2` when working in SAM on this `vPar`.

Let's start by running `vparstatus` to see which components are associated with `vPar 1` and which components are associated with `vPar 2`, as shown in the following listing:

```
```
root@appd1[/root] > vparstatus -v
    [Virtual Partition Details]
    Name: actrappd1    <-- beginning of vPar 1 information
    State: Up
    Attributes: Dynamic,Manual
    Kernel Path: /stand/vmunix
    Boot Opts:
    [CPU Details]
    Min/Max: 2/2
    Bound [Path]: 33
                   37
    Unbound [Path]:
    [IO Details]
    0.0.1.1.2.0 BOOT
    0.0.4.0 CONSOLE
    0.0
    0.0.2.0.2.0 ALTBOOT
    [Memory Details]
    Specified [Base /Range]:
    (bytes) (MB)
    Total Memory (MB): 2048
    [Virtual Partition Details]
    Name: ecvpard2     <-- beginning of vPar 2 information
    State: Up
    Attributes: Dynamic,AutoBoot
    Kernel Path: /stand/vmunix
    Boot Opts:
    [CPU Details]
    Min/Max: 2/2
    Bound [Path]: 97
                   101
    Unbound [Path]:
    [IO Details]
    0.12.0.0.1.0, BOOT
    0.8
```
```