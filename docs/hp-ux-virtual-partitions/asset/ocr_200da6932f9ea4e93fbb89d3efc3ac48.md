these resources, loads kernels, and performs other functions that make it look as though each virtual partition is its own system.

Rather than booting a kernel directly from the ISL (see the non-vPars-specific portion of this chapter for detailed information on all aspects of booting including ISL), you boot the **vpmon**. The **vpmon** then loads the partition database /stand/vpdb and creates the vPars based on the resources allocated to the vPars in the database. **vpdb** is the default database which contains partition-related information. A copy of **vpdb** is kept on the disk for every partition and is automatically kept synchronized. When a change is made to any partition, the master **vpdb** is updated and then the local copies on other vPars are automatically updated. This synchronization occurs every few seconds and ensures that **vpdb** on all running partitions remains synchronized. If a partition is not running its **vpdb** cannot be updated.

Without vPars you would boot the HP-UX kernel directly from ISL as shown below:

![](bbox=[0.05, 0.43, 0.17, 0.51])

```
ISL> hpxp /stand/vmunix
```

You can boot the **vpmon** from ISL with the command below:

```
ISL> hpxp /stand/vpmon
```

The **vpmon** is invoked with this command and the **vpmon** prompt appears from which you can load vPars.

From the **vpmon** prompt we could issue the **vparload** command to load one or more Virtual Partitions. There are many options to the **vparload** command. There is no man page for **vparload** in Appendix A because it is a **vpmon** command. **vparboot** is a shell command so there is a man page in Appendix A for it. The following are the three forms of **vparboot** at the time of this writing: