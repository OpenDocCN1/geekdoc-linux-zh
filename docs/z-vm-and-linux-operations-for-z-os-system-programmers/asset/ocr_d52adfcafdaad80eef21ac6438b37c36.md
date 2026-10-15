# 4.5 Running a z/OS image as a z/VM guest

The process of running a z/OS system as a guest of z/VM is much the same as running any other guest system. In this section, we discuss moving a z/OS image from a z10 LPAR to run as a z/VM guest operating system. This should work for systems on any System z processor. It could be the scenario for many sites because of LPAR constraints, server consolidation, or to simplify their test environment. One strength of z/VM is its ability to virtualize hardware in the form of (for instance) virtualized coupling facilities, channel-to-channel adapters and more. One could also manipulate the device addresses, thus minimizing the need for administration of the hardware configuration (IOCDS). The latter enables a quick and efficient path to set up new test images when desired.

This process is essentially the same as though a new z/OS system were being created to run as a z/VM guest. Determining the resources needed would still have to be planned and at the point were we IPL the existing z/OS system as a z/VM guest, the z/OS installation process would then be performed.

# 4.5.1 z/OS candidate description

The z/OS image we are moving from an LPAR to z/VM guest had specific resources defined for it. It had a SYSNAME of SC59, and you might want use that as your z/VM user ID, but it is not required. It had no CTCs and was not utilizing CFs or other hardware to take into account, in addition to communication through OSA adapter. It had a hardware configuration similar to the simplified listing in Table 4-2:

Table 4-2: Table of resources

| Type of resource | Description | Comment |
|---|---|---|
| Sysname | SC59 | Can be the z/VM user ID |
| Memory / CS | 2 GB | Initial storage |
| Processors / CPs | 4 | — |
| DASD / Disks | 53 volumes | 3390 Mod 3 and Mod 9 |
| OSA network adapter | 2000-2005 | QDIO |
| Console | Address F008 | 3270 console |