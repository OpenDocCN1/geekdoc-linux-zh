# MorpheusArch 3/10

MorpheusArch had fairly limited appeal as compared to some of the other repair and rescue distros in the *Roundup*. It only really advertises the inclusion of *TestDisk* and *PhotoRec* utilities that help users to recover accidentally deleted files. The distro boots up to a locked LXQt desktop and there’s no mention of the default password (`arch`) on the project’s website, which is a serious oversight.

The LXQt desktop has a handful of apps including *Firefox*, *Zenmap* and *LFTP*. The desktop provides no indication on how to proceed, which is rather disorientating.

The lack of getting started documentation inside the distro or even on the project’s website doesn’t help matters either.

One of the best things about the MorpheusArch project is the assistantive *LinDiag* utility. However, it isn’t included with the distro and you’ll have to manually pull it in, which again is not made clear.

![](bbox=[0.07, 0.48, 0.35, 0.6])

# SystemRescueCd 7/10

Earlier versions of the distro had a comprehensive boot menu with over a dozen boot options.

There’s an option to copy the entire system to RAM and the default option will boot the system to a console, which lists the command to configure the keyboard layout and start the graphical environment.

The distro uses the Xfce desktop and houses a handful of essential productivity apps in its menus including a web browser, a VNC viewer, a password manager and some developer-friendly tools.

A majority of the rescue tools in the distro are CLI-based and just like MorpheusArch the distro doesn’t give any pointers to help users get started. Its saving grace is its website, which is flush with all sorts of detailed documentation to help first-time users use the distro.

![](bbox=[0.37, 0.48, 0.65, 0.6])

# Ultimate Boot CD 9/10

Unlike the other distros here, UBCD is unique in that it directly boots into its customised text-based menu. The menu divides the packaged utilities into categories based on the part of the computer that they influence, such as HDD, Peripherals, System and such.

Step into the category to view the list of entries for the individual tools. Some categories, such as HDD, are further divided into different tasks, such as Boot Management, Data Recovery, Disc Cloning and Disk Wiping, and more.

As you move across each tool in a category, the menu displays brief but useful information about it. The menus might be text-based, but the clear categories and helpful descriptions mean the distro can be easily navigated and used by inexperienced users. Coupled with the useful information on the project’s website, UBCD makes for a great choice.

![](bbox=[0.67, 0.48, 0.95, 0.6])

# Security and privacy features

What can they do besides repair and rescue?

While the primary purpose of these distros is to rescue a broken computer, many also pack in a bunch of tools to help secure your system and prevent privacy leaks. That’s because it isn’t uncommon for security issues to bring down a computer. On occasion, you might also have to sanitise an installation before bringing it back up in order to ensure the health of the other machines it interacts with on the network.

MorpheusArch has the *nmap* tool for exploring the network, which you can use through the *LinDiag* script. The distro also has a couple of utilities which can wipe filesystem signatures from a device and also set hard disk parameters.

AIO System Rescue Toolkit also includes *nwipe* to help securely zap files. ALT Linux Rescue includes tools to securely delete files and investigate security breaches. The distro is designed for several scenarios, but unfortunately ensuring privacy isn’t one of them.

SystemRescueCd does take steps to enhance your privacy if you’re using a YubiKey. It includes the *YubiKey Manager* app as well as the *YubiKey Personalization Tool* that can help you reprogram the configuration slot on the device to enable additional authentication functionalities such as OTP. Besides these, you’ll find several tools to help you delete data securely including *shred*, *wipe*, and the *THC-Secure Deletion* tool.

Much like its peers, although ensuring security and privacy aren’t among the goals of UBCD, the distro does have a specific category where it lists about a dozen tools, including several low-level utilities, for securely wiping disks. There are also scanners to sniff out viruses and malware.

# VERDICT

AIO SYSTEM RESCUE TOOLKIT 4/10
ALT LINUX RESCUE 6/10
MORPHEUSARCH 5/10
SYSTEMRESCUECD 7/10
ULTIMATE BOOT CD 7/10

You can use any of these distros to securely delete files so that they aren’t recoverable. Otherwise, their security features vary quite a bit.