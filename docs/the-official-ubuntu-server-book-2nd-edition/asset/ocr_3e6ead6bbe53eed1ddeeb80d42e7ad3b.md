![](bbox=[0.25, 0.14, 0.72, 0.62])

Figure 10-3 Partition menu with RAID devices created

appears as before, but above them are the RAID devices. These devices will be numbered and will display their RAID level as well as the overall size of the RAID device.

The next step is to tell the partitioner how to use each of these new RAID devices. Select the unlabeled partition on the line under each RAID device and hit Enter. From there you can configure the file system, mount point, and other options as if it were an ordinary partition. See Figure 10-4 for an example of how my final partition menu looked when I was done. Once you are finished, select "Finish partitioning" and write the changes to disk. If you get a prompt asking whether to boot when the array is degraded, read through the description of the risks of doing so and select Yes or No. The installation program will then continue the rest of the install process. Skip ahead to the Software RAID Management section to learn how to use the features of the mdadm package to manage your software RAID.

# Configure RAID after Installation

You may choose to add RAID storage to a server after the initial installation. Later in the chapter I discuss how to migrate from a single disk to a RAID array and how to migrate from one RAID type to another, but for now I will