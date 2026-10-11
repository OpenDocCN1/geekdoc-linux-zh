
## server services
The services that are made available for other computers across a network.

## shareware
The programs developed and provided at minimal cost to the end user. These programs are initially free but require payment after a period of time or usage.

## software
The programs stored on a storage device in a computer that provide a certain function when executed.

## Solaris
A version of UNIX developed by Sun Microsystems from AT&T source code.

## source code
The sets of organized instructions on how to function and perform tasks that define or constitute a program.

## SuSE
One of the most popular and prevalent distributions of Linux in Europe.

## system service
The additional functionality provided by a program that has been incorporated into and started as part of the operating system.

## tarball
A compressed archive of files that contains scripts that install Linux software to the correct locations on a computer system.

## total cost of ownership (TCO)
The full sum of all accumulated costs, over and above the simple purchase price of utilizing a product. It includes such sundries as training, maintenance, additional hardware, and downtime.

## UNIX
The first true multitasking, multiuser operating system developed by Ken Thompson and Dennis Ritchie, and from which Linux was originated.

## user interface
The interface the user sees and uses to interact with the operating system and application programs.

## workstation
A computer used to connect to services on a server.

## workstation services
The services that are used to access shared resources on a network server.

## X Windows
The core component of the GUI in Linux.

## Review Questions

1. A `____________` consists of a series of visual depictions of tasks known as icons, which the user can use to control the operating system.
   - a. command prompt
   - b. graphical user interface
   - c. Windows interface
   - d. visual user interface

2. `____________` is distributed free of charge, yet after a certain number of hours of usage or to gain certain features of the program, payment is required.
   - a. Shareware
   - b. Freeware
   - c. Artistic license software
   - d. GPL license software

3. Linux documentation is provided in the form of easy-to-read instructions known as `____________` documents, which are arranged by topic and are available to anyone.
   - a. Installfest
   - b. LUG
   - c. HOWTO
   - d. MANUAL

4. The UNIX operating system was rewritten in the `____________` programming language.
   - a. BSD
   - b. DEC
   - c. C
   - d. Solaris

5. The core component of the GUI in Linux is referred to as `____________` and can be obtained from the Internet.
   - a. X Windows
   - b. Linux X
   - c. Visual Linux
   - d. Solaris

6. True or false? A program is a file stored on your computer, whereas a process is that file in action, performing a certain task.

7. True or false? The Linux kernel is no longer under development.

8. True or false? When dealing with Linux version numbers, if the minor number is even, it is referred to as a developmental kernel, and if the minor number is odd, it is referred to as a production kernel.

9. True or false? Companies that run the UNIX operating system might find it difficult to migrate to Linux.

10. True or false? A Finnish student named Linus Torvalds first developed Linux in 1991.

11. The format and structure of source code follows certain rules defined by the `____________________` in which it was written.

12. A(n) `____________________` license ensures that the source code of the program is freely available, yet allows the original author of the source code some control over the changes made to it.

13. A(n) `______` is a software system that installs and maintains software.

14. Services that are used on the local computer are referred to as `____________________` services.

15. The most common method of Linux clustering is known as `____________________` clustering, which is easy to configure and well documented.

# Chapter 2

## Preparing for Linux Installation

After completing this chapter, you will be able to:

- Describe common types of hardware and their features
- Obtain the hardware and software information necessary to install Linux

A computer is composed of hardware, which is simply a collection of switches and circuits that require operating system software to function in a meaningful way. This chapter introduces you to the hardware and software terminology necessary to install a Linux system and discusses how to obtain this information from several sources.

## Understanding Hardware

Fundamental to the installation of Linux is an understanding of the computer’s various hardware components. This allows the user the ability to verify that any hardware detected automatically during installation was detected correctly and that the hardware meets any installation requirements. The hardware components necessary to understand prior to installing Linux include the following:

- Central processing units (CPUs)
- Physical memory
- Disk drives
- Mainboards and peripheral components
- Video adapter cards
- Keyboards and mice

## Central Processing Units (CPUs)

The core component of any computer is the **central processing unit** (CPU), also known as the microprocessor or processor; it is where the vast majority of all calculations and processing of information takes place. Processors are integrated circuit boards consisting of millions of transistors forming electrical pathways through which electricity is channeled. They consist of two main components: the **Arithmetic Logic Unit** (ALU) and the **Control Unit** (CU). The ALU is where all the mathematical calculations and logic-based operations are executed. The CU is where instruction code or commands are loaded and carried out, and often sends information to the Arithmetic Logic Unit for execution.

Processors can have their integral electronics arranged in different ways; this is referred to as the processor’s *architecture* or platform. Recall from Chapter 1, “Introduction to Linux,” that the Linux operating system is available for many different platforms, including SPARC (Scalable Processor Architecture), Alpha, and Intel. These different arrangements of electrical circuits can have a specific effect on the processor’s speed of executing certain types of instructions. Hence, processors are categorized based on the types of instructions they execute. The two main categories of processor architectures are **Complex Instruction Set Computers (CISC)** processors and **Reduced Instruction Set Computers** (RISC) processors. CISC processors normally execute more complex individual commands than RISC processors; however, because complex commands take longer to execute on a processor, RISC processors tend to be faster than CISC processors. The discussion is limited to the Intel processor architecture throughout the remainder of this book because Intel is the most common CISC processor available in homes and businesses around the world.

![](img/09bf13b782f71165e17bb3839040c96a_63_0.png)

The new Itanium processor from Intel is a RISC processor that has some CISC features. Because it differs in design from most RISC processors, its architecture is often called the Explicitly Parallel Instruction Computing (EPIC) architecture.

The speed at which a processor can execute commands is related to an internal time cycle referred to as **clock speed**. Similar to the way a quartz watch keeps time, the processor has a crystal that oscillates at a determinable frequency when current is passed through it. This is the drumbeat to which the processor keeps time and by which all actions are measured. The clock speed is measured in MegaHertz (MHz), or millions of cycles per second; a processor running at 200MHz has a clock speed or oscillation frequency of 200 million cycles per second. A processor might require one cycle to complete a command or might be superscalar, that is, able to complete more than one command in any given cycle. In either case, the faster the clock speed of the processor, the greater the number of commands it can execute in a given span of time.

![](img/09bf13b782f71165e17bb3839040c96a_63_1.png)

The clock speed of the processor in a computer is separate from and does not need to match the clock speed of other hardware components in the computer; in most cases, the clock speed of the processor is the fastest of any hardware component inside the computer.

Clock speed alone is not the sole determination of the speed at which a processor can work. The amount of information a processor can work with or process at any given time, measured in binary digits (bits), is also a major factor.

Hence, processors are also classified by how much information they can work with at a given time; the more information that can be moved or worked on at once, the faster data can be manipulated. A computer able to process 16 bits of information at a time is over twice as fast as one that can process 8 bits of information at a time; an 8-bit processor running at 800MHz
