
client you've added, this file may not exist. Whether or not this is the first client, the following command should do the job (you may need to adjust paths or filenames for the public key file):

```
$ cat ~/id_rsa.pub >> ~/.ssh/authorized_keys
```

+   7. Ensure that the keys file has the correct ownership and permissions. Permissions should be no more than 0600 (rw-------). If necessary, type `chmod 0600 ~/.ssh/authorized_keys` to set these permissions.

Once you've completed these steps, you should be able to log in from the client (**weger**) to the server (**mail**) without typing a password. Depending on the order in which the protocol levels are listed in your `/etc/ssh/ssh_config` file's `Protocol` line, though, you may have to specify that you want to use level 2 of the SSH protocol:

```
$ ssh -2 mail.pangaea.edu
```

## Criterias for Completion

To complete this task, you should have configured an SSH server to accept connections for ordinary users but not for **root**. You should also have set up an ordinary user's account to use SSH keys rather than a password for authentication, which can simplify logins from a specific client computer on which you already have an account.

# Task 6.10: Add a Printer Using CUPS

Although you might not think of printing as being particularly network related unless you use a networked printer, in Linux the printing tools are all network enabled. Traditionally, Linux has used the Berkeley Standard Distribution (BSD) Line Printer Daemon (LPD) printing system or compatible tools, such as LPing. Since 2000, though, most Linux distributions have switched to the Common Unix Printing System (CUPS), which uses entirely different, but still network-enabled, protocols. This task steps you through the process of adding a printer to CUPS. The next task describes the tools you can use to print and manage your CUPS printer queue.

> Unlike most Linux tools, CUPS is best administered through a GUI tool, which in the case of CUPS is a Web-based utility. Some distributions provide their own unique GUI printer configuration tools. You can use such distribution-specific tools if you like, but their details differ from those described here.

## Scenario

You've just obtained a new printer and you want to configure your computer to use it. Your printer is connected directly to your computer via a USB port. (CUPS can also handle printers connected via parallel or RS-232 serial ports and network printers, but a few configuration details differ for these types of printers.)

## Scope of Task

This task requires using the Web-based configuration tool that's part of CUPS. This tool guides you through the setup process, but a few steps provide the opportunity for slipsups that can cause problems.

## Duration

This task should take about half an hour to complete, or more if you run into problems. Unfortunately, each printer configuration task is unique, so you're as likely to encounter problems the 10th or 100th time you install a printer as the first time—although if you really do install a hundred unique printers, you'll have seen the most common types of problems and know how to work around them!

## Setup

This task requires that your computer be running CUPS, which most modern distributions do. You'll also need **root** access, both for installing printer drivers and for configuring CUPS via its Web interface. You may also need to restart the CUPS server: After you plug in a USB-based printer, you should turn the printer on and then restart the CUPS server as **root**. In most cases, you can do this via SysV startup scripts, as in **/etc/init.d/cups restart**. You must do this because CUPS looks for USB printers when it starts up, so if you add or turn on a printer after the system has booted, you must restart CUPS so that it can find and use the printer. For this reason, you should also ensure that any USB printer is powered on before you boot the computer. This step isn't necessary for printers that connect via a parallel or RS-232 serial port or for network printers (unless they're USB models that are managed by a computer that runs CUPS).

## Caveats

With the exception of restarting CUPS, as just described, and installing printer definitions, you won't be entering commands as **root**, which reduces the risks associated with this task. You will, however, be using the CUPS Web-based configuration tool as **root**, and you can damage your printer configuration if you make a mistake. In particular, you could delete or make unwanted changes to an existing working printer configuration.

## Procedure

This task requires you to perform two specific subtasks. First, you must obtain and install CUPS printer definitions (aka printer drivers). These may already be installed on your system, though, so perhaps just verifying that they're present will be sufficient. If in doubt, you can move on to the second subtask and go back to the first if you don’t see a suitable definition for your printer when you get to that point. The second subtask is actually using the CUPS Web interface to set up and test your printer.

## Obtaining CUPS Printer Definitions

Linux programs that print typically generate one of two types of files: plain text or PostScript. Linux printer queues typically recognize these two types of files, and perhaps some others such as common graphics file formats, and convert the printed file into a format that the printer can understand. Most commonly, the printer queue first converts non-PostScript to PostScript and then uses Ghostscript (`http://www.cs.wisc.edu/~ghost/`) to convert PostScript to a format that the printer can understand. (Of course, the Linux printing system bypasses Ghostscript when it uses a true PostScript printer.) To do all of this, you must install printer definitions, which tell the printer queue what PostScript options to use to convert PostScript into the desired format for your printer.

The basic version of CUPS ships with support for just a few printers, including raw queues that do no processing and a few models from Hewlett-Packard, Epson, and Okidata. If you use another printer, you should obtain extra CUPS printer definitions. These definitions may consist of PostScript Printer Definition (PPD) files, appropriate behind-the-scenes “glue” to tell CUPS how to use them, and possibly Ghostscript driver files. These printer definitions can be obtained from several sources:

- **Your Linux distribution** Many distributions ship extra printer definitions in a package called `cups-drivers` or something similar, so check your distribution for such a package. In truth, this package is likely to be the Foomatic or Gutenprint package under another name.

- **Foomatic** The Linux Printing Web site hosts a set of utilities and printer definitions known collectively as Foomatic (`http://www.linuxprinting.org/foomatic.html`). These provide many additional printer definitions for CUPS (as well as for other printing systems).

- **Gutenprint** The Gnu Image Manipulation Program (GIMP) is a major Linux bitmap graphics program that supports its own printer drivers. These in turn have been spinned off into a package called Gutenprint (formerly GIMP Print), which can be integrated with CUPS to provide additional printer options. Check `http://gutenprint.sourceforge.net` for more information.

- **Your printer manufacturer** A few printer manufacturers make Linux printer definitions available for their printers. Sometimes these are open source definitions that they’ve repackaged, but sometimes the manufacturers have written their own Ghostscript drivers or definitions. Check your printer manufacturer for details.

- **ESP Print Pro** Easy Software Products (ESP) is the company that first developed CUPS. Although CUPS is open source, ESP offers a variety of printer definitions for CUPS for a price. See `http://www.easysw.com/printpro/` for more details.

If you’re printing to one of the basic printers supported by the standard CUPS definitions, you may not need to add anything else. You might also find that your distribution has installed
