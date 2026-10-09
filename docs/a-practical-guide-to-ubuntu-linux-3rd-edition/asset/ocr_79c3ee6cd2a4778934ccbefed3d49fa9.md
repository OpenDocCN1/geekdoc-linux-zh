# # 20

# ## exim4: SETTING UP MAIL SERVERS, CLIENTS, AND MORE

# **In This Chapter**

+   * Introduction to exim4. . . . . . . . . 714
+   * JumpStart I: Configuring exim4 to Use a Smarthost . . . . . . . . . . . . 716
+   * JumpStart II: Configuring exim4 to Send and Receive Mail . . . . . . 718
+   * Configuring an exim4 Mail Server. . . . . . . . . . . . . . . . . . 724
+   * SpamAssassin . . . . . . . . . . . . . . . . . . . . . 727
+   * Webmail . . . . . . . . . . . . . . . . . . . . . . . . . 731
+   * Mailing Lists . . . . . . . . . . . . . . . . . . . . . 733
+   * Setting Up an IMAP or POP3 Mail Server. . . . . . . . . . . . . . . . . . 735
+   * Authenticated Relaying . . . . . . . . . . . . . 736

Sending and receiving email require three pieces of software. At each end, there is a client, called an MUA (mail user agent), which is a bridge between a user and the mail system. Common MUAs are mutt, Evolution, KMail, Thunderbird, and Outlook. When you send an email, the MUA hands it to an MTA (a mail transfer agent, such as exim4 or sendmail), which transfers it to the destination server. At the destination, an MDA (a mail delivery agent, such as procmail) puts the mail in the recipient's mailbox file. On Linux systems, the MUA on the receiving system either reads the mailbox file or retrieves mail from a remote MUA or MTA, such as an ISP's SMTP (Simple Mail Transfer Protocol) server, using POP (Post Office Protocol) or IMAP (Internet Message Access Protocol).