# Steps to Create Virtual Partitions

identify the one *bound* processor. These two Virtual Partitions will use different I/O paths for their devices. Let’s now run the **vpcreate** command to create **cable2**:

We can now proceed to create the second partition with the command shown in the following file:

```
# cat /tmp/cable2
vpcreate -p cable2 -B manual -b /stand/vmunix -a cpu::1
-a cpu::1:1:3 -a mem::1024 -a io:0/8
-a io:0/8/0/0.8.0.5.0.0.0:boot -a io:0/10
#
```

After executing this file we can determine if the second vPar has been created and the components of which it is comprised by running **vpstatus**:

```
# vpstatus -v

[VirtuaI Partition Details]
Name:    cable1
State:   Up
Attributes: Dynamic, Manual
Kernel Path: /stand/vmunix
Boot Opts:

[CPU Details]
Min/Max: 1/3
Bound by User [Path]:
Bound by Monitor [Path]: 33
Unbound [Path]:

[IO Details]
 0.0
  0.0.1.1.2.0 BOOT

[Memory Details]
Specified [Base /Range]:
           (bytes) (MB)
Total Memory (MB): 1024

[VirtuaI Partition Details]
Name:    cable2
State:   Down
Attributes: Dynamic, Manual
Kernel Path: /stand/vmunix
Boot Opts:
```