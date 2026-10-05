to a top-level vCenter Server object. Because statistics are kept in the vCenter Server database and not lost during a vMotion, you have the benefit of greater tracking and analysis.

> **NOTE** Prior to PowerCLI version 5.1 Release 2 there was no official support for managing-distributed switches. The first edition of this book demonstrated how to manage them via a custom PowerCLI module put together by the authors. This was followed by a VMware-released, which took us closer to a supported solution, and finally in PowerCLI 5.1 R2, official support was added via a VDS snap-in as part of the PowerCLI installation. The custom PowerCLI module for the first edition of this book contains some functionality not available in the official version, of which is referred to later in this chapter, and is still available for download from

```
http://powerclibook.com/wp-content/uploads/2013/07/PowerCLIBook.zip
```

If you're accustomed to using a vSphere standard switch, the VDS can take a little getting to. The biggest challenge is disassociating in your mind the network from the vSphere host. Previously, you had to work on a single host at a time. This process could be automated with PowerCLI, but still, the level and potential for mistakes makes the VSS less optimal. Let's take a look at the two processes.

To configure a network using a VSS, follow these steps:

+   1. Create a VSS.
2. Add uplinks to the VSS.
3. Create the port groups.
4. Create the VMkernel ports.

With the new model using the VDS, the configuration now requires the following steps:

+   1. Create a VDS.
2. Configure the VDS uplink ports.
3. Create the VDS port groups.
4. Create the VMkernel ports.
5. Add the vSphere hosts to the VDS binding your physical NIC (pNIC) to a VDS uplink port.