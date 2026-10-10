This output shows many components available for our second parti-tion. Based on our earlier planning exercise, we know the components that we wish to include in the second vPar and this `vparstatus -A` command con-firms that they are indeed available.

For *cable2* we want one CPU initially, and there are three available. We want the I/O cards for boot and LAN at *0/8* and *0/10* respectively We want one GBByte of memory and there are now roughly three GBBytes available. We have all of the components we need to proceed to our next step of creat-ing *cable2*.

# 8) Create the Second Virtual Partition

![](bbox=[0.05, 0.44, 0.15, 0.55])

We earlier listed all of the components of which our second partition is to be comprised and confirmed that these components are still available with the `vparstatus -A` command. HP-UX 11i has already been loaded on a second disk on the same system used to create our first Virtual Partition *cable1*. We can create our second Virtual Partition, which we’ll call *cable2*. We’ll create the second while the first is running and boot the second vPar from the first.

Here are the components we earlier listed for our second vPar:

```
```
name
processors   cable2
              min of one (bound) max of three (two unbound)
              with num (bound + unbound) equal to one
memory       1024 MB
LAN          0/10
LBA          0/8
boot disk    0/8/0/0.8.0.5.0.0.0
kernel       /stand/vmunix (this is the default)
auto       off (manual)
console      virtual console to be created
```
```

There are several differences between the list of components for the two vPars. We have devoted a different LAN card and boot disk. We have specified the CPUs in the same manner in both vPars with *min* (this will be *bound*) of one and *max* of three. *num* of one, and let the vPars software