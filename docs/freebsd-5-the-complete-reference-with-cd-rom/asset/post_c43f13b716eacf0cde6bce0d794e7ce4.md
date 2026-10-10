
## at least some of these commands, such as those to view and manipulate files.

To run GUI programs, you must start X by typing a single command (`startx`), which loads X and whatever X environment you've chosen as the default or configured for yourself as an individual user. Some FreeBSD GUI environments are very similar to those of Windows or other GUI OSs, so if you're familiar with such tools, you shouldn't have too much trouble adjusting to FreeBSD. When you're done, you should log off of your account to reduce the risk of it being abused by a passer-by. When you need to turn the computer off or reboot it, you should be sure to use a proper shutdown procedure, rather than simply hitting the power switch or Reset button.

![](img/f34d37e3abe9f4517128e54f80ab2616_134_0.png)

# The Complete Reference

![](img/f34d37e3abe9f4517128e54f80ab2616_136_0.png)

## Chapter 4

Coexistence with Other Operating Systems

As described in earlier chapters, and particularly in Chapter 2, FreeBSD can run either as the only OS on a computer or as one of two or more OSs. In the second case, it's important that you know how FreeBSD and your other OS or OSes interact, so that you can make the best use of your available resources and avoid mistakes. (It's possible to completely destroy one OS's installation from another OS, for instance.) This chapter covers these interactions. It begins with a look at the boot process, focusing on the configuration and use of boot loaders. The next topic is partition management—addressing partitions in a way that won't cause problems. Most partitions hold filesystems, and these usually differ from one OS to another. Thus, a large part of this chapter is devoted to this important topic. Finally, the chapter concludes with a look at ways you can run non-FreeBSD programs, such as Linux or Windows applications, in FreeBSD.

### Note

> If your computer runs FreeBSD and nothing else, most of this chapter won't interest you. The information on filesystems might be relevant if you need to mount floppy disks, Zip disks, or the like in FreeBSD, though. Likewise, you might want to run non-FreeBSD programs from time to time, even on a FreeBSD-only system.

### Configuring the Boot Process

Chapter 2 included basic information on installing the FreeBSD boot loader. This boot loader works well in most simple configurations, such as FreeBSD with Windows and nothing else on a single hard disk. More advanced configurations, though, may require you to modify the default FreeBSD boot loader configuration, or even use another boot loader. This section covers these topics, as well as using the FreeBSD boot loader to pass special options to the FreeBSD kernel. These options can alter the way FreeBSD treats hardware, thus enabling the OS to boot on some hardware that might cause problems for the default configuration.

#### Understanding Boot Loaders

When an x86 computer boots, it looks for code to run in several locations, starting with the computer's *Basic Input/Output System (BIOS)* ROM. The BIOS, in turn, tells the computer to look for a *boot sector* on one or more boot devices. During installation, you may have needed to reconfigure your BIOS to boot from a floppy disk or CD-ROM drive, for instance. Normally, the computer boots from the hard disk, either because the BIOS is configured to check it first or because other potential boot devices don't contain bootable media. The boot sector of a hard disk is more commonly known as the *Master Boot Record (MBR)*. A standard MBR contains code that, in a typical DOS or Windows installation, redirects the boot process to use code in the boot partition's boot sector. This code boots DOS or Windows. This simple one-OS configuration is illustrated in Figure 4-1. (Note that Figure 4-1 shows a FreeBSD partition, but the boot process depicted doesn't *boot* it.)

![](img/f34d37e3abe9f4517128e54f80ab2616_138_0.png)

**Figure 4-1.** The standard single-OS x86 boot process involves redirecting the CPU to run code from various places.

In a multi-OS system, some part of this boot process must be modified to support a choice of OSs. The usual approach using the standard FreeBSD tools is to replace the MBR's boot code with new code that enables you to choose between FreeBSD and the other OSs on your system. This approach works well in simple configurations, and with a bit of work, in more complex setups. Some OSs support their own boot loaders, though, and third-party boot loaders also exist. These may replace the MBR with their own code, replace the Windows boot sector, intercept the boot process further down the line in the Windows boot process, or install a special partition dedicated to redirecting the boot process. If you want to use such a boot loader, you may, as described in the upcoming section, “Using a Third-Party Boot Loader.”

One important complication to understand is the so-called 1024-cylinder limit. Traditionally, x86 computers have used cylinder/head/sector (CHS) addressing, in which three numbers uniquely identify any given sector on the hard disk. The BIOS was originally written when hard disks were much smaller than they are today, and so it included limits on CHS numbers that today produce a maximum addressable disk size of just under 8GB. (Limits in the old IDE interface further reduced this to 504MB, but BIOS trickery raised this limit to the BIOS maximum of just under 8GB in the mid-1990s). Because the boot process relies heavily upon the BIOS, these limits, and particularly the limit of 1024 cylinders, have been important ones in booting any OS.

By the late 1990s, BIOSes were shipping with features (known as *extended INT13 calls*) that enabled them to overcome the 1024-cylinder limit, but boot loaders need to support these BIOS features. FreeBSD's boot loader does so, but you may need to add special parameters to get it to boot FreeBSD from above the 1024-cylinder limit. (Note that a disk may be larger than 1024 cylinders but still need no special options, if the FreeBSD boot files reside below this limit.) Third-party boot loaders may also need support for these extended INT13 calls in order to boot FreeBSD (or any other OS) from above the 1024-cylinder limit.

#### Using the FreeBSD Boot Loader

If you followed the instructions in Chapter 2 and installed the FreeBSD boot loader in the usual way, your system should boot FreeBSD and possibly one or more other OSs, such as DOS or Windows. You may want to modify this configuration, though. For instance, you might want to add another OS to the menu of options that appears when the computer starts. You can do this by reconfiguring the boot loader with the *boot0cfg* command. This command's syntax is:

```
boot0cfg [-Bv] [-b boot0] [-d drive] [-f file] [-m mask] 
[-o options] [-s slice] [-t ticks] disk
```

In most cases, you won't need more than one or two of these options. In particular, typing `boot0cfg -B /dev/ad0` as *root* installs the boot loader in the conventional way on the first EIDE disk; the utility searches for all bootable partitions and, at boot time, gives you the option of which to boot. (You would use `/dev/da0` instead of `/dev/ad0` if your system uses SCSI disks.) In case you need them, the options to this command are:

- **-B**  
  This option tells `boot0cfg` to install MBR code to permit selection of the OS you want to use. Omit this option if you're using another primary boot loader in the MBR, as described in the upcoming section, "Using a Third-Party Boot Loader."

- **-v**  
  Normally, `boot0cfg` provides little feedback. This option causes it to display additional information (that is, to be verbose), such as the slices it's making bootable.

- **-b boot0**  
  To install a boot loader, `boot0cfg` copies a file from elsewhere into the MBR. This file defaults to `/boot/boot0`, but you can specify another file if you want to use some other boot loader. You might use this option if you want to try an experimental FreeBSD boot loader, but otherwise you won't use it. (If you use a third-party MBR boot loader, it should have its own way to install in the MBR.)

- **-d disk**  
  The BIOS refers to hard disks by a drive number. The first physical disk is normally 0x80 (that is, hexadecimal 80, or decimal 128), the second is 0x81, and so on. If you've configured your BIOS to boot from the second or subsequent disk, you may need to use the `-d` option to tell it one to use. Pass the BIOS drive identifier, such as `0x81`, as *disk*. For simplicity, arrange your drives so that the FreeBSD boot loader and any OS that must boot from the first physical disk can reside on that disk; then you don't need this option.

- **-f file**  
  This option tells `boot0cfg` to back up the existing MBR to the specified file. This procedure can be useful in case there are problems; you can restore the original MBR using the *dd* utility.

- **-m mask**  
  Normally, `boot0cfg` can tell which slices should be listed in the initial boot selections menu. If it guesses wrong, you can use this option to override it. The *mask* variable takes a value from 0 (no slices enabled) to `0xf` (decimal 15; all slices enabled). The *mask* is a four-bit binary code, with each bit corresponding to one slice.

- **-o options**  
  You can specify any of three special options with this parameter. Precede an option with *no* to reverse its meaning (for instance, *nopacket* as opposed to *packet*). If you want to use multiple options, you can separate them with commas. The options are:
  - **packet**  
    The default value is *nopacket*, which causes the MBR boot loader to use the old CHS addressing modes. This value effectively limits
