# TABLE 32.1 Continued

| Name | Description |
|---|---|
| Multimedia devices | Drivers for hardware implementations of video and sound devices such as video capture boards, TV cards, and AM/FM radio adapter cards. |
| Graphics support | Configures VGA text console, video mode selection, and support for frame buffer cards. |
| Sound | Large subsection to configure supported sound card drivers and chipset support for the kernel. |
| USB support | Universal Serial Bus configuration options. Includes configuration for USB devices, as well as vendor-specific versions of USB. |
| File system | Configuration options for supported file system types. |
| Additional device driver support | A section for third-party patches. |
| Profiling support | Profiling kernel behavior to aid in debugging and development. |
| Kernel hacking | This section determines whether the kernel will contain advanced debugging options. Most users will not want to include this option in their production kernels because it increases the kernel size and slows performance by adding extra routines. |
| Security options | Determines whether NSA Security Enhanced Linux (SELinux) is enabled. |
| Cryptographic options | Support for cryptography hardware (Ubuntu patches not found in the "vanilla" kernel sources). |
| Library routines | Contains zlib compression support. |

After you select all the options you want, you can save the configuration file and continue with step 7 in the kernel compiling checklist shown earlier.

# Creating an Initial RAM Disk Image

If you require special device drivers to be loaded in order to mount the root file system (for SCSI drives, network cards, or exotic file systems, for example), you must create an initial RAM disk image named /boot/initrd.img. For most users, it is not necessary to create this file, but if you are not certain, it really does not hurt. To create an initrd.img file, use the shell script /sbin/mkinitrd.

The format for the command is the following:

```
/sbin/mkinitrd file_name kernel_version
```

where file_name is the name of the image file you want created.