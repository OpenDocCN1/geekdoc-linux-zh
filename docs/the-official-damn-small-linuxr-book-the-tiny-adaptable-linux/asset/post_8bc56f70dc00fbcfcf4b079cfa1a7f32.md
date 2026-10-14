
+   3. Start DSL using the pendrive.bat.
+   4. From DSL running in Qemu, add files and change settings in your home directory.
+   5. From DSL, download any extensions you need into the /cdrom/mydsl directory.
+   6. From DSL, click DSLpanel, click Backup/Restore, and click Backup.
+   7. From the DSL menu, select Apps->Net->SMBclient and enter your specifics to connect (Domain, Machine, Share, Name, and Password). Then, type the following from the SMB prompt:
+   
+   smb:\> lcd /cdrom
+   smb:\> put backup.tar.gz
+   smb:\> lcd mydsl
+   smb:\> cd mydsl
+   smb:\> put just_downloaded_extension
+   
+   (Repeat for all newly downloaded extensions)
+   
+   smb:\> quit
+   8. Shut down DSL.

## Using Your DSL-Embedded Equipped Pen Drive for Native BIOS Booting

This subject is covered in Chapter 6, “Running a Native Pen Drive Install,” but I want to mention that you have to apply Syslinux to the drive before the BIOS will recognize the pen drive as being bootable. There is a version of Syslinux that is usable from within Windows, but we are getting feedback that sometimes it doesn’t quite work with users’ systems. You can always set up Syslinux by booting Damn Small Linux from the LiveCD provided with this book.

Be sure to read the readme.txt found in the dsl-embedded.zip file. There are tips in there that may be useful if you run into difficulties.

## Increasing Qemu’s Performance with KQemu

So, you think having an embedded Linux system at your disposal is pretty cool, but you wish the speed was a little faster? The Qemu developers have a fix for you.

KQemu is a Qemu accelerator, and it works nicely. During my experiments, I have reduced the virtual bootup time in half. This is a great development that makes running DSL-Embedded that much more enjoyable.

With the default configurations in DSL-Embedded bat files (1st-boot.bat, dsl-base.bat, dsl-vhd.bat, and printer.bat), we have Qemu run without KQemu enabled. You have to modify the .bat file of your choice configuration to enable KQemu acceleration.

Look for the following option on the qemu.exe command line:

```
-no-kqemu
```

Replace it with

```
-kernel-kqemu
```

You need to download the Microsoft Windows build of KQEMU at

http://www.h7.dion.ne.jp/~qemu-win/

At the time of this writing, version Kqemu-1.3.0pre11-install.exe was available. After downloading and installing KQEMU, you need to run the following:

```
net start kqemu
```

Either type it into the run command or open a command prompt and type the command in there. Figure 7-2 shows an example of KQemu being enabled from the Run utility:

![](img/af53325d7f38f1cdafca9f44568e4ab8_166_0.png)

**FIGURE 7-2** Enter `net start kqemu` into the Run utility.

That should be all you need to do to enjoy your accelerated performance. Now go ahead and launch DSL-Embedded in your usual way.

## RUNNING DSL IN VMPLAYER—VMWARE’S FREE VIRTUAL MACHINE

VMPlayer is VMWare’s free virtual machine. It is a free download, but not freely distributable. Parts of the technology behind VMPlayer are open source and are apparently licensed under the GPL. We will explore using Damn Small Linux with the VMPlayer virtual machine from within the Microsoft Windows environment.

Figure 7-3 shows an example of Damn Small Linux running in VMPlayer in Windows XP.

![](img/af53325d7f38f1cdafca9f44568e4ab8_167_0.png)

# FIGURE 7-3 Damn Small Linux running in VMPlayer on a Windows XP host system.

## Comparing VMPlayer to Qemu

In many ways, Qemu and VMPlayer performance benchmarks are comparable. Some studies have put Qemu with the KQEMU accelerator ahead in performance. In my limited testing, VMPlayer boots faster and seems to struggle less with resources during general use. It could be that our default settings in Qemu are limiting the system; we will have to do further testing to figure out the discrepancy.

VMPlayer is much larger than Qemu (25MB versus less than 2MB), and it needs to be installed on the host operating system. So, there is not a way to run VMPlayer from a low impact pen drive like QEMU. If you are in a situation where you are using a Windows computer and you want a way to get back into running
