
Finally, you might want to look at the COAST policy archive at ftp://coast.cs.purdue.edu/pub/doc/policy to see what some real life security policies look like.

## Means of Securing Your Site

This document will discuss various means with which you can secure the assets you have worked hard for: your local machine, your data, your users, your network, even your reputation. What would happen to your reputation if an intruder deleted some of your users’ data? Or defaced your Web site? Or publishing your company’s corporate project plan for next quarter? If you are planning a network installation, there are many factors you must take into account before adding a single machine to your network.

Even if you have a single dial-up PPP account, or just a small site, this does not mean intruders won’t be interested in your systems. Large, high profile sites are not the only targets—many intruders simply want to exploit as many sites as possible, regardless of their size. Additionally, they may use a security hole in your site to gain access to other sites you’re connected to.

Intruders have a lot of time on their hands, and can avoid guessing how you’ve obscured your system just by trying all the possibilities. There are also a number of reasons an intruder may be interested in your systems, which we will discuss later.

## Host Security

Perhaps the area of security on which administrators concentrate most is host-based security. This typically involves making sure your own system is secure, and hoping everyone else on your network does the same. Choosing good passwords, securing your host’s local network services, keeping good accounting records, and upgrading programs with known security exploits are among the things the local security administrator is responsible for doing. Although this is absolutely necessary, it can become a daunting task once your network becomes larger than a few machines.

## Network Security

Network security is as necessary as local host security. With hundreds, thousands, or more computers on the same network, you can’t rely on each one of those systems being secure. Ensuring that only authorized users can use your network, building firewalls, using strong encryption, and ensuring there are no rogue (that is, unsecured) machines on your network are all part of the network security administrator’s duties.

This document will discuss some of the techniques used to secure your site, and hopefully show you some of the ways to prevent an intruder from gaining access to what you are trying to protect.

## Security through Obscurity

One type of security that must be discussed is “security through obscurity.” This means, for example, moving a service that has known security vulnerabilities to a nonstandard port in hopes that attackers won’t notice it’s there and thus won’t exploit it. Rest assured that they can determine that it is there and will exploit it. Security through obscurity is no security at all. Simply because you may have a small site, or a relatively low profile, does not mean an intruder won’t be interested in what you have. We’ll discuss what you’re protecting in the next sections.

## Organization of This Document

This document has been divided into a number of sections. They cover several broad security issues. The first, “Physical Security,” covers how you need to protect your physical machine from tampering. The second, “Local Security,” describes how to protect your system from tampering by local users. The third, “Files and Filesystem Security,” shows you how to set up your filesystems and permissions on your files. The next, “Password Security and Encryption,” discusses how to use encryption to better secure your machine and network. “Kernel Security” discusses what kernel options you should set or be aware of for a more secure system. The “Network Security” section describes how to better secure your Linux system from network attacks. The section “Security Preparation (Before You Go Online)” discusses how to prepare your machine(s) before bringing them online. Next, the section “What to Do during and after a Break-in” discusses what to do when you detect a system compromise in progress or detect one that has recently happened. In “Security Sources,” some primary security resources are enumerated. The Q and A section, “Frequently Asked Questions,” answers some frequently asked questions, and finally you will find “Conclusion.”

The two main points to realize when reading this document are:

- Be aware of your system. Check system logs such as `/var/log/messages` and keep an eye on your system.
- Keep your system up-to-date by making sure you have installed the current versions of software and have upgraded per security alerts. Just doing this will help make your system markedly more secure.

## PHYSICAL SECURITY

The first layer of security you need to take into account is the physical security of your computer systems. Who has direct physical access to your machine? Should they? Can you protect your machine from their tampering? Should you?

How much physical security you need on your system is very dependent on your situation, and/or budget.

If you are a home user, you probably don't need a lot (although you might need to protect your machine from tampering by children or annoying relatives). If you are in a lab, you need considerably more, but users will still need to be able to get work done on the machines. Many of the following sections will help out. If you are in an office, you may or may not need to secure your machine off hours or while you are away. At some companies, leaving your console unsecured is a termination offense.

Obvious physical security methods such as locks on doors, cables, locked cabinets, and video surveillance are all good ideas, but beyond the scope of this document.

### Computer Locks

Many modern PC cases include a “locking” feature. Usually this will be a socket on the front of the case that allows you to turn an included key to a locked or unlocked position. Case locks can help prevent someone from stealing your PC, or opening up the case and directly manipulating/stealing your hardware. They can also sometimes prevent someone from rebooting your computer on their own floppy or other hardware.

These case locks do different things according to the support in the motherboard and how the case is constructed. On many PCs they make it so you have to break the case to get the case open. On some others, they make it so that it will not let you plug in new keyboards and mice. Check your motherboard or case instructions for more information. This can sometimes be a very useful feature, even though the locks are usually very low quality and can easily be defeated by attackers with locksmithing.

Some cases (most notably SPARCs and Macs) have a dongle on the back that, if you put a cable through, attackers would have to cut the cable or break the case to get into it. Just putting a padlock or combo lock through these can be a good deterrent to someone stealing your machine.

### BIOS Security

The BIOS is the lowest level of software that configures or manipulates your x86-based hardware. LILO and other Linux boot methods access the BIOS to determine how to boot up your Linux machine. Other hardware that Linux runs on has similar software (OpenFirmware on Macs and new Suns, Sun boot PROM, etc.). You can use your BIOS to prevent attackers from rebooting your machine and manipulating your Linux system.

Many PC BIOSs let you set a boot password. This doesn’t provide all that much security (the BIOS can be reset, or removed if someone can get into the case), but might be a good deterrent (i.e. it will take time and leave traces of tampering). Similarly, on S/LINUX (Linux for SPARC processor machines), your EEPROM can be set to require a boot-up password. This might slow attackers down.

Many x86 BIOSs also allow you to specify various other good security settings. Check your BIOS manual or look at it the next time you boot up. For example, some BIOSs disallow booting from floppy drives and some require passwords to access some BIOS features.

![](img/a3584dae761d2e3abed8bf40d7637389_485_0.png)

**NOTE**

If you have a server machine, or you set up a boot password, your machine will not boot up unattended. Keep in mind that you will need to come in and supply the password in the event of a power failure.

### Boot Loader Security

The various Linux boot loaders also can have a boot password set. LILO, for example, has *password* and *restricted* settings; *password* always requires password at boot time, whereas *restricted* requires a boot-time password only if you specify options (such as *single*) at the LILO prompt.

Keep in mind when setting all these passwords that you need to remember them. Also remember that these passwords will merely slow the determined attacker. They won’t prevent someone from booting from a floppy, and mounting your root partition. If you are using security in conjunction with a boot loader, you might as well disable booting from a floppy in your computer’s BIOS, and password-protect the BIOS.

If anyone has security-related information from a different boot loader, we would love to hear it (*grub*, *silo*, *milo*, *linload*, etc).
