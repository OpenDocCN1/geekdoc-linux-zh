
## # The Printer Command Family

There are a number of commands you have to deal with when managing your printer(s) under Linux. It can get confusing trying to keep them straight, so I laid them out for you here in Table 8.2. Each has a specific function in the greater scheme of print job and printer management.

**Table 8.2 Print-related commands in Linux.**

| Command | Purpose |
| :--- | :--- |
| **lpc** | Printer control program |
| **lpd** | Print daemon |
| **lpq** | Print spool control program |
| **lpr** | The print spooler |
| **lprm** | Print job removal |
| **pac** | Generates print accounting reports |

### The Printer Control Program

You use the **lpc** command in the format:

```
lpc command value
```

The available commands are listed in Table 8.3.

**Table 8.3 Available commands for *lpc*.**

| Command | Purpose | Values |
| :--- | :--- | :--- |
| **?** | Prints help information about a command. | **lpc** command |
| **abort** | Kills the active print daemon that manages this printer's spool, then disables printing to this printer. | Either **all** for every printer, or the printer name for the specific printer |
| **clean** | Removes any unprintable files from the printer's queue. Good for cleaning out temporary information. | Either **all** for every printer, or the printer name for the specific printer |
| **disable** | Turns the printer's queue off so it will not pull any more jobs from the spool. | Either **all** for every printer, or the printer name for the specific printer |
| **down** | Turns the printer's queue off and does not allow new jobs to be spooled. | Either **all** for every printer, or the printer name for the specific printer; plus a brief message explaining why the printer is down |
| **enable** | Turns the printer's queue on so new jobs can be spooled. | Either **all** for every printer, or the printer name for the specific printer |
| **help** | Prints help information about a command. | **lpc** command |
| **restart** | Shuts down the current **lpd** session and opens a new one. | Either **all** for every printer, or the printer name for the specific printer |
| **start** | Turns printing on for the printer and starts a print daemon for its spool. | Either **all** for every printer, or the printer name for the specific printer |
| **status** | Gives the current status of the spooling daemon and queue. | Either **all** for every printer, or the printer name for the specific printer |
| **stop** | Shuts off the spooling daemon when it has no more jobs to handle and then disables printing. | Either **all** for every printer, or the printer name for the specific printer |
| **topq** | Moves the specified jobs to the top of the queue. | The printer name, the job number, then the user |
| **up** | Turns on the printer's queue and allow jobs to be spooled. | Either **all** for every printer, or the printer name for the specific printer |

### The Print Daemon

You use **lpd** in the format:

```
lpd flag port
```

Believe it or not, there is only one flag available for **lpd**. It is not included by default because you may not want to use the flag at all. This flag is **-l**, which logs valid network jobs as they arrive to be spooled. If you want, you can also have **lpd** listen on a nonstandard port for network print jobs.

### The Print Spool Controller

You use **lpq** in the format:

```
lpq flag job user
```

There are two flags available with this command:

- **-l** — Prints a single line of information about each job.
- **-Printer** — Specifies exactly which printer you are interested in.

There can be more than one print job listed, separated by spaces.

### The Print Job Remover

You use the **lprm** command in the format:

```
lprm flag jobs user
```

Once again, there are only two available flags for this command:

- **--** (Yes, a dash.) Removes all jobs from this user.
- **-Printer** — Specifies exactly which printer you are interested in.

### The Report Generator

You use the **pac** command in the format:

```
pac flags name
```

The flags available for **pac** are listed in Table 8.4. You only include the *name* value if you want to generate a report for just one user.

The output from this command goes into /var/account/.

**Table 8.4 Flags available for the *pac* command.**

| Flag | Purpose |
| :--- | :--- |
| **-Printer** | The specific printer you want to generate a report for. |
| **-c** | Sorts the output by cost instead of alphabetically by name. |
| **-m** | Groups all charges together for a user, regardless of what host they printed from. |
| **-p**price | Cost of a page in dollars. Overrides the value in /etc/printcap. |
| **-r** | Sorts in reverse order. |
| **-s** | Includes a summary of the account information. |

## ## The Linux Printing Process

In a Unix system or Unix variant such as Linux, a file goes through a particular process when you try to print it. Understanding this process helps you both configure and administer it. What follows is an example of what happens to a file when you print it under Linux.

Suppose that you have the file ~/picture.jpg. You know that an inkjet printer named ij is installed on the network, so you type `"pr -Pij ~/picture.jpg"` to print the file, having read “Printing A File” in the Immediate Solutions section of this chapter.

The image file is now sent to the spool defined in /etc/printcap—the print services configuration file. In this case, because the printer is not local to the machine, its spool is on the NFS mount /share (see Chapter 17 for more information on NFS) in the directory /share/printers/spool/ij.

Whenever a file arrives in the print queue, the system notifies the print daemon, **lpd**, which spawns off a child **lpd** to handle the queue if it was inactive when this job arrived. Because the image file was sent directly into a queue that is also NFS-mounted on the print server, and because this machine points within its own printcap file to the same print spool file, `lpd` waits for data to arrive in /share/printers/spool/ij. When your print job enters the spool, it either waits its turn in the queue, if other jobs are already printing and waiting, or gets sent to the printer directly, if nothing else is waiting.

However, `~/picture.jpg` is not a raw ASCII text file. It is an image file—a JPEG (Joint Photographic Experts Group format) file, to be precise. Fortunately, you had the foresight to realize that people were pretty likely to print more than just raw text to a color printer. With the APSfilter program installed—as discussed in “Setting Up Popular Print Filters,” in the Immediate Solutions section—your machine knows how to print a JPEG file. The image is converted and sent as a PostScript file to the printer.

## ## Linux Printing Issues

With Linux, as with any other operating system, you need to consider the following items when setting up your printers and when printing:

- You cannot pass print jobs between Linux and another operating system without special tools. After your printers are set up and running, see Chapter 18 for information on how to share print jobs between Linux and other operating systems.
- Printing to a local printer and printing to a network printer are two entirely separate configuration issues. You need to configure network printers specially.
- Printing anything other than raw ASCII text files requires special filters to process the data and convert it into PostScript format. PostScript is a print-formatting language first developed by Adobe. It is more of a programming language than a markup language—more like C than HTML. If your printer is not PostScript-capable, you may be relegated to using only ASCII text documents.
- If you do not have print filters installed to do the conversion for you, there is a program called GhostScript that can handle this.

## ## Introduction To GhostScript

When the Unix community needed a program that could handle PostScript format files, the GNU (Gnu’s Not Unix, at www.gnu.org) folks, along with Aladdin Enterprises (www.aladdin.com), stepped in and gave us GhostScript, which actually is a suite of tools.

The GhostScript program, gs, is a PostScript and PDF (Adobe’s Portable Document Format) interpreter. You can use this tool to view or print the contents of a
