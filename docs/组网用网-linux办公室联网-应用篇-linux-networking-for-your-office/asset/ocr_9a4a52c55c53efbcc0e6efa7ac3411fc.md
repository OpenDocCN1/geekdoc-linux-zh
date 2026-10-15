# Tip

The rs option is only useful for restricting printing using native Linux/UNIX printer sharing mechanisms, but the rg= option can be useful with Samba, too. You can restrict printer access just as described here, and as long as your Samba users log on with their own passwords, you can restrict printer access in this way.

# Printing to a Remote UNIX Printer from Linux

Because native UNIX/Linux-style printing involves UNIX or Linux clients, it’s important to understand the client side of such printer configuration. For the most part, this configuration works much as described in Chapter 14, “Preparing to Share a Printer,” p. 351. There are a few unique details, though.

# Using printtool to Configure Printing

After you start printtool and click Add to add a printer queue, printtool asks what type of printer you want to add. Select Remote Unix (lpd) Queue and, instead of the Edit Local Printer Entry dialog box, printtool presents the Edit Remote Unix (lpd) Queue Entry dialog box, shown in Figure 15.1.

![](bbox=[0.42, 0.78, 0.68, 0.92])

# FIGURE 15.1

You must specify a remote host and printer queue when creating a local queue for a remote UNIX or Linux printer.

The Edit Remote Unix (lpd) Queue Entry dialog box works very much like the Edit Local Printer Entry dialog box described in Chapter 14. The only difference is that you must enter the name of the remote computer and the queue name of the destination printer on that computer, rather than the name of the printer device file. Other fields, including the printer name, spool directory, file size limit, and the input filter, work precisely as they do with local printers.