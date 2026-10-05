# The Generic Linux Configuration 113

The generic.m4 file contains six m4 commands after the copyright notice. The first is a VERSIONED macro that can be ignored. The first significant command is a define command.

# Defining .forward Path

The first define command assigns a value to the CONFORWARD_PATH variable. This holds a colon-separated list of paths that Sendmail searches when looking for a .forward file. (Chapter 2, “Understanding E-Mail Architecture,” explains the purpose of the .forward file.

The default value of CONFORWARD_PATH is $/. Sendmail:Sw:$z/.forward, where $z is the recipient's directory and $sw is a valid name for that host. (See Appendix C for a full list of Sendmail variables, including $z and $sw) If the recipient's directory is /home/jill and the hostname is gull, the path is interpreted as /home/jill/.forward.gull:/home/jill/.forward.

The first define in Listing 5 increases the complexity of the .forward path. It retains the two paths from the search list and inserts in front of them the value $z/.forward.Sw+$z/.forward-$h. The $z and $sw variables serve the same purpose as .forward. The $h variable contains the detail that user+detail addressing syntax is used and procmail is used as the local mailer. Now procmail is being used as the local mailer because we use the local_procmail feature in the linux.m4 OSTYPE file. Given this configuration, local mail on a host named egress addressed to craig+sysex would prefer the following .forward search path to the standard path: /home/craig/.forward+sysex:/home/craig/.forward+sysex.

![](bbox=[0.927, 0.273, 0.98, 0.373])

# The +detail Syntax

The +detail syntax is an adaptation of the mailbox syntax in the Cyrus mailers. The Cyrus mailers allow mail to be addressed to a specific mailbox. In a Cyrus address, the detail is a mailbox name. Thus mail addressed to rebecca+in is placed in a mailbox inbox owned by the user rebecca.

The problem with this is neither Sendmail nor Linux uses a mailbox architecture. Sendmail writes to a single spool file for each user, and Linux user mail agents read from a single spool file for each user. Thus, bound for user rebecca is written to and read from the file /var/spool/mail1/rebecca. Mailboxes exist on Linux systems, but they exist because the user mail agent reads the mail from the single spool file and routes it to different mailboxes based on some filtering defined inside the user mail agent.