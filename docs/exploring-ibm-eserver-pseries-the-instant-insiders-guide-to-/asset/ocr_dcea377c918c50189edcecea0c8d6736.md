# Application Programs and Operating Systems 199

that result from custom applications that precisely fit their needs. For customers who choose the custom software approach, pseries systems and the programming tools available for the AIX 5L operating system provide a very productive software development environment.

# Operating System

Few areas in information processing create more confusion and apprehension over the operating system layer of our software model, shown in Figure 3.3. The following discussion will help remove some of the mystery associated with the Advanced Interactive e (AIX) operating system using all pSeries and RS/6000 systems. The reader will become familiar with basic operating system terms such as “active processing” and “multiseruser,” and then move for a closer look at the AIX 5L operating system.

The description of AIX in this chapter provides AIX 5L for POWER Version 5 Release 1 (AIX 5L v5.1) and Release 2 (AIX 5L v5.2). AIX Version 4 (AIX 4.3) has been withdrawn from marketing and service will be discontinued December 31, 2003. Users of existing p servers can upgrade to AIX 5L, and only AIX 5L is available with new systems. All earlier AIX versions and releases have been withdrawn as newer versions have been announced. IBM supports two levels of AIX at any time, the latest level (version N) and the prior level (version N-1), at which time are AIX 5L v5.2 and v5.1.

# Introduction to Operating System Concepts

The operating system provides the necessary interface that allows the user and application programs to interact with pSeries systems. The user can interact directly with the operating system’s user interface to manage files on a disk, start application programs, print files, and so on. The operating system also performs tasks directly under the control of application programs without any user assistance. The application program initiates tasks by interacting with the operating system through the application program interface (API). This is simply a set of operating system commands that can be issued directly by the application program. The API simplifies the job of the application programmer, who need not get involved with the details of hardware interaction. Further, when an application program uses the API, it is shielded from changes in