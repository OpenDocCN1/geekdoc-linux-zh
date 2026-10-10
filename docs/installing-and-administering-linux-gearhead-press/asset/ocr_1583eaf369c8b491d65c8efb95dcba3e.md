![](bbox=[0.14, 0.06, 0.86, 0.35])

Figure 2.8 LILO configuration—boot options.

# Step 7. Installing and Configuring LILO

The first LILO configuration screen (Figure 2.8) will appear and will ask about the use of linear mode. As it clearly says, it pertains to SCSI drives only—and we will address this issue in our SCSI installation after this section. On older versions of the Red Hat distribution, it did not state that it was specific to SCSI installations. If you were to choose to enable this feature, it would have no effect—nor would it cause any problems. We choose to remove the default \* on Use linear mode . . . .

We plan to use LILO to manage the disk (see Figure 2.9). Therefore, we are going to choose the Master Boot Record (MBR) option. If there were some other alternate operating system partitions on the disk, the Linux configuration program would see them and you could choose to add them to your /etc/lilo.conf file as boot choices (see Figure 2.10). Because we are only installing the one Linux system, we will let this choice default to booting Linux. If your system is a production system, we recommend that no other operating systems should share the disk. This situation will primarily simplify the maintenance, backup, and recovery of the system. In other working environments, however, such as at home, you might appreciate having more than one operating system from which to choose.

# Step 8. Network Configuration

We are going to use a static IP address in the screen shown in Figure 2.11. But, if this system is going to be a print server or will run any services for other hosts, it should receive its own static IP address so that it will not