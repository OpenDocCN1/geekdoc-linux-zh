```
$ cat file1.ps | lpr -P nw1ps
```

# # Switching Printing Service to CUPS

Beginning with the Red Hat Linux 7.3 distribution, the Common UNIX Printing Service (CUPS) is offered as an alternative to LPng. CUPS is based on the Internet Printing Protocol, whose purpose is to standardize printing service across all UNIX platforms (including Linux).

CUPS supports many of the same interfaces that are in LPng. So if you decide to replace LPng with CUPS, you can still use the following commands to print and manage documents:

+   * cancel or lprm — Cancels a print job.
+   * lp or lpr — Prints a document.
+   * lpc — Controls operation of the print service.
+   * lpq — Views print queues.
+   * lpstat — Views the status of the print service.

In other words, after you replace the underlying print service, you and the others who print on your Red Hat Linux system should still be able to use the print service as you did before. (Most of these basic printing commands are described later in this chapter.)

# # Using Red Hat Printer Switcher to change to CUPS

You can switch to CUPS easily by using the alternatives feature, which is also new to Red Hat Linux 7.3. The alternatives system links the printing commands into the new service via the Red Hat Printer Switcher window. Then, all you have to do is start up the CUPS daemon instead of the LPng daemon for CUPS to take over. (Chapter 10 describes using the alternatives system to switch to CUPS. It consists mainly of switching services, stopping the 1pd daemon, and starting the cupsd daemon.)

Although switching LPng for CUPS isn't too difficult, you still need to do some work to configure CUPS. The following sections provide an overview of configuring CUPS as your printing service.

# # Using Web-based CUPS administration

Once the CUPS service is running you can administer CUPS from your Web browser. CUPS listens on port 631 to provide access to the CUPS Web-based administrative interface. On the local computer, type the following into your Web browser's location box:

```
http://localhost:631/admin
```

You will be prompted for a valid login name and password. Type in the root login name and the root user's password. A screen that is similar to the one shown in Figure 17-2 appears: