
## Memory and scheduler work

known as TLBs (translation lookahead buffers). TLBs store virtual address (VA) to physical address (PA) translations within microprocessor cores after the core has performed a ‘page walk’ off the page tables representing the virtual memory areas (VMAs) in use by the running process (known as a ‘task’ within the kernel). When a process switch occurs, it is necessary to ensure that stale translations aren’t seen by the new one, so a TLB ‘invalidate’ is performed. This was traditionally expensive on x86 (as opposed to modern alternatives, such as 64-bit ARM), but is less so with the enablement for PCID (process context ID) tag support in the TLBs, which allows for translations of two different address spaces to exist independently at the same time without conflicting.

One of the most interesting questions is whether Linus will decide to merge the initial patches for the RISC-V architecture. We covered RISC-V in the last issue. Version 4 of the enablement patch for the new architecture was posted by Palmer Dabbelt, incorporating all the existing feedback comments that had been given so far. While the support isn’t complete (it doesn’t provide actual drivers for specific real ‘machines’), it does form the basis for what can be used to enable actual platforms later. As of this writing, it has not been merged into Linus’s tree for Linux 4.13.

Jérôme Glisse has posted another iteration of his work on cache coherent device memory (CDM), which layers upon his existing work on HMM (heterogeneous memory management). The idea of CDM is to provide a generic means for Linux to handle ‘coherent’ memory – that is to say, memory which behaves as normal RAM and whose contents can be shared between different devices and cores without getting out of sync – present on plug-in adaptors, such as certain future graphics cards and workload accelerator modules in servers.

The AMD team have posted updates to its Secure Memory Encryption and Secure Encrypted Virtualization patches. SME can be used to ‘mark individual pages of memory as encrypted through the page tables. A page of memory that is marked encrypted will be automatically decrypted when read from DRAM.’ The technology allows users (especially, data centre operators) to ensure that data is not only encrypted at rest (on disks), but also even whenever it leaves the microprocessor. Thus, a chain of trust can be established between an end user running a virtual machine supporting Secure Encrypted Virtualization (SEV) and AMD (though various additional capabilities built into the chip) in such a way that the data centre hosting company running the VM is unable to introspect the content of the running VM’s memory. I look forward to having such a feature for my cloud VMs.

Nicolas Pitre is working on a ‘scheduler minification’ patch series that aims to ‘[make] it possible to configure out some parts of the scheduler such as the deadline and real-time scheduler classes’. The Linux scheduler code is what determines when it is time for the system to switch from running one process (known as a task within the kernel), to another.

On a modern multi-core system, there may be many processes actually running at a time, but there are rarely enough CPU cores even now to actually execute every task simultaneously. Instead, the illusion of multitasking is provided by means of the scheduler rapidly switching from one process to another. Nico aims to make it possible to shrink the scheduler code for use in very small embedded systems, where some of the normal features aren’t required. This could be true, for example, in some of the larger IoT devices on the market.

Finally this month, I would like to take a moment to request your input on kernel development topics you would like to see covered in depth in future issues. If you’ve got a burning kernel topic you’d like to see covered in this column, tweet or write to us at linuxuser@futureret.com.

![](img/fb76008333fb7aef815b136f9f1afe5f_16_0.png)

![](img/fb76008333fb7aef815b136f9f1afe5f_17_0.png)

## Secure your system

Reading Sun Tzu is just the first step in tackling those who seek to harm your Linux machines. Shashank Sharma reveals what you need to do next.

There’s an entire thread on Reddit discussing whether Professor Alastor ‘Mad-Eye’ Moody, from the Harry Potter books, ever uttered the catchphrase, ‘Constant vigilance!’ Regardless of who to attribute the statement to, if you are concerned about securing your Linux installation, whether as a home user or a system administrator, it’s good advice to adopt this mantra.

The entire gamut of operations that you can employ to defend yourself from threats are spread over the next few pages. We will walk you through creating a digital moat around your machines to stop the marching invaders in their tracks. This involves using password managers such as KeePass2, using secure login, working with ClamAV to detect trojans, viruses and malware, and more. We’ll also show you how you can make life easier for yourself by automating a number of essential tasks, such as monitoring the ports for scanners using tools like Nmap and implementing tools such as logcheck and logrotate to make sense of all the logs that are generated by various apps and services. Along the way we’ll help you deploy a rootkit checker, discuss various password-strengthening measures and lots more. Finally, we’ll discuss the projects that are working towards making Linux even more secure for servers and networks and the efforts being made to make the kernel robust.

While we’re using Linux Mint for this feature (which is on the cover disc), all the tools discussed here can just as readily be used on any popular distro such as CentOS, Fedora, Mageia, Ubuntu, Debian and so on.

But first, baby steps. These are the tricks that you can and must adopt to secure your machines. If you’re interested in protecting a relative’s desktop which they use to browse the internet for their daily dose of entertainment or world politics, even these changes should be enough to set your mind at peace.

The first step is to choose the right distro. Sounds rather silly, but there’s a reason why you should give serious thought before settling on any Linux distro. You must consider whether the distro has a dedicated team working on pushing regular bug fixes and security updates. This is important, because in recent years many security weaknesses in popular Linux apps and services such as Samba have been found and unless you plug these your system is at risk. As a further precaution, you can also disable or uninstall services that you don’t need. For instance, if you only have a single machine at home and haven’t configured it for printing, you don’t need CUPS or the Samba services.

Another trick to employ is to opt for encryption. Most Linux distros nowadays allow you to encrypt your home folder during installation itself. You can also optionally use apps such as 4crypt to configure encryption on your current installation.

It’s important to not use dictionary words nor keywords such as qwerty or god111 as your passwords. The safest option is to ensure that passwords are reset regularly, and you can program your system to reject passwords that users have used previously:

Throughout the next few pages, you’ll find helpful hints and sometimes detailed instructions on how to adopt many of these principles into your Linux installation, apart from all the other advanced tools and tricks which you can use to thwart attackers.

![](img/fb76008333fb7aef815b136f9f1afe5f_18_0.png)

![](img/fb76008333fb7aef815b136f9f1afe5f_19_0.png)

To secure your machines, you must adopt a two-pronged strategy against potential attacks. The first involves preparing against intruders by installing a firewall and adopting better password policies. But this alone isn't enough. It's one thing to lock all the windows in your house, but you must still make sure no one got in before you closed them.

### Secure logins

Trusting passwords to hold all your data is foolhardy. To prevent unauthorised access to your machine, you can add an extra layer of authentication. One of the easiest methods is by using the Google Authenticator service, which issues a time-based authentication token to supplement the existing password challenge.

You can configure the utility for all configured users on your Linux machine, and each will receive the OTP on their configured Android devices. Unless a user enters the token that quickly expires, they can't log in. If you've configured your machine to allow remote logins, you can also configure Google Authenticator to work with SSH.

To implement this multi-factor authentication with Google Authenticator, you'll need the Google Authenticator PAM module. PAM stands for 'pluggable authentication modules' - a mechanism for plugging different forms of authentication into a Linux computer.

### Stronger passwords

The libpam-pwquality tool is another such module that you can use to improve your passwords. Open the `/etc/pam.d/common-password` file in your favourite text editor and identify the line that reads `password [success=1 default=ignore] pam_unix.so obscure sha512`. Add the `minlen` parameter to the end of the line if you want users to choose passwords with a minimum-length, e.g., `password [success=1 default=ignore] pam_unix.so obscure sha512 minlen=8`.

If you similarly want to ensure that users choose passwords with a mix of upper/lower-case letters and special characters, throw in parameters such as `[credit=-1 credit=-1 credit=-2]`, which forces users to respectively use one lower-case letter, one upper-case letter and two digits. You can install it using the `sudo apt install libpam-pwquality` command from the terminal.

### Check for rootkits

The password tricks discussed here, coupled with using a firewall and regular system updates, are a good start to protecting your system, but hackers often employ other means to do you harm. A common attack strategy used by attackers is privilege escalation, wherein after

### HOW TO: Use the Gufw firewall

![](img/fb76008333fb7aef815b136f9f1afe5f_19_1.png)

#### 01 Enable the firewall

Gufw is the graphical front-end for UFW, the uncomplicated firewall, which is one of the simplest front-ends for iptables. Fire up Gufw and change the Status toggle to On to enable the firewall. Gufw includes three profiles: public, office and home. The default is the home profile that denies all incoming traffic and allows all outgoing traffic. This will let you surf the internet without any issues.

![](img/fb76008333fb7aef815b136f9f1afe5f_19_2.png)

#### 02 Define policies

You can alter the incoming and outgoing policies by selecting one of the three options in their respective drop-downs. The Allow option will allow traffic without asking any questions. The Deny option will silently discard packets, while the Reject option also sends an error packet to the sender. A good idea is to deny all incoming connections and then selectively enable the ones you wish to allow.

![](img/fb76008333fb7aef815b136f9f1afe5f_19_3.png)

#### 03 Preconfigured rules

After you've set the policy for traffic, you can define specific rules for allowing traffic for individual apps and services. To create a rule, switch to the Rules tab and click on the 'Add' button. Use the Application pull-down in the Preconfigured tab to select the application you want to allow and Gufw will define the most effective rule for that app. Then press the 'Add' button to append the new rule.
