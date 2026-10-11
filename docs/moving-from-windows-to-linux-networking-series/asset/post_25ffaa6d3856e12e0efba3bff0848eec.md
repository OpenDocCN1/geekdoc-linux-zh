
# Getting Started

![](img/12d790664598bbf390261087fbe55bbc_27_0.png)

The next step is to select packages. A *package* is a logical grouping of a number of separate applications. The various applications that you can install with Linux are grouped so that you can easily pick the set of applications you are most likely to need, depending on how you intend to use the machine. Your choice of packages will determine what software gets installed on your PC. The options are:

- Personal Desktop
- Workstation
- Server
- Custom

Each of these is designed for a specific type of user. These various package configurations are summarized in [Table 2.1](#).

**Table 2.1: Installation Packages**

| Package | Contents/Purpose |
| :--- | :--- |
| Personal Desktop | This includes things the average home user would want, including Internet software such as Web browsers and e-mail clients. It also includes graphics programs and games. |
| Workstation | This is intended for the business user and includes productivity tools such as Open Office. |
| Server | This option is for servers. It will install a Web server, an FTP server, an e-mail server, and other server software. |
| Custom | This option allows you to pick any packages you want to install. |

Each of these packages is provided to make installation for a certain type of machine simple. However, this simplicity comes at a cost. If you choose Personal Desktop or Workstation, you will not be installing the Web server, FTP server, or other server packages. Conversely, if you select Server, you will not be installing many personal use items such as games. Since each of the preset options has some limitations, for our purposes we will choose Custom because we want several elements drawn from more than one package. When you select Custom, you will be prompted during the installation to select individual packages and applications to install. Later in this chapter we will cover the options you should select. For now, select Custom. This screen is shown in Figure 2.8.

![](img/12d790664598bbf390261087fbe55bbc_28_0.png)

**Figure 2.8:** Selecting packages.

The next screen will take you into the process of disk partitioning. This is probably the most important and complex part of the installation. As such, it warrants a separate part of this chapter, which will explain exactly what disk partitions are and how to partition.

# Disk Partitioning

The first question you might be asking yourself at this point is: what, exactly, is a disk partition? Partitioning is literally the process of dividing your hard drive into one or more useable segments. Simply put, you can divide your hard drive into several *logical drives*. A logical drive is simply a part of your hard drive that is treated as if it were a separate device. In other words, you can treat your hard drive as if it were several different hard drives. This is particularly useful for very large hard drives, and in cases where people wish to organize their computer more efficiently. You might have one partition that is designated for business, and another for home use or entertainment. A partition that is created to look like a separate hard drive is called a *logical drive*. Your computer might have only one actual hard drive, but several logical drives. Partitions and logical drives are not applicable only to Linux. All operating systems have partitions and can be divided into logical drives. Even if you are not going to partition your hard drive into multiple logical drives, you will still need to partition it. The only difference is that you will partition it into a single logical drive.

This brings us to the topic of partitioning a hard drive that will run Linux. Your hard drive must have at least one main partition. This primary partition is the starting point when your computer turns on. This is called the *root partition*. It must also have one *swap partition*. This of course brings us immediately to the question of what is a swap partition and why do you need one? A swap partition is a pretty incredible innovation. Essentially, it is a small segment of your hard drive that is set aside as a sort of backup for your PC’s memory. The way it works is rather simple. As you open up programs, they are loaded into memory. So, as you open more programs, you utilize more and more of your memory and there is less free memory for other programs to use. When a program has been idle for a while, the program is taken out of memory and moved to this swap file. If you later activate that program, for instance by clicking on it, it is moved from the swap file portion of the hard drive back into memory. By placing it into a special segment of the hard drive, it can be more quickly reloaded into memory than if you simply loaded it off the normal hard drive partition. Thus the name ‘swap’, since it swaps programs from memory to a special segment of the hard drive.

All operating systems support swap partitions. The swap partition’s size should be at least equal to the amount of RAM your machine has, but no more than two and one half times the RAM. That means if you have 128 megabytes of RAM, your swap partition should be at least 128 megabytes in size but no more than 320 megabytes.

Now that you understand disk partitions, at least in a rudimentary fashion, you are ready to partition your hard drive. You will notice that the Red Hat Linux installation gives you three options. The first is to partition your hard drive automatically. You can choose this option if you have no intention of dual booting your machine.

> **Caution** If you choose to automatic partition, all existing partitions will be erased and one root partition, one boot partition, and one swap partition will be created.

The second option is to use Disk Druid. Disk Druid is a graphical disk partitioning program specifically designed for Linux.

The final option is FDisk. FDisk is a program that will be familiar to some Windows users because it is used to partition Windows machines. However, it is rather complicated to use and does not provide a nice graphical interface. For our purposes, we will use Disk Druid.

> **Note** While it is certainly possible to dual boot a system with both Windows and Linux, it is much simpler just to have a Linux machine. Less-experienced readers would probably have an easier time using their entire machine for a single Linux partition, using the Automatic Partition option. Those readers who want to dual boot are advised to read the following paragraphs and any documentation that came with their Linux distribution carefully.

When you select Disk Druid, you will be taken to a screen displaying your current partitions. There are two courses of action you might take. First, if you are not going to dual boot your system (have more than one operating system on it), then it is probably best to highlight each partition, one by one, and delete it. Then you can start fresh. Then you will choose the New button, which will take you to a screen where you can set the parameters for this new drive. This is shown in Figure 2.9a.

![](img/12d790664598bbf390261087fbe55bbc_30_0.png)

**Figure 2.9A:** Setting up partitions.

> **Note** You also are taken to this screen if you choose to edit an existing partition.

If you are planning to dual boot with an operating system that is already installed—for example, should you wish to install Linux on your Windows machine and keep both operating systems—then you will not delete all the existing partitions. You will delete all partitions except for the one that contains Windows. This means that when we are done you will have one Windows partition and one Linux partition. The important point to remember is that you should leave the partition that has Windows completely untouched. The real question is, how do you know which partition has Windows? Linux and Disk Druid identify partitions differently than Windows does, but both Disk Druid and Windows list the size of the partition. The trick is to boot up your system before you begin the install and use My Computer to note the size of the partition you want to install Linux on. For example, consider Figure 2.9b.

![](img/12d790664598bbf390261087fbe55bbc_30_1.png)

**Figure 2.9B:** My Computer.

> **Note** This is one more reason why you were advised to read this entire chapter before attempting to perform the installation.

Here we see there is a single large partition of 13.6 gigabytes, and it is called the C drive. When you start the Linux install and get to Disk Druid, you will not see a drive labeled C, but you will see a drive that is about 56.6 gigabytes in size.
