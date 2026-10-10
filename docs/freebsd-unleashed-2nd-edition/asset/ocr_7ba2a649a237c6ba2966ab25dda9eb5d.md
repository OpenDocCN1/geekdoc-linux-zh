396
CHAPTER 17 Keeping Up to Date with FreeBSD

# Troubleshooting the Kernel Upgrade and Installation

Building and installing the kernel is the riskiest stage yet in the `make world` process, and the safeguards in the system that protect the kernel during this process add to the arcane nature of the procedure by being quite user unfriendly. Here are two few common failure modes and their solutions:

+   * The compiler fails.

The kernel sources can fail to build for the same reasons that building the rest of the system can fail. If you can't resolve the failure yourself, try the mailing lists.

+   * The system won't let me install my new kernel!

If you've set `securelevel` to 1 or higher, `make installkernel` won't be able to remove the `schg` flag on the kernel. You will have to reboot into single-user mode to complete each step of the process. Remember that when you boot into single-user mode (using `boot -s` from the loader prompt), none of the filesystems will mount automatically; you'll need to run `mount -a` before you can go into /usr/src and run the `make installkernel` process.

# Running and Troubleshooting `make installworld`

After you've completed your kernels, it's time to reboot into single-user mode, which prevents multiuser processes (either run by other users or by daemons operating automatically) from altering files that you'll be upgrading. Collisions of this type can lead to serious instability. Using single-user mode is also a good idea simply because of the slight speed advantage and because it's nice to be able to bring the system back online completely upgraded and ready to go.

Reboot into single-user mode by using the `reboot` command. When you reach the loader (the countdown phase), press a key to get the loader prompt and then enter the `boot -s` command to bring the system up far enough for you to verify that the new kernel is working and to complete the installation.

> **NOTE**
> 
> If the system fails to come up (it might crash, it may spew error messages, or there may be any number of different failure modes), first try rebooting normally to see if the behavior is different from case to case, and to try to determine what in the new kernel is causing problems. If you still have no luck, it's time to drop back to your old kernels. Reboot again, and try booting single-user with the backup kernel, as you saw a little earlier. Keep trying kernels until you reach the one you were using before you began the upgrade (which should boot without trouble-so far, the kernel is the only thing you've changed in the system). You may want to postpone your `make world` and try again from scratch after you've resolved the problem with your new kernel. Chances are that a kernel failure at this point is indicative of a more widespread and temporary problem that will be resolved in the source in the near future.