
## 26.1 CUPS's command-line utilities and their origins

| Command | Function |
|---|--- |
| cups-config^a | Prints API, compiler, directory, and link information |
| cupsdconf^a | Configures CUPS through a KDE interface |
| cupsdisable^b | Stops printing on a printer or class |
| cupsenable^b | Restarts printing on a printer or class |
| lpinfo | Shows available devices or drivers |
| lpopions | Displays or sets printer options and defaults |
| lppasswd | Adds, changes, or deletes digest passwords |
| accept, reject | Accepts or rejects queue submissions |
| cancel | Cancels queue jobs |
| lp | Enqueues jobs for printing |
| lpadmin | Configures printers and classes |
| lpmove | Moves an existing print job to a new destination |
| lstat | Prints status information |
| lpc | Acts as a general printer-control program |
| lpq | Displays print queues |
| lpr | Enqueues jobs for printing |
| lpr | Cancels print jobs |

- a. Don't confuse these tools. **cups-config** is a command-line tool that's included with CUPS, and **cupsdconf** is a GUI tool in KDEPrint.
- b. These are also the **disable** and **enable** commands from System V, renamed.

## 26.3 PRINTING FROM DESKTOP ENVIRONMENTS

We've mentioned already that we encourage the use of the native CUPS GUI for administration rather than the use of add-ons for those designed for KDE. The native GUI is authoritative and also happens to be pretty good.

Another point to consider is portability. You may already be struggling with three different families of printing systems—why add to the confusion by several different administrative GUIs, too? If your CEO wants to print from his brand-new Macintosh, you may not know where to click to get to the latest Apple-designed GUI configuration widgets. But if you browse to localhost:631, you'll find yourself in unfamiliar territory.

Still, if all your users are on a particular desktop environment, you may decide to use that desktop's GUI to support them. For an example, KDEPrint, the overarching framework for printing under KDE.

KDEPrint provides its own tools for printing, administering print jobs, restarting print servers, and so on. Like other KDE tools, it has a KDE look and feel, allowing consistency for KDE users. (You've probably noticed that even KDE utility names have a distinctive look and feel. Someone once asked us if **ksh** was a KDE application.)

KDEPrint is not tied to CUPS. Although it can handle all of CUPS' features, it can be configured to work with everything from LPRng to a generic external program. For some reason you can't run CUPS (or worse, you have to switch back and forth between print systems), you can still use KDEPrint to manage printing. Be straightforward that CUPS is more capable than other printing systems, so if you have to downshift to an alternative printing system, some of KDEPrint's functionality may differ.

Here are the major components of KDEPrint that you should know about:

- *kprinter*, a GUI tool that submits print jobs
- The Add Printer wizard, which autodetects network printers (JetDirect, IPP, and SMB) and locally connected printers. The Add Printer wizard also lets you add and configure printers that are not autodetect.
- The Print Job Viewer, which moves and cancels print jobs and shows print job status information
- The KDEPrint Handbook, which documents the system. It's available through the KDE Help Center but can be annoyingly hard to find. An easier route is to invoke something like kprinter and click on Help. Another alternative is to use the KDE browser, konqueror, by running konqueror!/kdeprint.Print documentation can also be found at printing.kde.org.
- The Print Manager, which is the main GUI management tool for the printing system. It, too, can be a hard to find. You can poke around in your desktop menu, although the location in the menu tree varies from distribution to distribution. Another option is to run kcmshellprintmgr or konqueror!/manager.

The Add Printer wizard and the Print Job Manager are accessible through either kprinter or the KDE Print Manager, not to mention the URLs print:/manager and print/Konqueror.

Per-user information for KDEPrint is stored under ~/.kde. The files are human readable but designed to be changed through the Print Manager. Tinker with them at your peril.

## kprinter print documents

kprinter is a GUI replacement for lpr. It can be used from the command line without a GUI. For example, the command

```
$ kprinter --nodalog -5 -P rileyj4600 riley.py gillian.pdf zoe.prn
```

is equivalent to

```
$ lpr -5 -P rileyj4600 riley.py gillian.pdf zoe.prn
```

## Overview

Your users probably don't care; they want a GUI. Show them how drag files from the file manager or desktop into the kprinter dialog, they print the entire batch. Replace lpr for kprinter in their browser's Print dialog, and they'll have a GUI dialog. Teach them to click on their “Keep this dialog after opening” check box, and they won't experience a restart delay every time they print.

Take note of the “Print system currently in use” menu, evidence of KDEPrint offers-to-PDF and print-to-fax functions even if your network has no actual printers. The advanced options are also worth a look; you can queue your résumé for printing and specify that it is printed after your boss goes home.

## Konqueror and printing

Many web browsers recognize a set of special-purpose URLs that as gateways to idiosyncratic functionality. You've probably tried at least about:config and:mozilla in Firefox. Similarly, the family of URLs is Konqueror's secret gateway to the world of KDEPrint.

The print/URL shows all the possibilities. print/jobs monitors print jobs, and print/manager starts the Print Manager inside of Konqueror.

Even though you're not dealing directly with CUPS here, what makes all this relatively easy is the underlying fact that CUPS is a web server. Browsers know how to talk to web servers, so it's relatively easy to tweak them to add CUPS-specific printing features.

## 26.4 System V Printing

System V's printing software is the oldest and most primitive of the printing systems we cover—so old that it wasn't designed with network printing in mind. Most vendors that use it [missing text]... Solaris and HP use the system.

## Overview

Each printing "destination" has a name that consists of up to 14 alphanumeric characters and underscores. A destination is usually a printer, but it doesn't have to be. For example, a destination could be a file to which many users need to append text. Because printing systems are queuing systems, you can use lp to avoid a situation in which two people attempt to add to the file at the same time.

Every destination belongs to zero or more classes. A class is a group of destinations that all serve the same purpose in some way. For example, if a site has two printers in the same room, they might be combined into a class. Likewise, two printers with similar features (such as color, resolution, duplex, or speed) might be grouped into a class. Ipsched would direct output submitted to that class to whichever printer became available first. First class have the same restrictions as destination names.
