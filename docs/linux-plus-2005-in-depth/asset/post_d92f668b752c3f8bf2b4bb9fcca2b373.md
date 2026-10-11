
systems administration, yet are also well suited for those who will use or develop programs for Linux systems.

**Chapter 1, “Introduction to Linux”** introduces operating systems as well as the features, benefits, and uses of the Linux operating system. As well, this chapter discusses the history and development of Linux and Open Source Software.

**Chapter 2, “Preparing for Linux Installation”** introduces the various hardware components inside a computer, as well as methods that can be used to collect hardware and software information prior to installing the Linux operating system.

**Chapter 3, “Linux Installation and Usage”** walks through a typical Linux installation given the hardware and software information collected in the previous chapter. As well, this chapter describes how to interact with a Linux system via a terminal and enter basic commands into a Linux shell such as those used to obtain help and properly shutdown the system.

**Chapter 4, “Exploring Linux Filesystems”** outlines the Linux filesystem structure, and the types of files that can be found within it. As well, this chapter discusses commands that can be used to view and edit the content of those files.

**Chapter 5, “Linux Filesystem Management”** covers those commands which can be used to locate and manage files and directories on a Linux filesystem. Furthermore, this chapter outlines the different methods used to link files as well as how to interpret and set file and directory permissions.

**Chapter 6, “Linux Filesystem Administration”** discusses how to create, mount, and manage filesystems in Linux. This chapter also discusses the various filesystems available for Linux systems and the device files that are used to refer to the devices which may contain these filesystems.

**Chapter 7, “Advanced Installation”** introduces advanced hardware concepts and configurations that may prove useful when installing Linux. As well, this chapter discusses different methods that may be used to install Linux as well as common problems that may occur during installation, and their resolutions.

**Chapter 8, “Working with the BASH Shell”** covers the major features of the BASH shell including redirection, piping, variables, aliases, and environment files. Also, this chapter details the syntax of basic shell scripts.

**Chapter 9, “System Initialization and X Windows”** covers the different bootloaders that may be used to start the Linux kernel and dual-boot the Linux operating system with other operating systems such as Windows. This chapter also discusses how daemons are started during system initialization as well as how to start and stop them afterwards. Finally, this chapter discusses the structure of Linux Graphical User Interfaces as well as their configuration and management.

**Chapter 10**, “Managing Linux Processes” covers the different types of processes, as well as how to view their attributes, change their priority, and kill them. Furthermore, this chapter discusses how to schedule processes to occur in the future using various utilities.

**Chapter 11**, “Common Administrative Tasks” details three important areas of system administration: printer administration, log file administration, and user administration.

**Chapter 12**, “Compression, System Backup, and Software Installation” describes utilities that are commonly used to compress or back up files on a Linux filesystem. As well, this chapter discusses how to install software from source code as well as using the Red Hat Package Manager (RPM).

**Chapter 13**, “Troubleshooting and Performance” discusses the system maintenance cycle as well as good troubleshooting procedures for solving hardware and software problems. Also, this chapter outlines utilities that can be used to monitor and pinpoint the cause of performance problems, as well as how to patch and recompile the kernel to fix software, hardware, and performance problems.

**Chapter 14**, “Network Configuration” introduces networks, network utilities, and the TCP/IP protocol, as well as how to configure the TCP/IP protocol on a NIC or PPP interface. In addition, this chapter details the configuration of name resolution.

**Chapter 15**, “Configuring Network Services and Security” introduces commonly configured Linux network services and their configuration, as well as firewall and routing services. In addition, this chapter details the concepts and tools that may be used to secure a Linux computer locally and from across a network.

Additional information is also contained in the appendices at the rear of the book. **Appendix A** discusses the certification process with emphasis on the Linux+ certification and how the objective list for the Linux+ certification matches each chapter in the textbook. **Appendix B** is a copy of the GNU Public License. **Appendix C** explains how to find Linux resources on the Internet and lists some common resources by category. **Appendix D** contains the answers to the Review Questions at the end of each chapter.

## Features

To ensure a successful learning experience, this book includes the following pedagogical features:

- **Chapter Objectives**: Each chapter in this book begins with a detailed list of the concepts to be mastered within that chapter. This list provides you with a quick reference to the contents of that chapter, as well as a useful study aid.
- **Screenshots, Illustrations, and Tables**: Wherever applicable, screenshots and illustrations are used to aid you in the visualization of common installation, administration and management steps, theories, and concepts. In addition, many tables provide command options that may be used in combination with the specific command being discussed.
- **End-of-Chapter Material**: The end of each chapter includes the following features to reinforce the material covered in the chapter:
  - Chapter Summary: Gives a brief but complete summary of the chapter
  - Key Terms List: Lists all new terms and their definitions
  - Review Questions: Test your knowledge of the most important concepts covered in the chapter

## Text and Graphic Conventions

Wherever appropriate, additional information and exercises have been added to this book to help you better understand what is being discussed in the chapter. Icons throughout the text alert you to additional materials. The icons used in this textbook are as follows:

![](img/09bf13b782f71165e17bb3839040c96a_18_0.png)

TIP
Tips are included from the authors’ experiences that provide additional real-world insights into the topic being discussed.

![](img/09bf13b782f71165e17bb3839040c96a_18_1.png)

NOTE
Notes are used to present additional helpful material related to the subject being described.

# Chapter 1

## Introduction to Linux

After completing this chapter, you will be able to:

- Understand the purpose of an operating system
- Outline the key features of the Linux operating system
- Describe the origins of the Linux operating system
- Identify the characteristics of various Linux distributions and where to find them
- Explain the common uses of Linux in industry today

Linux technical expertise has quickly become significant in the computer workplace as more and more companies have switched to using Linux to meet their computing needs. Thus, it is important today to understand how Linux can be used, what benefits Linux offers to a company, and how Linux has developed and continues to develop. In the first half of this chapter, you learn about operating system terminology and features of the Linux operating system, as well as the history and development of Linux. Later in this chapter, you learn about the various types of Linux and situations in which Linux is used.

## Operating Systems

Every computer has two fundamental types of components: hardware and software. **Hardware** consists of the physical components inside a computer and are electrical in nature; they contain a series of circuits that are used to manipulate the flow of information. A computer can have many different pieces of hardware in it, including the following:

- A processor, which computes information (also known as the central processing unit or CPU)
- Physical memory, which stores information needed by the processor (also known as random access memory or RAM)
- Hard disk drives, which store most of the information that you use
- Floppy disk drives, which store information on floppy disks
- CD-ROM drives, which read information from CD-ROMs
- Sound cards, which provide sound to external speakers
- Video cards, which display results to the computer monitor
- Circuit boards, which hold and provide electrical connections between various hardware components (also known as mainboards or motherboards)

**Software**, on the other hand, refers to the sets of instructions or **programs** that understand how to use the hardware of the computer in a meaningful way; they allow different hardware to interact with, as well as manipulate data (or files) commonly used by programs. When a bank teller types information into the computer behind the counter at a bank, for example, that bank teller is using a program that understands what to do with your bank records. Programs and data are usually stored on hardware media, such as CD-ROMs, hard disks, or floppy disks, although they can also be stored on other media or even embedded in computer chips. These programs are loaded into various parts of your computer hardware (such as your computer's memory and processor) when you first turn your computer on, and when you start additional software, such as word processors or **Internet** browsers. After a program is executed on your computer's hardware, that program is referred to as a **process**. Thus, the difference
