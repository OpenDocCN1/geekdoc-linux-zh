# Watchdog card support

If you would like to create a watchdog timer so that it can reboot the system in case of a failure, answer yes here.

```
Watchdog Timer Support (CONFIG_WATCHDOG) [N/y/?]
```

If you enable this feature, you have to create a special device called /dev/watchdog (major,minor=130,10) by using the mknod program. Then, you can use a watchdog daemon program that writes to this special device every minute. If the kernel detects that the daemon has not written to the device for one minute, it reboots the system.

```
/dev/nvram support (CONFIG_NVRAM) [N/y/m/?]
```

This feature allows you to create the special device /dev/nvram to have read/write access to nonvolatile memory in the real-time clock. Unless you know what you are doing, choose the default answer.

```
Enhanced Real Time Clock Support (CONFIG_RTC) [N/y/?]
```

This feature allows you to create a special device, /dev/rtc, which you can use to access the real-time clock in your system. Unless you know what you are doing, choose the default answer.

# Ftape, the floppy tape, video and misc. device support

If you have a floppy controller-based tape drive, you need to choose to add support for it here.

```
Ftape (QIC-80/Travan) support (CONFIG_FTAPE) [N/y/m/?]
```

```
/dev/agpgart (AGP Support) (CONFIG_AGP) [Y/m/n/?]
```

AGP (Accelerated Graphics Port) support will allow you to enable advanced AGP video card features. Choose the default answer if you have an AGP video card.

```
Direct Rendering Manager (XFree86 DRI support) (CONFIG_DRM) [Y/n/?]
```

If you use X Windows system (using Xfree86) then choose the default answer to enable the Direct Rendering Infrastructure (DRI) support which enhances your X experience by providing security, synchronization, and Direct Memory Access (DMA) transfers for your video cards. If you enable this you will have to select a module suitable for your video cards.