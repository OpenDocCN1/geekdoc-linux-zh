# Console Print Control

Older versions of Red Hat Linux used the 4.3BSD line-printer spooling system and its suite of text-based printing utilities. (Newer versions of these utilities, with the same names, are included with your Red Hat Linux CD-ROMs.) The commands support the launching of print jobs in the background (as a background process), printing of multiple documents, the capability to specify local and networked printers, control of the printers, and management of the queued documents waiting in the printer’s spool queue.

# Console-based Printer Configuration

The redhat-config-printer-tui tool offers all the convenience and features of Red Hat’s graphical printer configuration client without the need for a currently running X session. As you learned earlier, you run this as root:

```
# redhat-config-printer-tui
```

After you press Enter, the command's main dialog appears, as shown in Figure 12.12. You use the Tab and spacebar keys to navigate among and choose controls in this dialog.

![](bbox=[0.193, 0.463, 0.788, 0.782])

FIGURE 12.12 Use Red Hat’s redhat-config-printer-tui printer configuration utility to create or edit printers during console-based Linux sessions.

# Using Basic Print Commands

After configuring your printer, you can print from the Red Hat desktop using any printer-capable graphical clients. If you don’t use the desktop, but prefer to use or access your Red