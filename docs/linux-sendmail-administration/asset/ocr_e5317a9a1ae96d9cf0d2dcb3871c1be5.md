# Chapter 12 Sendmail Security

RunAsUser id—includes Sendmail itself and all of the mailers and commands executed by Sendmail. All of the files read by Sendmail must be readable by this user and all of the files written by Sendmail must be writeable by this user.

The RunAsUser option is intended for use only on firewall mail servers. On a mail server, the mail is received, processed, and then forwarded to the internal mail server where users read their mail. The firewall mail server does not have any user accounts, so there is no need for the Sendmail program to assume the identity of a specific user or to deliver or write a file into a user's mailbox. The RunAsUser option is not used on a regular mail server.

For most configurations, you also need to define the mailuser in the /etc/passwd directory. The mailuser becomes the DefaultUser, which gives you the separation between file creation and command execution that is the key benefit of having different user IDs for Sendmail. Once mailuser is defined the DefaultUser option, to define a value for TrustedUser. For most systems, root is a fine TrustedUser. Additionally, root is the correct RunAsUser for the vast majority of Sendmail servers.

# Securing Files and File Access

Using the correct user for Sendmail is only part of the story. Sendmail also needs to be careful about the files it reads and what is in them. Maintaining the following standards will help avoid problems:

+   - Files that the relay-domains file is writable, for example, if anyone on the system can grant relay permission to their favorite spammer. The recommended permission for files read by Sendmail is 644.

+   - Files read by Sendmail should not be in group- or world-writable directories. Again, anyone in a given group, or perhaps anyone on the system, can create a file Sendmail bad instructions. The recommended permissions for directories used by Sendmail is 755.

+   - Files read or written by Sendmail should not be symbolic links.

In some conditions—for reading a .forward file—Sendmail checks that these standards are being maintained. You can disable this file access by setting the DontBlameSendmail option using the DontBLAME_SENDMAIL parameter in the m4 configuration file. All of the DontBlameSendmail settings reduce security, so they are not covered here. For more information about this option, see Appendix C, "Sendmail Variables, Options, and Flags."

Sendmail takes special care with the .forward file because that can contain an e-mail address that forwards the file to a program using the l program, where program is the name of the program to be executed. The aliases database can also use this syntax