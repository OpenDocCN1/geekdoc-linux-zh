
## Upgrading a Custom Kernel

The upgrading process is made a bit more complex if you're running a custom kernel. The adventurous might try building a new version of the custom kernel and running with that, but you can set up a safety net by building a GENERIC kernel first and keeping it on hand to boot with if you have to. You'll also have your old kernel (the one currently running) as a fallback if all else fails.

Still within /usr/src, enter the following:

```
# make buildkernel KERNCONF=GENERIC
```

This is your first backup kernel, a GENERIC one built from the new sources. Now, if you haven't done this already, copy /boot/kernel1 to /boot/kernel1.prev (or some other name to indicate that this is the kernel you were already running and you know works). Next, install the newly built kernel:

```
# make installkernel KERNCONF=GENERIC
```

Then, copy this kernel to kernel1.GENERIC:

```
# cp /boot/kernel1 /boot/kernel1.GENERIC
```

Now, here's how to build your first-choice kernel (the custom one built from the new sources):

```
# make buildkernel KERNCONF=CUSTOM
```

Naturally, replace CUSTOM with whatever the name of your custom kernel is. Now, install the new custom kernel as /boot/kernel1:

```
# make installkernel KERNCONF=CUSTOM
```

To recap, your lineup of kernels is shown in Table 17.4.

### TABLE 17.4 Newly Available Kernels

| Kernel | Description |
| :--- | :--- |
| /boot/kernel1 | New custom kernel |
| /boot/kernel1.GENERIC | New GENERIC kernel |
| /boot/kernel1.prev | The old tried-and-true kernel |

When you reboot, if the first kernel fails, try booting with the new GENERIC kernel. As described in “Understanding the FreeBSD Startup Process” in Chapter 10, this is accomplished by pressing a key during the countdown to get to the loader prompt, then entering **boot kernel1.GENERIC**. If that fails, boot with the previously working kernel, and you'll be back to where you started.

## Troubleshooting the Kernel Upgrade and Installation

Building and installing the kernel is the riskiest stage yet in the `make world` process, and the safeguards in the system that protect the kernel during this process add to the arcane nature of the procedure by being quite user unfriendly. Here are two common failure modes and their solutions:

-   **The compiler fails.**
    The kernel sources can fail to build for the same reasons that building the rest of the system can fail. If you can't resolve the failure yourself, try the mailing lists.

-   **The system won't let me install my new kernel!**
    If you've set `securelevel` to 1 or higher, `make installkernel` won't be able to remove the `schg` flag on the kernel. You will have to reboot into single-user mode to complete each step of the process. Remember that when you boot into single-user mode (using `boot -s` from the loader prompt), none of the filesystems will mount automatically; you'll need to run `mount -a` before you can go into /usr/src and run the `make installkernel` process.

## Running and Troubleshooting `make installworld`

After you've completed your kernels, it's time to reboot into single-user mode, which prevents multiuser processes (either run by other users or by daemons operating automatically) from altering files that you'll be upgrading. Collisions of this type can lead to serious instability. Using single-user mode is also a good idea simply because of the slight speed advantage and because it's nice to be able to bring the system back online completely upgraded and ready to go.

Reboot into single-user mode by using the `reboot` command. When you reach the loader (the countdown phase), press a key to get the loader prompt and then enter the `boot -s` command to bring the system up far enough for you to verify that the new kernel is working and to complete the installation.

> **NOTE**
>
> If the system fails to come up (it might crash, it may spew error messages, or there may be any number of different failure modes), first try rebooting normally to see if the behavior is different from case to case, and to try to determine what in the new kernel is causing problems. If you still have no luck, it's time to drop back to your old kernels. Reboot again, and try booting single-user with the backup kernel, as you saw a little earlier. Keep trying kernels until you reach the one you were using before you began the upgrade (which should boot without trouble—so far, the kernel is the only thing you've changed in the system). You may want to postpone your `make world` and try again from scratch after you've resolved the problem with your new kernel. Chances are that a kernel failure at this point is indicative of a more widespread and temporary problem that will be resolved in the source in the near future.

In single-user mode, you're root by default. The first thing to do is to mount your filesystems, so you can have access to the source tree; do this with a `mount -a` command and then verify that it worked by using `df`. Go back into `/usr/src` now and enter the final, most important part of the `make world` process. Installing the system binaries won't take as long as building them, but there is an equal chance of errors occurring—and this time, a failure will result in a partially altered system. Make sure to start your `script` output log before you begin this step. Here's the command for this step:

```
# make installworld
```

After this step completes, your binaries and kernel should be compatible; try running utilities such as `ps` and `top` to make sure they work properly. You'll get errors if the kernel and the binaries aren't built from the same source base, so if the utilities work, you can be pretty confident you successfully installed everything so far.

Anything that goes wrong during the `make installworld` step is potentially dangerous—you can end up with a partially installed system, with some of it compatible with the new kernel and some of it not. Fortunately, there are fewer things that can potentially go wrong than in the other stages. Here's the most common problem:

-   **The installer fails, citing a problem with permissions or ownership.**
    This is the reason for synchronizing your `/etc/group` and `/etc/master.passwd` files before installing the world. Check again to make sure some user or group isn't missing and try again.

## Using mergemaster to Check for Changed Configuration Files

There's only one step left in the `make world` process: merging the `/etc` hierarchy (and other miscellaneous areas such as `/var/log` and `/usr/share`). As you learned earlier, the `make world` steps don't touch `/etc`, in order to keep from stomping on heavily customized configurations. In earlier days, the only way to merge changes into `/etc` was to do it manually, a very painful and error-prone process. The mergemaster utility, a standard part of FreeBSD, makes this process a great deal simpler and safer.

A lot of safeguards are built into mergemaster; it's a very safe tool to use. Nevertheless, there always exists the risk of damaging your configuration, so as a precaution, you should make a backup copy of `/etc`. Fortunately, this is easy:

```
# cp -Rp /etc /etc.old
```

![](img/48eec858cce7dfb89da36a4d40b7daf3_430_0.png)

## Running mergemaster

Typically, mergemaster doesn’t really need any options; its defaults are set to sensible behaviors. This first time through, you can add the -v (verbose) option to see an explanation of what mergemaster is doing at each step. You can also use the -c option to use contextual diffs instead of unified ones. Here’s the command:

```
# mergemaster -cv
```

The first thing mergemaster does is create a temporary root directory and install everything from the relevant sources into it, including the various trees of files that need to be “installed” rather than simply copied over. This “staging area,” by default, is in /var/tmp/tmproot. It shows you a listing of files that only exist in /etc and not in the temporary root directory (generally, these are files you have added yourself, so it won’t touch them). Then, mergemaster proceeds to compare all the files in /etc and certain other locations with the new ones in /var/tmp/tmproot. Whenever it encounters files that don’t match, it displays the diff output in whatever pager you have specified in the PAGER environment variable (or more, by default).

When you scroll to the bottom of the diff display (or press > to jump directly to the bottom), you are given a list of choices for what to do with the new file, similar to Listing 17.3.

### LISTING 17.3 Options for Merging a File in mergemaster

```
********************
***  321,326  ***
---  327,333  ----

  kern_securelevel="-1"  # range: -1..3 ; '-1' is the most insecure
  update_motd="YES"      # update version info in /etc/motd (or NO)
  start_vinum=""         # set to YES to start vinum
  + unaligned_print="YES"  # print unaligned access warnings on the alpha (or NO).

  ############################################################################
  ##  Define source_rc_confs, the mechanism used by /etc/rc.* ##

      Use 'd' to delete the temporary .//etc/defaults/rc.conf
      Use 'i' to install the temporary ..//etc/defaults/rc.conf
      Use 'm' to merge the old and new versions
      Use 'v' to view the differences between the old and new versions again

      Default is to leave the temporary file to deal with by hand

      How should I deal with this? [Leave it for later]
```
