
The *real* memory ❶ is the amount of RAM physically installed in the computer, while the *avail* memory ❷ is the amount of memory left over after the kernel is loaded. I have 31,669MB of RAM ❸ available for real work, which more than suffices for the load on this system.

```text
❶ ioapic0 <Version 2.0> ❷ irqs 0-23 on motherboard
❸ ioapic1 <Version 2.0> irq 24-47 on motherboard
```

Here’s a fairly typical device entry. This device is known as ioapic, and the kernel has found that this hardware is version 2.0 and has extra information associated with it ❷. What’s more, we’ve found two devices of that type, numbered 0 ❶ and 1 ❸. (All devices are numbered starting with zero.) You can find out more about the device by reading the man page for the device driver. Almost all—but not all—device drivers have man pages.

```text
usbus0: EHCI version 1.0
usb us0 on ehci0
usb us0: 480Mbps High Speed USB v2.0
```

Not all device drivers print all their information on a single line. Here, we have a single device, usb us, that takes up three lines with just a single instance of the device. The only way to know that this is a single USB bus rather than three separate ones is to check the number of the device. All of these are for device number zero, so it’s a single device.

```text
❶ pci0: <simple comm> at device 22.0 (no driver attached)
❷ pcib8: <ACPI PCI-PCI bridge> irq 17 at device 28.0 on ❸ pci0
❹ pci8: <ACPI PCI bus> on ❶ pcib8
```

One interesting thing about the boot messages is that they display how your computer’s components are attached to one another. Here, we have pci0 ❶, a PCI interface directly on the mainboard. Then, there’s pcib8 ❷, PCI bridge number eight attached to pci0 ❸. We also find PCI bus pci8 ❹ attached to that PCI bridge ❺. As you read on, you’ll find individual devices attached to that bus. You might not be equipped to do much with this information now, but you'll find that having it available will be valuable when you have to troubleshoot a problem.

```text
em0: <Intel(R) PRO/1000 Network Connection> port 0xd000-0xd01f mem 0xfba00000-0xfba1ffff,0xfba20000-0xfba23fff irq 18 at device 0.0 on pci9
```

This entry shows em0, a network card of type em(4), and indicates that the card speaks gigabit Ethernet. We also see all sorts of information about its memory address, IRQ, and PCI bus attachment.

Every device on your computer has one or more entries like these. Taken as a whole, they describe your computer's hardware in reasonable detail. If you boot in verbose mode, you'll see even more detail—probably far more than you want.

![image](img/f11aeb3fa2ed406688e13ccb43ed9dab_150_0.png)

One key thing that the kernel displays in the boot messages is the device name for each piece of hardware. This is critical information for managing your system. Every piece of hardware has a device node name, and to configure it, you'll need to know that name. For example, earlier we saw an entry for an Ethernet card called em0. The card uses the em(4) driver, and the first device controlled by this driver has number zero. Your second device of this type would be em1, then em2, and so on.

Most devices that can be configured or managed have a device node entry somewhere under /dev. For example, the first optical drive is represented by the file /dev/cd0. These files are called device nodes, and they’re a convenient way to address a particular piece of hardware. Most device nodes can’t be directly accessed as a regular file; you can’t cat(1) a device node or copy another file to it. However, device nodes are used as arguments to specialized programs. For example, the hard drive that showed up at boot as ada4 is the same as the device node /dev/ada4. When you want to mount that hard drive, you can use the device node name and be sure you’re getting that exact piece of hardware.

## Multiuser Startup

Beyond single-user mode, you’ll find multiuser mode. This is the standard operating mode for a Unix-like OS. If you’re doing real work, your system is in multiuser mode.

When FreeBSD finishes inspecting the hardware and attaching all the device drivers appropriately, it runs the shell script /etc/rc. This script mounts all filesystems, brings up the network interfaces, configures device nodes, identifies available shared libraries, and does all the other work necessary to make a system ready for normal work. Most systems have different startup requirements; while almost every server needs to mount a hard drive, a web server’s operating requirements are very different from those of a database server, even if it’s running on absolutely identical hardware. This means that /etc/rc must be extremely flexible. It achieves flexibility by delegating everything to other shell scripts responsible for specific aspects of the system.

The /etc/rc script is controlled by the files /etc/defaults/rc.conf and /etc/rc.conf.

## /etc/rc.conf, /etc/rc.conf.d, and /etc/defaults/rc.conf

Much like the loader configuration file, the configuration of /etc/rc is split between two files: the default settings file, /etc/defaults/rc.conf, and the local settings file, /etc/rc.conf. Settings in /etc/rc.conf override any values given in /etc/defaults/rc.conf, exactly as with the loader.

The /etc/defaults/rc.conf file is huge and contains quite a few variables, frequently called knobs, or tunables. We aren’t going to discuss all of them, not only because knobs are added continually and such a list would be immediately obsolete but also because quite a few knobs aren’t commonly used on servers. Almost everything in a standard FreeBSD system has one or more *rc.conf* knobs, from your keyboard map to TCP/IP behavior. For a complete, up-to-date list, read rc.conf(5). To change *rc.conf* settings, you can either use a text editor or sysrc(8).

### sysrc(8)

While editing *rc.conf* by hand works just fine, in this age of cloud computing, it’s not sustainable across large numbers of machines. If you must change dozens of servers, you need a reliable way to alter the system without either manually editing each server’s config or resorting to sed/awk hackery.

FreeBSD includes sysrc(8), a command line program to consistently and safely alter /etc/rc.conf and friends from the command line. Additionally, sysrc(8) can display information about your system’s non-default settings.

Start by using -a to ask sysrc(8) what it knows about your host.

```bash
# sysrc -a
clear_tmp_enable: YES
defaultrouter: 203.0.113.1
dumpdev: AUTO
keymap: us.dvorak.kbd
-- snip --
```

You’ll get a list of all non-default /etc/rc.conf settings.

To have sysrc(8) enable a service, give it the variable name, an equals sign, and the new value.

```bash
# sysrc rc_startmsgs=NO
rc_startmsgs: YES -> NO
```

The variable rc_startmsgs is now set to no.

Remember that sysrc(8) is a tool for changing *rc.conf*, not for configuring FreeBSD. It does no validity checking. One of my very junior sysadmins really doesn’t want Bert logging in, and he took some bad advice on how to prevent that.

```bash
# sysrc bert=no
```

While this code sets `bert="no"` in /etc/rc.conf, this variable doesn’t do anything. Remove it with the `-x` flag.

```bash
# sysrc -x bert
```

Many FreeBSD configuration files closely resemble `rc.conf`. You can use `sysrc(8)` to manage them by adding the `-f` flag and the file name.

```bash
# sysrc -af /boot/loader.conf
```

Should you edit `rc.conf` or use `sysrc(8)`? If you’re making manual changes, then use whichever you prefer. Automation should err on the side of `sysrc(8)`. This book mixes examples of both.

### /etc/rc.conf.d/

If you use a server configuration system such as Puppet or Ansible, you might trust copying entire files more than editing them. Use `/etc/rc.conf.d/` files to enable services through such tools.

To manage a service in /etc/rc.conf.d/, create a file named after the service. That is, to manage `bsnmpd(8)` you’d create `/etc/rc.conf.d/bsnmpd`. Enable or disable that service in this file.

```bash
bsnmpd_enable=YES
```

I normally use Ansible’s service enabling features that directly alter /etc/rc.conf rather than /etc/rc.conf.d/, but use whatever you prefer.

The next few sections illustrate the types of things you can enable and disable in /etc/rc.conf. Each appears in /etc/defaults/rc.conf and can be overridden by an /etc/rc.conf entry. Each variable appears with its default setting.

### Startup Options

The following `rc.conf` options control how FreeBSD configures itself and starts other programs. These far-reaching settings affect how all
