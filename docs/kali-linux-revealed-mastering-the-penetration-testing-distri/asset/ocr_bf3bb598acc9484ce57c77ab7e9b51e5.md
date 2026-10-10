Next, the installer asks you to enter an encryption passphrase (Figure 4.23, “Enter Your Encryption Passphrase” [page 89]). In order to view the contents of the encrypted partition, you will need to enter this passphrase every time you reboot the system. Note the warning in the installer: *your encrypted system will only be as strong as this passphrase.*

![](bbox=[0.09, 0.18, 0.91, 0.71])

# Figure 4.23 Enter Your Encryption Passphrase

The partitioning tool now has access to a new virtual partition whose contents are stored encrypted in the underlying physical partition. Since LVM uses this new partition as a physical volume, it can protect several partitions (or LVM logical volumes) with the same encryption key, including the swap partition (see sidebar “Encrypted Swap Partition” [page 86]). Here, LVM is not used to make it easy to extend the storage size, but just for the convenience of the indirection allowing to split a single encrypted partition into multiple logical volumes.