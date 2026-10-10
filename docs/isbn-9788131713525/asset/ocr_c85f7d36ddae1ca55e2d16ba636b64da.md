The MTD subsystem is enabled via the first configuration option, which is selected via the first check box shown in Figure 10-1, Memory Technology Device (MTD) Support. The next two entries into the configuration shown in Figure 10-1 enable special device-level access to the MTD devices, such as Flash memory, from user space. The first one (`CONFIG_MTD_CHAR`) enables character device mode access, essentially a sequential access characterized by byte-at-a-time sequential read and write access. The second (`CONFIG_MTD_BLOCK`) enables access to the MTD device in block device mode, the access method used for disk drives, in which blocks of multiple bytes of data are read or written at a time. These access modes allow the use of familiar Linux commands to read and write data to the Flash memory, as you shall shortly see.

![](bbox=[0.05, 0.36, 0.77, 0.75])

# FIGURE 10-1
MTD configuration

The `CONFIG_MTD_MTDRA` element enables a special test driver that enables us to examine the MTD subsystem even if we don't have any MTD devices (such as Flash memory) available. Coupled with this configuration selection are two parameters