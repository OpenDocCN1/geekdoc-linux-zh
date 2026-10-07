The tasks that a Sendmail server performs can be divided into two basic functional groups: the roles that Sendmail performs as a message submission agent and as a message transport agent. The distinctions between these roles can be subtle, and the roles sometimes overlap. But these two basic roles incorporate all of the tasks performed by a Sendmail server and help explain what various configuration values do and why they need to be defined. Much of the Sendmail configuration is used to specify how Sendmail should handle its duties as a message submission agent.

# A Message Submission Agent

The functions of Sendmail described in this section might not meet the RFC definition of an MSA, but they come close. An MTA that accepts a message directly from an MUA and takes an active role in formatting a complete mail message is an MSA.

+   - accepts mail from an MUA
- determines the delivery program for the mail
- reformats the mail addresses for the selected mailer
- adds the headers required by the mailer
- sends the message to the mailer for delivery

In this book I'm using "message submission agent" (the MUA) to describe the role that Sendmail fills as the interface between the user's e-mail program (the MUA) and the mail delivery program (the MTA). Even when Sendmail is the MTA, things must be done to the mail received from the MUA to prepare for delivery, and of course, Sendmail is not the only MTA that can run on a Linux system. A user can create a wide variety of mail with an e-mail program. The mail entered by the user could be local mail bound for another user; it could be Internet mail bound for a remote user; it could be data bound for a Linux program; to prepare for delivery. (See Appendix A, "Macro Command Reference," for a full list of the mailers supported by Sendmail.) All that a supported mail program running on a Linux system needs to do is pass the mail message to Sendmail. Sendmail is equipped to select the appropriate delivery agent and to properly prepare the mail for delivery.

# Sendmail Mailers

The mail delivery programs are called mailers in Sendmail terminology. The mailers available to Sendmail are defined inside the Sendmail configuration file. A mailer definition assigns an internal mailer name to a mail delivery program. These names are arbitrary, but most Linux systems use the standard mailers defined by the default Sendmail configuration. Chapter 5, "Understanding a Vendor Configuration," describes each of the default mailers.

A mailer definition also provides Sendmail with the full pathname of the mail delivery program and the command-line arguments Sendmail should use when it launches