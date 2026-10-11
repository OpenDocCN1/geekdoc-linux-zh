
## Chapter 11: Adding New Hardware

You should note that all the supported devices are not in your current kernel. You may need to download a recent development kernel and may also need third-party software. Kernel 2.2.7 and later contain the basic USB code and support for a few devices. Each new kernel supports new devices. You must also recompile the kernel to enable USB support in the configuration screen, where you must also enable support for a controller and device.

You can determine whether USB support was installed correctly and whether your USB device was loaded by looking the logs in `/var/log/messages`. Once the controller is detected, you can start configuring your devices.

## Configuring USB Mouse

If you have a USB mouse, begin configuring it by creating the device node like so:

```
mknod /dev/usbmouse0 c 180 16
```

When complete, edit your `X86Config` file and change the protocol to `IMPS/2` and the port to `/dev/usbmouse0`.

## Configuring USB Keyboard

USB keyboards should require no configuration; they should work normally. Make sure that your BIOS supports the USB keyboard by contacting your manufacturer.

## Configuring USB Printer

To support a USB printer, create a special device node using this command line:

```
mknod /dev/usblp0 c 180 0
```

When complete, you can configure the printer like any other printer in your `/etc/printcap` file or by using the `printtool` utility.

## Troubleshooting

When everything fails, it's time to troubleshoot. This section introduces a few actions you can take to make Linux detect your hardware and where you can look for the scripts that control the bootup process and the detection of new hardware.

Before looking for scripts to modify, refer to any manuals and other documentation that came with your system and with the device you are trying to install.

Although they may not talk about Linux configuration, they will include useful information such as the IRQ and I/O ports supported by the device.

You should also determine the purpose for any jumpers that may exist on the device. Some newer devices don't have jumpers, but you should check any troublesome devices to see whether they exist.

## LILO

The initial system configuration is done in `/etc/lilo.conf`. This file tells LILO what parameters to pass to the kernel, which file is the actual kernel, and which hard disk should be booted on startup. If you have problems with the initial startup, type `man lilo.conf` to refer to the complete syntax of commands.

One such parameter you may need to add is the amount of memory (RAM) you have. If Linux detects 16MB and you know you have 24MB, add the following line to the configuration file:

```
append = 'mem=24M'
```

If you have a problem where a device is not detected by the kernel, you need to look elsewhere for a solution. For example, most drivers are loaded from the configuration and startup scripts, as we will examine in the next sections.

## Configuration Scripts

The scripts used by the Red Hat utilities are stored in `/etc/sysconfig`, which contains files describing the mouse, network card, network configuration, and PCMCIA. Unless you are confident that you know exactly what you are doing, you should not attempt to modify any file in this subdirectory.

If you find that the Red Hat utilities are not able to complete the settings you require and have tried everything else, you may need to edit the configuration files manually. They are text files, so you can edit them with your favorite text editor—but again, you must be very careful. You may want to check the Red Hat Linux Web site to search for a solution to your specific problem before delving into this procedure.

## Startup Scripts
