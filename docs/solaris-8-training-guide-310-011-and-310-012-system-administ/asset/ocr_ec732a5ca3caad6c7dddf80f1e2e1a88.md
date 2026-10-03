# EXTENSIVE REVIEW AND SELF-TEST OPTIONS

At the end of each chapter, along with some summary elements, you will find a section called “Apply Your Knowledge” that gives you several different methods with which to test your understanding of the material and review what you have learned.

# CHAPTER SUMMARY

+   **KEY TERMS**
- OpenBoot
- Bootblock
- ufsboot
- OBP
- NVRAM
- PROM
- POST
- Device Tree
- Full Device Name
- Device Alias

This chapter provided a complete description of the OpenBoot environment; the PROM, the NVRAM, and the kernel.

In this chapter, I described how to access OpenBoot and the various commands available to test and provide information about the hardware.

I described the OpenBoot architecture. I explained how OpenBoot controls many of the hardware devices. Using the programmable user interface available in OpenBoot, the system administrator can set several parameters that control system hardware and peripherals.

Device names were also explained in this chapter. Throughout this book, I will be referring to various device names used in Solaris. It's important that you understand each one of them. I'll revisit this topic in Chapter 16, where devices and device drivers are covered in depth. Along with device names, I explained how to set temporary and permanent device aliases.

**Key Terms:** A list of key terms appears at the end of each chapter. These are terms that you should be sure to know and are comfortable defining and understanding when you go in to take the exam.

**Chapter Summary:** Before the “Apply Your Knowledge” section, you will find a chapter summary that wraps up the chapter and reviews what you should have learned.

**Exercises:** These activities provide an opportunity for you to master specific hands-on tasks. Our goal is to increase your proficiency with the product or technology. You must be able to conduct these tasks in order to pass the exam.

**Review Questions:** These short-answer questions allow you to quickly assess your comprehension of what you just read in the chapter.

# APPLY YOUR KNOWLEDGE

# Exercises

4.1 Software Package Administration

This exercise takes you through the task of installing, verifying, and removing software on a Solaris system using the command line.

Estimated Time: 20 minutes

+   1. List the software packages that are currently installed on your system by typing the following:
   `pkginfo`
2. Display a long-format listing of information for the SUNWman package installed on your system.
   `pkginfo -l SUNWman`
   What is listed for the status, install date, number of files, and number of blocks used by this package?
3. Remove the SUNWdoc package from your system with the following:
   `pkgrm SUNWdoc`
4. Use the following commands to verify the presence of SUNWdoc in the default spool area:

+   5. Observe the messages displayed, and verify that the package is installed in /var/spool/pkg.
6. Reinstall the SUNWdoc package from the spool area as follows:
   `pkgadd`
7. Select the SUNWdoc package when you are prompted, and the package will be reinstalled.
8. To remove the SUNWdoc package from the spool area, type the following:
   `pkgrm -s /var/spool/pkg`
9. You can now use the pkgchk command to check the completeness, pathname, file contents, and file attributes of the SUNWdoc package:
   `pkgchk SUNWdoc`

# Review Questions

+   1. Which of the following commands is used to show software package information?
   A. pkgadd
   B. pkgchk
   C. pkgparam
   D. pkginfo
2. Which of the following commands verifies the accuracy of a software package installation?
   A. pkgadd
   B. pkgchk