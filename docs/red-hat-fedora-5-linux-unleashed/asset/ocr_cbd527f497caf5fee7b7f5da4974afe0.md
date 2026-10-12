# CHAPTER 7
# Managing Software

+   **IN THIS CHAPTER**
+   * Using RPM for Software Management
+   * Alternatives for Software Management
+   * Compiling Software from Source
+   * Reference

In this chapter we will look at the options you have to manage your software in Fedora. If you are used to a Windows environment where you are reliant on visiting several different vendor websites to download updates, you are in for a shock! Updating a full Fedora installation, including all the application software, is as easy as typing **yum update** at the command line. You will discover just how easy it is to install and even remove various software packages.

Fedora provides a variety of tools for system resource management. The following sections introduce the RPM Package Manager (RPM), along with command-line and graphical software management tools. You will also learn about monitoring and managing memory and disk storage on your system.

# ## Using RPM for Software Management

RPM was derived (in part) from early Linux package management software—named RPP, PMS, and PM—that were written in Perl. RPM was first used with Red Hat Linux 2.0 in late 1995, and then rewritten in C for the Red Hat Linux 3.0.3 (Picasso) release in 1996. Since then, the **rpm** command has been the prime feature of Red Hat's unique software management system, which is based on the concept of pristine sources, or the capability to use a single, initial archive of a program's source code to build packages for different systems and to track versions. With the release of Red Hat 8.0 (Psyche) in 2002, Red Hat offered a slightly updated graphical management interface for its venerable RPM application.