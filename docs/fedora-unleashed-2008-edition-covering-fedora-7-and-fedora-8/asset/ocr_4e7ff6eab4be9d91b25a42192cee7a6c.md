# ## CHAPTER 8
## Printing with Fedora



+   - Overview of Fedora Printing
+   - Configuring and Managing Print Services
+   - Creating and Configuring Local Printers
+   - Reference

From the word go, Fedora provides support for a huge range of printers from many different manufacturers. This chapter looks at how to get your printer connected and talking to Fedora, as well as at the software that Fedora uses to manage printers and print jobs.

In keeping with most of the other Linux distributions, Fedora uses CUPS (Common Unix Printing System) to handle printers. Other systems are supported, such as LPRng, but you do not have access to some of the graphical management tools from within Fedora.

# The Internet Printing Protocol

CUPS supports the Internet Printing Protocol, known as IPP, and offers a number of unique features, such as network printer directory (printer browsing) services, support for encryption, and support for PostScript Printer Description (.ppd) files.

According to the Internet Engineering Task Force (IETF), IPP grew out of a 1996 proposal by Novell to create a printing protocol for use over the Internet.

Since then, the system has been developed and has matured into a stable print system for use on a variety of Linux and Unix-like operating platforms.

# ## Overview of Fedora Printing

Fedora's print filter system is the main engine that enables the printing of many types of documents. The heart of that engine is the GNU GPL version of Aladdin's Ghostscript interpreter, the gs client. The system administrator's printer configuration tool is the system-config-printer client.