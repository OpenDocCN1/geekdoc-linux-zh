
To configure GRUB to boot the new Linux kernel (the one you just built), follow these steps:

- Copy the new kernel binary to the /boot directory.

The new, compressed kernel file is in the `arch/i386/boot` subdirectory where the kernel source resides. The kernel filename is usually `bzImage`. I simply copy that file to the `/boot` directory with the same name.

If the kernel filename is `vmlinux`, make sure you use `vmlinux` instead of `bzImage`. You can change the kernel filename in `/boot` to anything you want, as long as you use the same filename when referring to the kernel in the GRUB menu file in Step 3.

- Copy the new System.map file from the kernel source directory to the /boot directory.

- Use your favorite text editor to edit the GRUB menu file to add the following lines in the file:

```
title New Linux kernel (2.6.11)
root (hd0,2)
kernel /bzImage root=/dev/hda10 ro
initrd /initrd-2.6.11.img
```

On your system, make sure that the `root` line is correct — instead of `(hd0, 2)`, list the correct disk partition that’s mounted on `/boot`. Also, use the correct filename for the kernel image file (for example, `/vmlinux` if the kernel file is so named). The `root` option on the kernel line must be set to the device name of the partition mounted on the `root` directory (`/`) of the Linux filesystem.

Note: The initrd line refers to the initrd file that you created in an earlier step.

- Save the GRUB menu file and exit the editor.

Now you’re ready to reboot the system and try out the new kernel.

# Rebooting the System

After you finish configuring GRUB, you can restart the system. While you’re still logged in as `root`, type the following command to reboot the system:

```
reboot
```

When you see the GRUB screen, select the name you assigned to the new kernel in the GRUB menu file.

After the system reboots, you see the familiar graphical login screen. To see proof that you’re indeed running the new kernel, log in as a user, open a terminal window, and type `uname -srv`. This command shows you the kernel version, as well as the date and time when this kernel was built. If you upgraded the kernel source, you see the version number for the new kernel. If you have simply rebuilt the kernel for the same old kernel version, the date and time matches the time when you rebuilt the kernel. That’s your proof that the system is running the new kernel.

![](img/11709a8f88c8cd03868a929dc94c0e2b_521_0.png)

If the system *hangs* (you don’t see any output on-screen or any disk activity), you may have skipped a step during the kernel rebuild. You can power the PC off and on to reboot. This time, select the name of the old working kernel at the GRUB screen.

# Book VI

# Security

The 5th Wave By Rich Tennant

![](img/11709a8f88c8cd03868a929dc94c0e2b_522_0.png)

# Contents at a Glance

Chapter 1: Introducing Linux Security....499

Chapter 2: Securing a Linux Host....513

Chapter 3: Improving Network Security ....529

Chapter 4: Performing Computer Security Audits .....547

# Chapter 1: Introducing Linux Security

In This Chapter

- Establishing a security policy and framework
- Understanding host security issues
- Understanding network security issues
- Translating computer security terminology
- Keeping up with security news and updates

In this chapter, I explain why you need to worry about security and give you a high-level view of how to get a handle on security. I explain the idea of an overall security framework and explain the two key aspects of security — host security and network security. I end this chapter by introducing you to the terminology used in discussing computer security.

## Why Worry about Security?

In today’s networked world, you have to worry about your Linux system’s security. For a standalone system, or a system used in an isolated local area network (LAN), you have to focus on protecting the system from the users and the users from one another. In other words, you don’t want a user to modify or delete system files, whether intentionally or unintentionally. Also, you don’t want a user destroying another user’s files.

If your Linux system is connected to the Internet, you have to secure the system from unwanted accesses over the Internet. These intruders — or *crackers*, as they are commonly known — typically impersonate a user, steal or destroy information, and even deny you access to your own system (known as a *Denial of Service* or DoS attack).

By its very nature, an Internet connection makes your system accessible to any other system on the Internet. After all, the Internet connects a huge number of networks across the globe. In fact, the client/server architecture of Internet services, such as HTTP (Web) and FTP, rely on the wide-open network access the Internet provides. Unfortunately, the easy accessibility to Internet services running on your system also means that anyone on the Net can easily access your system.

If you operate an Internet host that provides information to others, you certainly want everyone to access your system's Internet services, such as FTP and Web servers. However, these servers often have vulnerabilities that crackers may exploit in order to cause harm to your system. You need to know about the potential security risks of Internet services—and the precautions you can take to minimize the risk of someone exploiting the weaknesses of your FTP or Web server.

You also want to protect your company's internal network from outsiders, even though your goal is to provide information to the outside world through a Web or FTP server. You can protect your internal network by setting up an Internet *firewall*—a controlled access point to the internal network—and placing the Web and FTP servers on a host outside the firewall.

## Establishing a Security Framework

The first step in securing your Linux system is to set up a *security policy*—a set of guidelines that state what you enable users (as well as visitors over the Internet) to do on your Linux system. The level of security you establish depends on how you use the Linux system—and on how much is at risk if someone gains unauthorized access to your system.

If you're a system administrator for one or more Linux systems at an organization, you probably want to involve company management, as well as the users, in setting up the security policy. Obviously, you cannot create a draconian policy that blocks all access. (That would prevent anyone from effectively working on the system.) On the other hand, if the users are creating or using data valuable to the organization, you have to set up a policy that protects the data from disclosure to outsiders. In other words, the security policy should strike a balance between the users' needs and the need to protect the system.

For a standalone Linux system, or a home system that you occasionally connect to the Internet, the security policy can be just a listing of the Internet services that you want to run on the system and the user accounts that you plan to set up on the system. For any larger organization, you probably have one or more Linux systems on a LAN connected to the Internet—preferably through a firewall. (To reiterate, a *firewall* is a device that controls the flow of Internet Protocol—IP—packets between the LAN and the Internet.) In such cases, thinking of computer security across the entire organization systematically is best. Figure 1-1 shows the key elements of an organization-wide framework for computer security.

The security framework outlined in Figure 1-1 includes:

- Determining the business requirements for security
- Performing risk assessments
- Establishing a security policy
- Implementing a cyber security solution that includes people, process, and technology to mitigate identified security risks
- Continuously monitoring and managing security

In the following sections, I discuss some of the key elements of the security framework.

![](img/11709a8f88c8cd03868a929dc94c0e2b_526_0.png)

# Determining business requirements for security

The business requirements identify the security needs of the business — the computer resources and information you have to protect (including any requirements imposed by applicable laws, such as the requirement to protect the privacy of some types of data). Typical security requirements may include items such as the following:

- Enabling access to information by authorized users
- Implementing business rules that specify who has access to what information
- Employing a strong user-authentication system
- Denying malicious or destructive actions on data
- Protecting data from end to end as it moves across networks
- Implementing all security and privacy requirements that applicable laws impose
