
## Editing the lilo Configuration

If this is your first compilation, you will want to edit your /etc/lilo.conf file if you normally use lilo to configure your bootup sequence. Otherwise, you may want a lilo boot sector to a floppy. This is a minor safety precaution in case you do not want someone to be able to reboot the machine into single-user mode and then redo the root password. You can always take the floppy with you and prevent unguarded reboots. Securing the machine physically against any unauthorized access is also a strong recommendation. However, if you place lilo on the Master Boot Record (MBR) or /dev/hda1, and if the machine does indeed reboot, it should come back up after a few moments and will not require that you manually replace the boot floppy.

Also be sure to back up your distribution copy of the lilo.conf file. If you make a change and then realize that your new setting may not work, having this backup copy will enable you to restore the default setting easily. Copy the preinstalled lilo.conf to another filename. Here is one possible suggestion:

```bash
# cp /etc/lilo.conf /etc/lilo.conf.DIST
```

The `DIST` extension identifies this file as a distribution file or one that came with the default install.

This file is quite dependent upon your system. Listing 14.1 shows an example from my own system with comments included. The first section is the default location for the new kernel and is usually the /boot/vmlinuz file. The second section lists the older file that you might currently be using. It is a tried and tested kernel, and so I usually give it the release number as its name. The last kernel version is usually the older distribution kernel. If using a Red Hat 5.x or 6.x release, this can be a 2.0.x or 2.2.x kernel and so it is named linux.old.

### Listing 14.1 A Sample lilo.conf File

```ini
#
# general section
#
boot=/dev/hda
# install=/boot/boot.b
# message=/boot/message
prompt

#
# wait 20 seconds (200 10ths) for user to select
# the entry to load
#
timeout=200

#
# default entry
#
image=/boot/vmlinuz
  label=linux
  root=/dev/hda1
  read-only

#
# golden entries
#
image=/boot/vmlinuz-2.2.16
  label=linux.golden
  root=/dev/hda1
  read-only

#
# older entries
#
image=/boot/vmlinuz-old
  label=linux.old
  root=/dev/hda1
  read-only

#
# end of file
#
```

In this file, I have granted myself a couple of options for safety. First, when Linux first boots up, it normally stops at the LILO: prompt. I have given myself 20 seconds in which to choose the type of kernel that I wish to boot. At that prompt, I can press the Tab key to see the available choices: linux, linux.golden, and linux.old. If your machine is a dual- or triple-boot machine, you might also include settings for a particular Windows version or some other operating system. It is in lilo.conf that you can enter settings for alternative boot partitions.

During the initial installation, be sure that any other operating systems are already installed because lilo will overwrite any boot record on the Master Boot Record. Red Hat will also attempt to detect other systems and grant you the options to set one of them up as the default system.

The first entry in lilo.conf is also the default OS. Because the kernel labeled linux is the first entry, that kernel will begin booting after 20 seconds, without any interaction on my part. By placing an entry for the Windows partition in the first section, I ensure that Windows is my default boot OS. If something goes wrong with the new kernel, I also have the option to boot back into my older kernel. Be sure to save the System.map and the vmlinuz files in the /boot directory. Their names should correspond to their appropriate entries in lilo.conf.

![](img/a0884097af3186d9b4f616aaa3f065b0_503_0.png)

If you want to boot up other operating systems, Listing 14.2 shows an example of how you can set up Windows as the default OS. Though the Linux partition is not listed first, Linux provides a default option for specifying Windows as the default OS into which the system can boot.

### Listing 14.2 A Default lilo.conf File Generated During the Red Hat Install

```ini
boot=/dev/hda
map=/boot/map
install=/boot/boot.b
prompt
timeout=50
linear
default=windows

image=/boot/vmlinuz-2.2.14-5.0
label=linux
read-only
root=/dev/hda2

other=/dev/hda1
label=windows
```

The user can configure the options specified in the lilo.conf file. You may specify any system you wish. To change the default OS, simply substitute `linux` for `windows` under the `default=` option. As you can see, this drive is separated into two partitions, `/dev/hda1` and `/dev/hda2`. Linux is installed on `/dev/hda2`, hence the `root=` variable.

For some people, saving the kernel directly back onto the hard drive is an impractical option, or a disagreeable one at best. They like to make absolutely sure that the newly compiled kernel works before changing any configurations or settings to their machine. Making sure that the kernel works usually involves first copying the new kernel directly onto a bootable floppy. After you have stored the kernel on the floppy, you insert the floppy in the floppy drive and reboot the machine. If the machine boots successfully, you can safely load the kernel onto your drive. Once that is complete you can edit the lilo.conf file to point to the new kernel and have it be the default kernel. Make sure to rename or backup the original kernel so that you have something to fall back on if the newer kernel does not boot.

## Placing the New Kernel on Boot Media

Now that both your kernel and the modules have successfully compiled and you have edited your boot configuration, you can place the new kernel and System.map on your boot media. This means either locating them somewhere on the hard drive or placing them on a floppy disk. If you choose to keep the new kernel on the hard drive, you will need to locate the new kernel now called `vmlinuz`, and place it in your `/boot` directory and in your `/` (root) directory. Because the default kernel under Red Hat comes installed on the `/boot` directory, keeping any newer kernels there can be convenient also.

If you wish to manually copy the new kernel to the `/boot` directory, use the following two commands to copy the newly created files to their default location.

```bash
cp /usr/src/linux/arch/i386/boot/bzImage /boot/vmlinuz
cp /usr/src/linux/System.map /boot/System.map
```

Another option that I like to move as well is the System.map file. It usually is created right in the linux/ directory and can also be placed in the /boot directory as well.

On the latest Red Hat release, there are several symbolic links pointing to the files vmlinuz and/or System.map. You can remove these symbolic links. The files they point to are usually identifiable by their release number.

An even easier method of installing the newly compiled Linux kernel is to issue the following command after running the make modules and make modules_install commands.

```bash
make install
```

This command copies the correct kernel to the proper location. The preceding example that manually copies the kernel is x86-specific. Using the make install command under Red Hat will locate the correct kernel for your distribution and then copy it to the proper boot directory. It will also move the older kernels and retain the symbolic links to then point to your new kernel. At the end it will also run the /sbin/lilo command and reread your lilo.conf file. This is why you edit the LILO configuration before installing the kernel.

If you wish to place the newly created kernel and the System.map file on a floppy disk, copy them by using the following command:

```bash
cp /usr/src/linux/arch/i386/boot/bzImage /dev/fd0
```

Once you have the new kernels in place, you need to let lilo know where everything is situated. Run the following command to make the lilo executable re-read the configuration file and to enable lilo to identify the newly created kernels. The command also informs the system where to look for the older kernels.

If booting a kernel from off the floppy drive, change the /etc/lilo.conf file to point to the proper location. Rather than using the placing the root=/dev/hda1 in your lilo.conf file, replace it with root=/dev/fd0.

Again, if you wish to skip the make install command and run lilo by hand instead use the following command.

```bash
/sbin/lilo
```

You may also wish to run a similar older command that works well, which does more of the task automatically.

```bash
make zlilo
```

This command installs the kernel and makes the floppy bootable, but does not do anything with the modules.
