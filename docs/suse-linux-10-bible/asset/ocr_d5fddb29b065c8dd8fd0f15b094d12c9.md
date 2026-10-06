# Mail Servers - Postfix, Sendmail, Qpopper, and Cyrus

# CHAPTER 17

# In This Chapter

+   - Sending mail via SMTP
- Configuring Postfix
- Configuring sendmail
- Configuring Qpopper
- Configuring Cyrus
- Choosing a mail client

One of the primary uses for Linux is mail servers — the Internet (aside from Apache) — both the position of an MTA (Postfix, sendmail, Exim, and so on) and an MDA (Cyrus, Qpopper, and so on).

The MTA, MDA, and MUA are generic ways of referring to the components in a mail system.

+   **Mail Transfer Agent (MTA)**—The component of the mail system that handles the receiving and sending of mail over the SMTP protocol.
**Mail Delivery Agent (MDA)**—Controls the delivery of mail into a user's mailbox. MDA also deals with the presentation of mail to a user over POP3 or IMAP.
**Mail User Agent (MUA)**—The component that the end user employs to read mail. This could be Evolution, Outlook, mail, *mutt*, or any other choice of MUA on the market.

A few very popular MTAs have arrived on the scene, the grandfather of all being sendmail.

Linux is extremely suited to the hosting of mail, and the authors have worked on very large mail infrastructures where Linux has been prevalent. This chapter discusses using Linux as a mail server, and focuses in particular on sendmail or Postfix as an MTA and Qpopper and Cyrus as MDAs.