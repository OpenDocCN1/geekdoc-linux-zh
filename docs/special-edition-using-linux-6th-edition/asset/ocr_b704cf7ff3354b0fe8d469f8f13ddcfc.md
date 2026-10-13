It is important that all the necessary steps be performed in the correct order.

If you've already performed these steps at one point, you might want to obtain and install a patch to the kernel instead of starting over with a new source. Patching a kernel is not as difficult as it sounds and is explained later in this chapter. Using a patch will save you a significant amount of time and bandwidth.

# ## OBTAINING THE KERNEL SOURCE (STEP 1)

Your distribution comes with the kernel source. However, this source might not be the most current. By the time you're comfortable with your new Linux installation, a newer kernel is probably out. Kernel sources are released when there are significant new drivers to add, old drivers with important updates, or security updates.

The best way to get the kernel sources is not from the RPMs on your distribution's CD-ROM, unless you know you need something special that Caldera, Red Hat or your distribution producer has added that is not yet in the stable kernels. You can get pristine sources from `ftp://ftp.us.kernel.org` (a number of mirror sites are also available) in the subdirectory `pub/linux/kernel/v2.4`. Look for the latest source and download it. Put the file in `/usr/src`.

> > **Note**
> >
> > If you want to keep the graphical Caldera bootup screen, you'll need to use the Caldera-supplied SRPMs to do so because they have been modified to support the graphical boot process. The latest kernels in SRPM format should be available on the Caldera FTP site. See Chapter 17, “Building/Rebuilding a Package,” section “Advanced Package Management,” for details as well as instructions on the Caldera Web site.

Create a directory for the kernel source. Normally, you'll want it to be something like `linux-2.4.10`, where the `2.4.10` is the kernel version you just downloaded (mkdir `linux-2.4.10`). Then create a link to this directory called `linux` (`ln -s linux-2.4.10 linux`).

If the `linux-2.4.10` already exists because you've installed the RPM, remove it first. You can do this either by removing the RPMs (recommended) or by simply removing the `linux-2.4.10` directory before you begin.

# ## PREPARING THE SOURCE TREE (STEP 2)

When you've successfully completed step 1, you're going to prepare the source tree. The source tree is all the source code opened into its own portion of the directory tree and ready for use.

The command to open the file you downloaded depends on which file you grabbed. The source file is either `linux-2.4.10.tar.gz` or `linux-2.4.10.tar.bz2`. Each uses a slightly different set of commands to open.

For `linux-2.4.10.tar.gz`, use the following command:

```
```sh
tar zxvf linux-2.4.10.tar.gz
```
```