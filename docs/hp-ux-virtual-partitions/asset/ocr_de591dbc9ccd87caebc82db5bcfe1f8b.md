# # Software Distributor Example

![](bbox=[0.04, 0.13, 0.13, 0.23])

Software Distributor-HP-UX (I'll call this Software Distributor throughout the book; HP documentation typically uses SD-UX) is the program used in HP-UX 11i to perform all tasks related to software management. Software Distributor will be used in an example to install software on the same system we loaded our operating system on earlier in this chapter. Software Distributor is a standards-based way to perform software management. It conforms to the Portable Operating System Interface (POSIX) standard for packaging software and utilities related to software management. The Software Distributor product described in this section comes with your HP-UX system. Additional functionality can be obtained by buying the OpenView Software Distributor (SD-OV) product. SD-OV provides support for additional platforms, allows you to push software out to target systems, features centralized monitoring, and provides a job browser to assist in managing software on target systems. In this section, I won't cover SD-OV, but will make some comments about SD-OV functionality where appropriate.

Software Distributor can be invoked using the commands described in this section, by using SAM (covered in Chapter 11), or by installing software for the first time as described earlier in this chapter.

The following are the four phases of software installation performed with Software Distributor:

+   * Selection(1) - You can select the source and software you wish to load during this phase. In the upcoming example, the graphical user interface of Software Distributor is used and you'll see how easily you can select these.

+   * Analysis(2) - All kinds of checks are performed for you, including free disk space; dependencies; compatibility; mounted volumes; and others. One of the very useful outputs of this phase is the amount of space the software you wish to load will consume on each logical volume. This will be shown in the example.

+   * Load(3) - After you are satisfied with the analysis, you may proceed with loading the software.