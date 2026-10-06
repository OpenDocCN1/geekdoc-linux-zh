# CHAPTER 26 Printing 719

TIP Regular users can typically manage only their own print jobs—that is, user A cannot ordinarily go and delete a job submitted by user B from the print queue. The superuser, of course, control everybody's print jobs. Also, you should understand that the window of sending a job to the printer and being able to delete it is very narrow. Therefore, you may find that the lprm request fails because the command was issued too late. This will usually result in an error such as, "lprm: Unable to lprm job(s)". As root, you may, of course, use the dash (–) option to clear the print queue of all jobs at any time.

# Summary

This chapter discussed the Common UNIX Printing System (CUPS) and touched on simple printer management tasks, such as adding printers via the CUPS web interface and from the command line, managing printers, and printing jobs under Linux.

Usage of common client tools to manage print jobs in Linux was discussed, with examples provided. You also learned some about the configuration directives that are used in CUPS' main configuration file, cupsd.conf.

However, we only scratched the surface of the capabilities and features of CUPS. Fortunately, the software comes with extensive documentation, which is a highly recommended if you plan on using CUPS extensively to deploy and manage printers in your environment. The same documentation is also available online at the CUPS home page, www.cups.org.

Once you have printing set up on your Linux server, you'll find that it does its job quite nicely and lets you focus on other new and interesting challenges. Problems that arise with printing services typically stem from the physical printer itself (such as paper jams, running out of paper), user abuse, office politics and so on.