
# 3

# Application Programs and Operating Systems

## Types of Software—A Conceptual Model

The term “software” is analogous to the term “publication.” Newspapers are a category of publication. Annual reports, novels, and Who’s directories are some other categories of publications. These different categories fill very different needs. The same situation exists with software. There are three basic categories, or software layers—the application program layer, the operating system layer, and the device driver layer, as shown in Figure 3.1. Each software layer performs a completely different job, but all three work closely together to perform useful work for the user.

## Application Programs

The top software layer in the model is the application program layer (highlighted in Figure 3.2). The programs in this layer “apply” systems to a specific task (computer-aided design, word processing, counting, etc.) and thus are called “application” programs. They actually perform the task for which the user purchased the computer while the other two layers play important support roles. A single PSeries system might run one application program at a time, or it might run many application programs simultaneously.

![](img/29c52a1767a1e621ce6343faa9399737_214_0.png)

**Figure 3.1.** Conceptual software model of the pSeries system’s basic software structure. The three layers of the software model work together to perform useful work for the user.

![](img/29c52a1767a1e621ce6343faa9399737_214_1.png)

**Figure 3.2.** The application program software layer of the software model. This is the application program that defines the particular task the computer is performing for the user.

The arrows in the figure indicate how users “see” the computer system. The user usually interacts with the application program layer and (less frequently) the operating system layer. By working closely with the other software layers, the application program processes the various keystrokes by the user and responds information on the computer’s display or some other output device.

As we will later in the chapter, many programs for other computers run UNIX operating systems (i.e., open systems) can be migrated to the PSeries and the AIX 5 operating system by the software developer. This allows PSeries users to capitalize on many applications originally developed for other systems. There is an application program to help users with just about anything they wish to do. Examples of common functions that application programs provide include e-business (Web serving, secure on-line shopping, customer support, etc.), accounting, statistical analysis, database, banking, telecommunications, and computer-aided design.

The application software layer is more familiar to the user because it provides a business function and is the layer with which he or she interfaces. However, the operating system and device driver layers are equally vital, they provide the framework or “infrastructure” that controls the hardware (PSSeries system and attached I/O devices) and allow many independent applications to execute. The interactions between the application and operating system layers, as well as between the operating system and device driver layers, are very complex. Although it is important for programmers and administrators to understand these layers in detail, it is sufficient for most readers to think of the operating system and device drivers as a single entity that supports application software on one side and system hardware on the other. The next two sections give a high-level description of the specific roles of the operating system and device driver layers.

## Operating Systems

The operating system (highlighted in Figure 3.3) must manage the hardware resources of the computer system and perform tasks under the control of application program(s) and keyboard/mouse commands issued by the user. The application program can rely on the operating system to perform many of the detailed housekeeping tasks associated with the internal workings of the computer. Thus, the operating system is said to provide the environment in which application programs execute. The operating system layer also accepts commands directly from the user; for instance, it can copy files, change a user's password, and so on.

Although not distributed by IBM, the Linux operating system is supported on pSeries servers. At the time of this writing, Linux distributions from SuSE are supported on most pSeries servers, including LPARs. Distributions from Red Hat and Turbo Linux are available for selected pSeries and RS/6000 systems. This chapter includes a section on Linux support for pSeries servers. For links to additional information about Linux, see the companion Web site for this book (www.maxpress.com).

## Device Drivers

The third and final layer of software in our software model is the device driver layer (highlighted in Figure 3.4). “Device driver” is a fancy term for a set of highly specialized programs, usually written by the manufacturer of hardware. These specialized programs reside in pSeries main memory or in memory provided right on the adapters they control.

Unlike application programs or operating systems, device drivers are only used by the users and exist only to help application programs and the operating system elements under their tasks. They interact directly with computer hardware elements under the control of the operating system or application program layers.

![](img/29c52a1767a1e621ce6343faa9399737_217_0.png)

**Figure 3.4.** The device driver software layer of the software model. Device drivers directly control the hardware elements of pSeries systems and shield application programs and operating systems from hardware details.

Device drivers also help shield applications from the hardware specifics of computers, allowing for evolutionary product improvements without sacrificing application program compatibility. Each hardware feature (device or adapter card) requires a device driver program. The device drivers for pSeries features (discussed in Chapter 2) are included with AIX 5L.

## pSeries Software Compatibility

Computer systems that run the UNIX operating system have been in existence for many years. As a result, a wide variety of application programs have been developed for UNIX. The flexibility afforded by virtue of this large and diverse software allowed computers running to fill many different needs. Of course, this sea of available application programs did not exist when the original UNIX operating system was first announced. It took the independent efforts of a great many people over many years to develop the large number of application programs (called an application software base) that exist today.

## Why Compatibility Is Important

In order to capitalize on that software base, application software compatibility was a primary objective in the design of the AIX 5L operating system. That is, most application programs written for UNIX operating systems can easily be migrated to the pSeries system and the AIX 5L operating system.

It is important to understand that the three layers in our software model, compatibility with the programs layer is most important. Why? First of all, application programs typically represent the lion's share of a user's investment. Further, being forced to abandon an application program because of incompatibilities may make users throw away data and experience they have accumulated—both of which can be substantial. Some users have developed custom application programs at considerable cost in development time and money. Incompatibility at application program level would render these programs virtually useless. Last, and perhaps most important, application compatibility allows pSeries system users to choose from the thousands of application programs that were originally developed for the operating system.

What about the operating system and device driver layers? The ability to run earlier operating system software is not important for several reasons. Operating systems typically represent only a small fraction of the user's investment; they can be upgraded without changing the user's view of the computer system. Further, a new operating system is usually necessary to allow users to access new features of the computer system not considered by the programmers of the old operating system. Of course, one of the purposes of the device driver layer is to allow the computer hardware to change without affecting compatibility with the operating system and application programs. This is done by changing the way a device driver interacts with hardware without changing the way the driver interacts with the operating system or application programs. The user is supplied with new device drivers to support pSeries hardware.

## Inside pSeries Compatibility

To understand pSeries compatibility, you must understand a little about how application programs are written. First, a programmer writes an application program's instructions or code using a programming language (e.g., C++, FORTRAN, etc.). A programming language is basically a library of computer instructions from which a programmer may choose to write programs. The list of programming language instructions that make an application program is called the program's source code. In order to run the application program on a computer, the source-code instructions must be converted into instructions a computer can understand. This process is compiling the program. When the source code is compiled, the result is called object code and can be directly executed by the computer hardware.

The most important thing to understand about pSeries compatibility is that any model of the pSeries family is object-code-compatible with all other pSeries models and earlier RS/6000 systems. That is, you can take the object code for an application program compiled on an
