The first part of this chapter assumes that you have a printer connected to a parrel port. It is possible to use FreeBSD with printers that connect to the serial port. However, serial printing is very slow, and is obsolete. Only ancient printers use serial printing. In addition, this chapter assumes that you know whether your printer understands PostScript or not. See your printer's documentation to find out.

# # How lpd, the Print Spooler, and the Print Queue Function in FreeBSD

lpd is the line printer daemon. This software runs in the background and waits for print requests. When it receives them, it sorts the requests through any relevant filters, converts the data to a different format if necessary, and sends the requests to the print queue.

The *print queue* is an area on the hard disk where print data is stored that is waiting to be sent to the printer. Each printer connected to the system has its own separate queue and spool area. The spool area holds the data until it can be sent to the printer. It can hold multiple jobs from the same or different users.

When a user submits a job to be printed, it is put in the queue. *The spooler* then spools the job to the printer when the printer is available. Jobs can have different priorities that determine in which order they will get printed. The spooler has several advantages over simply printing directly to the printer, as DOS used to do:

+   *   It allows the printer to be shared by multiple users because data can be queued up to be printed, and the program that sent the data can then forget about it.
+   *   It allows for background printing. Once again, the program that requests a print job can send the job and then forget about it. This means you don't have to wait for the program to finish printing before you can continue working in it. It also means you can shut down the program after the job has been submitted to the queue without losing the print job.
+   *   It allows for some degree of fault tolerance. If the printer has to be reset, you will not lose the jobs that are in the queue and have to resubmit them. After the printer is back online, the remaining jobs in the queue should print normally, as if nothing happened.

Generally, the spool directories are located in `/var/spool`. The first printer on the system will normally spool to `/var/spool/lpd` or `/var/spool/output/lpd`. However, this can be changed by editing a configuration file, and we will look at how to do this later in the chapter.