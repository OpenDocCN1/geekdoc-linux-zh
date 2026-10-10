
## Scenario

Two devices (a second parallel port and a sound card) are both trying to use IRQ 5 on your computer, and this is causing both devices to malfunction. You must reconfigure the system so that this conflict is avoided.

## Scope of Task

This task involves reviewing jumper settings, BIOS options, and Linux software configuration. As such, it's fairly wide reaching, although each individual part of the task is restricted in scope.

### Duration

This task should take about half an hour to complete. Once you're familiar with hardware reconfiguration, you can perform individual parts of this task in a few minutes.

### Setup

Ideally, you should have a computer with both a second parallel port and a sound card configured to use IRQ 5. In practice, though, you're unlikely to have a computer with this precise configuration, so you should simply follow the descriptions in this task and review your own hardware's capabilities and your own Linux system's software configuration. Start with your Linux system powered down. You'll need to enter the BIOS, and you may want to physically examine the hardware in your computer.

### Caveats

Physically examining or modifying hardware runs the risk of damaging it by accidental static discharge or other mishandling. If possible, you should use an anti-static wrist strap or take other anti-static precautions, such as regularly grounding yourself by touching a radiator while you work. Software adjustments run the risk of rendering your system unbootable if you make a mistake, so be careful not to make inappropriate changes.

## Procedure

To perform this task, you will review several types of settings for your hardware. If you were really fixing a problem, you would adjust one or more of these options to fix the problem. In reality, you'll probably leave these settings alone.

### Adjusting Hardware Jumpers

A hardware jumper is a set of two or more metal pins that stick out of a motherboard, plug-in card, hard disk, or other device and may be shorted together by using a small cap made of metal and plastic. Figure 2.4 shows a typical jumper, shown in the open (unshorted) position. Some jumpers, such as the one shown in Figure 2.4, support only open and closed positions. Others provide three or more pins that may be shorted together in different ways to configure the device.

![](img/f430a19bdf014c43ad7c2d594afd5b21_97_0.png)

### Adjusting BIOS Options

Unfortunately, I can’t give you any hard-and-fast rules as to when to set jumpers in particular positions. You must consult the device’s documentation to learn how to set its jumpers to achieve particular goals. (Some devices print basic documentation on the hardware itself, but most require you to read separate documentation.)

Older ISA cards used jumpers as the exclusive means of configuration. You’d use jumpers to set IRQs, I/O ports, and other options and sometimes to disable or enable particular functions of a board. Later ISA cards and PCI cards use PnP technology to enable the computer to set these features, but such cards still sometimes sport a jumper or two. Hard disks also commonly use jumpers to set master/slave status, SCSI ID number, and other features, although hard disk standards are moving toward software-driven configuration as well.

If one or both of the problem devices in this task’s scenario uses jumpers, you can avoid the conflict by setting the jumpers of one device so that it uses an unused IRQ rather than the IRQ 5 that’s in contention. If the device is part of a multi-function card and you don’t need the function in question, you may be able to use a jumper to disable it. For instance, if you don’t need the second parallel port, you may be able to disable it on the plug-in card by setting an appropriate jumper while leaving the card’s other hardware (such as RS-232 serial ports) working. A still more radical solution is, of course, to completely remove the card, but this will disable all of its functions.

If one or both of the devices in this task’s scenario are built into the motherboard or are PCI devices, you may be able to use BIOS settings to resolve the conflict. Review Figure 2.3 and the description earlier of the Integrated Peripherals area of the BIOS configuration utility. The options in this area are similar to the jumpers on older hardware; you can use them to enable or disable motherboard functions and to adjust various hardware options. If you need only one parallel port, you could disable one of them from this screen. Most motherboards provide only a single parallel port, though, so you might need to combine this action with reconfiguring a plug-in parallel port card via its jumpers or PnP settings.

Another way to adjust BIOS options to avoid conflicts is to review its PnP features. These options vary substantially from one BIOS to another, but you might want to review the options provided by your hardware. In Figure 2.1’s BIOS, you could select the PNP/PCI Configurations menu option, which produces a screen in which you can set a few features, such as whether you’re using a PnP-aware OS (recent versions of Linux qualify, but selecting Yes tells the BIOS to do more PnP configuration itself, which sometimes helps clear up problems) and what IRQs to assign to the devices in particular PCI slots. These options might help you to avoid an IRQ conflict.

## Adjusting Linux PnP Settings

Finally, Linux itself provides several PnP options you can adjust. For older ISA cards, two methods have existed for PnP configuration: the `isapnp` utility and kernel configuration options. The `isapnp` utility is largely outdated, so I don’t describe it in detail here.

Both ISA PnP boards and PCI boards can be configured via kernel options. These are passed to the kernel at boot time via your boot loader configuration or to separate kernel modules via lines in the `/etc/modules.conf` file. (Some distributions build this file from files in the `/etc/modules.d` directory tree, so you may need to edit files in that directory instead and then type `modules-update` or a similar command to rebuild `/etc/modules.conf`.) Unfortunately, the details of how to set specific options are highly device specific, so you’ll need to consult the documentation for the Linux driver for the device to learn how to do the job. To adjust the IRQ used by a device, you might pass an option such as `irq=10`, or perhaps simply `10`, to the driver. When the driver loads, it configures the device to use the requested IRQ instead of the one the kernel or BIOS would otherwise have assigned it.

![](img/f430a19bdf014c43ad7c2d594afd5b21_98_0.png)

> Sometimes PnP software reconfiguration doesn’t work as you’d expect. This can happen because you’ve specified an option that won’t work for the device, because the driver recognizes a conflict that you didn’t see, or because of an error in the way you specified the option. Review the driver’s documentation and try again if you can’t seem to get an option to change.

For devices whose drivers are built into your kernel, you should modify your boot loader configuration. This is typically `/boot/grub/grub.conf` or `/boot/grub/menu.lst` for the Grand Unified Boot Loader (GRUB) or `/etc/lilo.conf` for the Linux Loader (LILO). Phase 5 describes boot loader configuration in more detail.

## Criteria for Completion

To complete this task, you should have reviewed three methods of reconfiguring your hardware: hardware jumpers, BIOS options, and Linux PnP settings (particularly the `/etc/modules.conf` file). Making random changes is inadvisable, but you should have familiarized yourself with the basic form of all these hardware configuration options. If your hardware is particularly modern, though, you might be hard-pressed to find any jumpers at all.

# Task 2.4: Configure USB Devices

USB 1.0, the first incarnation of USB, was finalized in 1996. Since then, USB has played an increasingly important role. Today, mice, printers, scanners, digital cameras, CD-RW drives, and many other devices can interface to computers via USB. Thus, being able to configure USB devices to work with Linux is an important skill.

USB was designed to permit relatively painless *hot-plug* operation, meaning that devices can be plugged into the computer and unplugged while the computer operates. Unfortunately, this type of operation is alien to Linux's basic driver model. Thus, to accommodate USB's hot-plug nature, various special utilities and interfaces have been developed. Configuring USB devices means working with these utilities.

## Scenario

To support efforts to digitize old documents and presentations, your employer has purchased a film scanner. This scanner uses a USB interface and must be configured to work correctly with Linux; however, your default Linux configuration prevents ordinary users from accessing the scanner when it's plugged into the computer and turned on. You must reconfigure Linux to enable ordinary users to work with the scanner.

## Scope of Task

This task involves examining configuration and system status files to learn about your hardware and then modifying configuration files to have the system configure hardware in the way you want. If you're lucky, you won't need to engage in the low-level configuration described here; many distributions provide tools that automatically detect and configure a wide variety of USB devices. These tools fail with obscure or very new hardware, though, necessitating manual configuration.

## Duration

This task will take about half an hour to complete. Once you're familiar with the procedure, you should—in theory—be able to perform similar tasks in half that time. In practice, though, adding hardware often involves overcoming unexpected problems. Thus, when you add your own truly unknown hardware, you could end up taking anywhere from a few minutes to several hours to configure it.

## Setup

To complete this task, you need *root* access to a Linux computer. Ideally, you should have a scanner or other USB device that's not accessible to ordinary users in your default configuration. (For this task, I use a Minolta DiMAGE Scan Elite 5400 film scanner and Fedora Core 5 as the example hardware and software.) This example assumes that your system uses the *udev* filesystem for handling device files, which is common with modern distributions. If you lack
