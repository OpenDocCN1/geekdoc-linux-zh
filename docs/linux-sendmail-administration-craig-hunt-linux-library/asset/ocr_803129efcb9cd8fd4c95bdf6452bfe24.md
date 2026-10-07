# The Generic Linux Configuration

The generic.m4 file contains m4 commands from the copyright notice. The first is a VERSIONID macro that can be ignored. The first significant command is a define $ command.

# Defining the .forward Path

The first define command assigns a value to the confFORWARD_PATH variable. This variable holds a colon-separated list of the paths that Sendmail searches when looking for a .forward file. (Chapter 2, “Understanding E-Mail Architecture,” explains the purpose of the .forward file.

The default value of confFORWARD_PATH is $z/$w:$z/.forward, where $z is the recipient's home directory and $w is a valid significant name for this. (See Appendix C for a full list of the Sendmail variables, including $z and $w.) If the recipient's directory is /home/jill and the hostname is guill, the path is interpreted as /home/jill/.forward.guill:/home/jill/.forward.

The first define in Listing 5.3 increases the complexity of the .forward path list. It retains the two paths from the default search list and in front of them the .forward.sw+$h:$z/.forward+$h. The $z and $w variables serve the same purpose as before. The $h variable contains the detail value when the user+detail syntax is used and procmail as the local mailer. We know procmail is being used by the local mailer because we use the local_procmail file on a host named egret addressed to craig+sysex by this configuration, local mail on a host named egret would prepend the following. forward search path to the standard path: /home/craig/.forward.egret+sysex:/home/craig/.forward+sysex.

# The +detail Syntax

**+detail syntax is an adaptation of the mailbox syntax used in the Cyrus mailers. The Cyrus mailers allow mail to be addressed to a specific mailbox. In a Cyrus address, the detail is a mailbox name. Thus mail addressed to rebecca+inbox is placed in a mailbox name inbox by the user rebecca.

The problem with this is that neither Sendmail nor Linux uses a mailbox architecture. Sendmail writes to a single pool file for each user, and Linux user mail agents read from a single pool file for each user. Thus, bound for user rebecca is written to and read from the file /var/pool/mail1/rebecca. Mailboxes exist on Linux systems, but they exist because the user agent reads the mail from the single pool file and routes it to different mailboxes based on some rules defined inside the user agent.

![](bbox=[0.935, 0.272, 0.985, 0.378])