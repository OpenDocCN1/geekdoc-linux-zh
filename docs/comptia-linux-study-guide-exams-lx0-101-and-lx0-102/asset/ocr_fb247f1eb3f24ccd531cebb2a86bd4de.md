# Configuring Printing 309

directly to true PostScript printers, a program called Ghostscript converts the print job into a form that the system's printer can handle. The print queue, which is managed by software known as the Common Unix Printing System (CUPS), then sends the job to the printer. At various stages, administrators and users can examine the contents of a print queue and modify the queue. Understanding the tools used to create and manage print queues will help you to manage Linux printing.

# Conceptualizing the Linux Printing Architecture

Linux printing is built around the concept of a print queue. This is a sort of holding area where files are put to. A single computer can support many distinct print queues. But it's also possible to configure several queues in different ways to the same printer. For instance, you might use one queue to print single-sided and another for double-sided printing on a printer that supports duplex.

Users submit print jobs by using a program called lpr. Users can call this program directly, or they may another another call it. In either case, lpr sends the print job into a specified queue. This queue corresponds to a directory on the hard disk, typically in a subdirectory of /var/spool/cups. The CUPS daemon runs in the background, waiting for print jobs to be submitted. The printing system accepts print jobs from lpr or from remote computers, monitors print queues, and serves as a sort of "traffic cop," directing print jobs in an orderly fashion from print queue to printers.

> The exam examines the CUPS printing system, which is the most common printing system on modern Linux systems. Older systems used the BSD Line Printer Daemon (LPD) or the similar LPRng printing system. Many of the CUPS tools are nowadays of the LPD tools. If you ever use a system that runs LPD or LPRng, you'll find that user commands such as lpr work in the way you expect, but configuring the printer must be done in a very different way.

![](bbox=[0.143, 0.538, 0.223, 0.584])

One important and unusual characteristic of Linux printing is that it's highly-networked. As noted, Linux printing can accept print jobs that originate from remote systems as well as from local ones. Local print jobs submitted via network protocols, although they don't normally use hardware, a computer with no network connection can. In addition to being a server for print jobs, CUPS can function as a client, printing jobs to other computers that run the same protocols.

Applications can query CUPS about a printer's capabilities—its paper sizes, whether it supports color, and so on. The older LPD and LPRng printing systems didn't support such bidirectional communication. Thus, support for these features still isn't universal; some programs make assumptions about a printer's capabilities or be told things that other programs can figure out by themselves.