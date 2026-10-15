# CHAPTER 12

# Printing with Ubuntu

From the word go, Ubuntu provides support for a huge range of printers from many different manufacturers. In this chapter, we look at how to get your printer connected and talking to Ubuntu and examine the software that Ubuntu uses to manage printers and print jobs.

In keeping with most of the other Linux distributions, Ubuntu uses CUPS (Common UNIX Printing System) to handle printers. Other systems are supported, such as LPRng, but you will not have access to some of the graphical management tools from within Ubuntu.

# The Internet Printing Protocol (IPP)

CUPS supports the Internet Printing Protocol, known as IPP, and offers a number of unique features, such as network printer directory (printer browsing) services, support for encryption, and support for PostScript Printer Description (.ppd) files.

According to the Internet Engineering Task Force (IETF), IPP grew out of a 1996 proposal by Novell to create a printing protocol for use over the Internet. Since then, the system has been developed and has matured into a stable print system for use on a variety of Linux and UNIX-like operating platforms.

# Overview of Ubuntu Printing

Ubuntu's print filter system is the main engine that enables the printing of many types of documents. The heart of that engine is the GNU GPL version of Aladdin's Ghostscript interpreter, the gs client. The system administrator's printer configuration tool is the gnome-cups-manager client.

# IN THIS CHAPTER

+   - Overview of Ubuntu Printing
+   - Configuring and Managing Print Services
+   - Creating and Configuring Local Printers
+   - Reference