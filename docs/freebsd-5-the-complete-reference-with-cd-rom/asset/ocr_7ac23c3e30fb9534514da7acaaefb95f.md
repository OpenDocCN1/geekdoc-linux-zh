the server and retrieve mail from it. In the case of IMAP, you should be able to move mail in and out of folders on the mail server computer from the mail client.

> Caution
> 
> **_IW IMAP stores mail in the user's home directory. Consequently, if the account is used for anything but mail storage, an IMAP client may take quite some time to scan all the files and directories, and report many of them as mail folders when they aren't. Some other IMAP servers store mail folders elsewhere or provide a way to configure how mail folders are stored._**

# # Setting Up Fetchmail

Ordinarily, a pull protocol such as POP or IMAP is used at the end of a mail delivery chain. These protocols allow mail clients such as Outlook, Eudora, or Sylpheed to retrieve mail from a mail server on which the user has a mail account. There are cases, though, where you might want to extend a mail delivery chain past the pull mail server and its client. For instance, suppose you're setting up the mail system for a small office that uses a broadband Internet connection. This broadband connection comes with an e-mail account, or the office has contracted with another ISP to host its e-mail, because the broadband ISP forbids the use of an SMTP server accessible from the outside. In such a case, you might want to retrieve e-mail from the outside pull mail servers and inject the mail into an internal mail server's mail queue. This approach allows you to combine mail from multiple external servers into a single local mail server. It also allows you to perform various mail manipulation tricks, such as running IMAP locally even if the ISP's support only POP.

To extend the mail delivery chain beyond a pull mail server, you need a special type of pull mail client. Rather than function as a conventional mail reader, this client can automatically inject mail into a local or remote mail queue. The recipient system can forward the mail further through SMTP connections or make it available via its own pull mail server. A popular program for performing this task of retrieving pull mail and re-mailing it is Fetchmail (http://www.tuxedo.org/∼esr/fetchmail/), which is available as a FreeBSD package and in the ports system.

# ## Fetchmail's Configuration File

Unlike many servers, Fetchmail doesn't need to run with any special permissions; it functions as an ordinary pull mail client, then as a client to a push mail server on its own or another computer. Thus, it is common to run Fetchmail as an ordinary user or as a special low-privilege user devoted to Fetchmail operation.

Fetchmail relies upon a configuration file called `.fetchmailrc` in the Fetchmail user's home directory. This file provides Fetchmail with all the information it needs