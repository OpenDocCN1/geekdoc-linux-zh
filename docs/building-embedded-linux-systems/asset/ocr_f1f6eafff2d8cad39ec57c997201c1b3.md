![](bbox=[0.14, 0.09, 0.39, 0.28])

# # Root Filesystem Setup

Having built the files for our root filesystem and prepared the target’s storage device, we are now ready to set up the root filesystem on the target as well as any additional filesystems we may wish to use. First, we need to select a filesystem type for each of the filesystems. Then, we need to pack the filesystem’s content (the files and directories) in the selected format. Finally, we need to write those filesystems to a storage device on the target.

Because Linux supports quite a few different filesystem types and an embedded-Linuxbased system typically uses several of them, we will need to understand what types exist and how they can be put to use in our embedded device.

We shall begin, therefore, with a short overview of important properties that Linux filesystems offer to embedded devices. Then, we will continue with a guide to deciding on a filesystem type, and describe how they can be combined to fulfill different roles in the embedded device. Last but not least, we’ll cover the issue of upgrading embedded system software. As we shall see, this last topic ties in closely with the types and uses of the filesystems you choose to employ.

# ## Filesystem Types for Embedded Devices

This section will highlight the features and potential pitfalls to think about when selecting a filesystem and how these play out in some of the more popular filesystems used on Linux embedded devices.

# ## Characterizing Filesystems

To select the best filesystem or best combination of filesystems for an embedded device, it’s useful to compare them along a coherent set of characteristics. The following sections will present general filesystem properties that we will use later to characterize the current filesystems that are appropriate for embedded systems.