L=990 The argument defines the maximum line length for this mailer. In this case, the mailer can handle messages that contain individual lines up to 990 bytes long.

T=DNS/RFC822/SMTP The argument defines the MIME types for messages handled by this mailer. In this case, the mailer uses DNS for hostnames, RFC822 for e-addresses, and SMTP for error codes.

A=TCP 5 The argument defines the command used to execute the mailer. In this case, the argument refers to an internal Sendmail process. In other cases—the local mailer is a good example—the A argument is clearly a command line.

NOTE One of the confusing idiosyncrasies of Sendmail is that the path to Sendmail's internal mail delivery can be either TCP or IPC. For this version of Sendmail, TCP was used in the A argument. Or your version it might be IPC.

It is good to know how mailer definitions are structured, but the basic mailer definitions built from the m4 macros contain all the mailers you need to run Sendmail in a TCP/IP network environment. You shouldn't need to modify any mailer definitions for an average configuration. In fact, nothing in sendmail.cf files needs direct modifications for an average configuration. But this section of the book doesn't limit itself to average configurations, so in the next section we directly edit the sendmail.cf file and use tools to observe the impact of the change.

# # Editing the sendmail.cf File

It's important to realize how rarely the sendmail.cf file needs to be modified on a typical Linux system. The configuration file that comes with your Linux system will work. Generally, you modify the Sendmail configuration not because you need to, but because you want to. You modify the configuration to improve the ways things operate, not to get them operate, and when you do modify it, you change the m4 macro configuration—sendmail.cf. Despite this, in this section we edit the sendmail.cf file to change the way that Sendmail works.

> TIP Before you make any change to sendmail.cf—even a minor one—copy sendmail.cf to a work file such as test.cf and edit the work file. Never edit sendmail.cf without having a backup copy.

Assume your Linux system is named parrot.foobirds.org. Using the default configuration, the From address on outbound e-mail is user@parrot.foobirds.org. This is a valid