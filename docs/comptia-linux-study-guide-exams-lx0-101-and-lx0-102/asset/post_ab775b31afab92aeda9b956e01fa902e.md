
## Configuring Printing 309

directly to true PostScript printers, a program called Ghostscript converts the print job into a form that the system's printer can handle. The print queue, which is managed by software known as the Common Unix Printing System (CUPS), then sends the job to the printer. At various stages, administrators and users can examine the contents of a print queue and modify the queue. Understanding the tools used to create and manage print queues will help you to manage Linux printing.

## Conceptualizing the Linux Printing Architecture

Linux printing is built around the concept of a print queue. This is a sort of holding area where files are put to. A single computer can support many distinct print queues. But it's also possible to configure several queues in different ways to the same printer. For instance, you might use one queue to print single-sided and another for double-sided printing on a printer that supports duplex.

Users submit print jobs by using a program called lpr. Users can call this program directly, or they may another another call it it. In either case, lpr sends the print job into a specified queue. This queue corresponds to a directory on the hard disk, typically in a subdirectory of /var/spool/cups. The CUPS daemon runs in the background, waiting for print jobs to be submitted. The printing system accepts print jobs from lpr or from remote computers, monitors print queues, and serves as a sort of "traffic cop," directing print jobs in an orderly fashion from print queue to printers.

> The exam examines the CUPS printing system, which is the most common printing system on modern Linux systems. Older systems used the BSD Line Printer Daemon (LPD) or the similar LPRng printing system. Many of the CUPS tools are nowadays of the LPD tools. If you ever use a system that runs LPD or LPRng, you'll find that user commands such as lpr work in the way you expect, but configuring the printer must be done in a very different way.

![](img/35f616c7eba4e79e12bfd762129c5d27_363_0.png)

One important and unusual characteristic of Linux printing is that it's highly-networked. As noted, Linux printing can accept print jobs that originate from remote systems as well as from local ones. Local print jobs submitted via network protocols, although they don't normally use hardware, a computer with no network connection can. In addition to being a server for print jobs, CUPS can function as a client, printing jobs to other computers that run the same protocols.

Applications can query CUPS about a printer's capabilities—its paper sizes, whether it supports color, and so on. The older LPD and LPRng printing systems didn't support such bidirectional communication. Thus, support for these features still isn't universal; some programs make assumptions about a printer's capabilities or be told things that other programs can figure out by themselves.

## Understanding PostScript and Ghostscript

If you've configured printers under Windows, Mac OS, OS/2, or certain other OSs, you're probably familiar with the concept of a printer driver. In these OSs, the printer driver stands between the application and the printer queue. In Linux, the printer driver is part of Ghostscript (http://cs.wisc.edu/~ghost/), which exists as part of the printer queue. This relationship can be confusing at times, particularly because not all applications or printers need Ghostscript. Ghostscript serves as a way to translate PostScript, a common printer language, into forms that can be understood by many different printers. Understanding Ghostscript's capabilities, and how it fits into a printer queue, can be important for configuring printers.

## PostScript: The De Facto Linux Printer Language

PostScript printers became popular as accessories for Unix systems in the 1980s. Unix programs wer designed with Windows-style printer drivers in mind, Unix programs took advantage of laser printer features were typically written to produce PostScript output. As a result, PostScript developed into the de facto printing standard for Unix, and by inheritance, Linux. Where programs on Windows systems were built to interface with the printer driver, similar programs on Linux generate PostScript and send the result to the printer queue.

Some programs validate this standard. Commonly, many programs can produce raw text output. Some output sedem poses a major problem for modern printers, although some PostScript-only models choke on raw text. Other programs can produce PostScript or Printer Control Language (PCL) output for Hewlett-Packard Laser printers or their many imitators. Very few programs generate output that's directly accepted by other types.

The problem with PostScript is that it's a programming language, and it requires an interpreter. This is where Ghostscript fits.

## Ghostscript: A PostScript Translator

When it uses PostScript, the smart filter is usually involved. Ghostscript takes input and produces output in different formats, which are accepted by many printers. The smart filter can be configured to call Ghostscript with whatever parameters are appropriate to produce output for the queue. One of Ghostscript's drawbacks is that it produces large files. If this page is text, the size may be just a few kilobytes. If this page includes colors, the size could be much larger. In some sense, this is unimportant because these files will be stored on your hard disk only. They still have to get from the computer to the printer, though, this process can be slow. Also, some printers (particularly older printers) may require memory expansion to operate.

> For information about what printers are supported by Ghostscript, see the Ghostscript manual.

## Squeezing Ghostscript into the Queue

Printing to a non-PostScript printer in Linux requires fitting Ghostscript into the queue. This is generally done through the use of a smart filter. This is a program that's called as the printing process, the smart filter examines the file that's being, determines its type, and passes it through one or more additional programs before the printing software sends it to the printer.

CUPS ships with its set of smart filters, which it automatically calls when you tell the smart model you're using. CUPS provides a Web-based configuration tool. This system, or distribution-specific GUI tools, can make setting up a printer for CUPS straightforward.

The result of a typical Linux printer queue configuration is to treat any printer as if it were a PostScript printer. Applications that PostScript output print directly to the queue. The smart filter detects that the output is PostScript and runs it through Ghostscript. The smart filter can detect other types, such as plain-text and graphics files, and it can send them through appropriate programs instead of or in Ghostscript to create a reasonable printout.

If you have a printer that can process PostScript, the smart filter doesn't need to pass PostScript through Ghostscript. In this case, the smart filter passes PostScript directly to the printer, but it still sends other types through whatever processing is necessary to turn them into PostScript.

## Running a Printing System

Because Linux systems run as daemons, they must be started before they're useful. This task is normally handled automatically via startup scripts in /etc/rc.d, /etc/init.d, or /etc/rc.d (if d is a run number). Look for startup scripts that contain the string cups (or lpd or lpr for other systems) in Linux to learn what your system is running. If you're unsure if a printing system is currently active, use the ps utility to search for running processes by these names, as in

```
$ ps ax | grep cups
1896 ?       Ss       0:01 cupsd
```
