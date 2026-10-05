# 82 Chapter 6 • Printing and Print Sharing

entire printer queue, and even remove their job if they choose. Be sure to install a printer driver for Windows for the kind of printer you have installed, as the printer filter on Linux should just pass the data along to the printer.

To print from Linux to a Windows machine, the procedure is a bit different. RedHat allows you to via Server Message Block (SMB), and it takes care of the rest. The Windows machine finds the data and sends them off to the printer. In these cases, the print queue commands (see below) will probably not work, as Windows has its own protocol for handling the queues.

As you can see, it would be much easier and simpler for a printer to exist on a Linux server.

# 6.6 Managing Print Queues

Now that the printer is connected and working, people are going to try sending print data to it. At this point, it's time to put on the "print master" hat and get to work.

The print queues are FIFO (First In First Out) queues, so the first one in line gets to have access to the printer. If one job gets stuck, or the printer runs out of paper, the queue will begin to fill and you will be hounded by users desperately trying to find their printouts. Not to worry.

The commands you'll want to know about are the lpc, lprm, and lpq commands. The lpc command shows what's in the queue and gives you the current status of the printer, as lpc can figure that information out. Some printers will be able to tell lpc that they are out of paper, or that the connection is down, and these errors will show up in the lpq.

The lprm command will remove jobs from the queue. Only root and the person who submitted the print job can remove a job from the queue. If an accidental print job is 3 Mb in size and is currently tying the queue, it may be best to remove the job. As root, you can remove all the jobs owned by a particular user with the command lprm user.

The lpc command is the "lpc control." It can activate and deactivate queues and printers, rearrange jobs in the queue, and get a status of any printers listed in /etc/printcap to paraphrase the man manual.

Lpc can be run on the command line (lpc restart lpc) or run interactively, submitting many commands to various printers. Here's a list of some of the more important lpc commands: