
# Chapter 7 • Securing Exchange and Outlook Web Access

> WARNING
> Enabling HTTP logging will generate huge log files with just a few OWA connections due to the number of requests that hit the server for each message opened. A simple request to open the default OWA mailbox page and send a single OWA e-mail message generates 140 entries in the log file. Plus each currently connected OWA client (running IE 5.0 or later) polls the server once every two minutes. Remember to purge or archive older logs.

# Securing MAPI Clients

One of the places people often forget to focus their security effort is the client side. As far as the messaging system is concerned, this is one of the most vulnerable areas because this is where messages are the easiest to read. This is also the location from which e-mail-based viruses are spread. In this section, I make a couple of recommendations to help keep your messaging system safe from viruses and protect the message content.

# Message Content Vulnerabilities

Any message content that is stored on the client side is vulnerable to being viewed by an intruder. This is because the local file systems on workstations are much easier to compromise than a physically secured Exchange server. The following are some recommendations for helping to ensure that the client-side of the messaging security equation is secure:

- If you are concerned about messaging security, do not allow users to use POP3 or IMAP4 solutions. Deploy only Outlook MAPI clients. Locally stored data in POP3 and IMAP4 clients is too easily compromised.
- Do not allow users to store critical e-mail in PST files; in a very security-conscious organization, PST files should never be used. Even though PST files can be password protected, there are a couple of utilities that are easily downloadable that can crack these passwords.
- Require users to lock their workstations prior to leaving their desks.
- Enable and require SSL for users using OWA

![](img/729efc56f204a2ebffb8295c3a2dfdfb_400_0.png)

# Protecting Against Message-Based Viruses at the Client

Almost all the e-mail-based viruses over the past couple of years have been targeted and spread by API clients. These viruses open your global address list or personal address books and send themselves to everyone in your address list. For this reason, providing additional anti-virus protect at the client is essential. The following is a list of anti-virus precautions that you should take at the client side:

- If you are not running Outlook 2002, install the Outlook Security Update for Outlook 98 and 2000. This disables some of the features that allow viruses to spread from the Outlook client.
- If you are running Outlook 2002, configure the Outlook Security Template to restrict dangerous attachments from being opened at the Outlook client.
- All clients must have anti-virus software installed. The software should be able to scan e-mail messages when they are prepared or processed.
- Anti-virus client software and signature files must be kept up to date.
- Outlook 2002 SR-1 includes a feature that allows users to read HTML messages as plain text, thus reducing the potential danger associated with HTML mail. See www.slipstick.com/dev/code/zaphtml.htm for more information.

For more information about the Outlook Email Security Update, visit Slipstick System's Outlook Security update page at www.slipstick.com/outlook/esecup.htm. If you are interested in learning more about using the Outlook 2002 security features, read about the Outlook Security Template from the Office XP Resource Kit or in Chapter 2 of the NSA's Guide to Secure Configuration and Administration of Microsoft Exchange 2000; you can download it at http://nsa2.www.conion.com/win2k/download.htm.

378 Chapter 7 • Securing Exchange and Outlook Web Access

# Enabling Message Encryption (S/MIME)

If you are truly paranoid about the security of your messaging data, and all of the other precautions you have taken not made you feel at ease, enabling your users to use S/MIME (Secure/MIME) may be the next step for you. S/MIME defines extensions to the MIME standard that allow a user to send encrypted and/or digitally signed messages between any two messaging clients as long as both clients support S/MIME.

> NOTE
> For more information on S/MIME, see RFCs 2311 and 2633. The full text of the RFCs can be found at www.rfc-editor.org.

When using an S/MIME solution, the message body and attachments are encrypted at the sender's computer prior to being sent to the sender's home server. The message remains encrypted while the message is transmitted and it is stored in the recipient's home message store. It is decrypted only when the intended recipient opens the message. The only catch is that the sender must have a digital certificate (X.509v3) for all intended recipients of the message.

Implementing an S/MIME solution for your users will most definitely increase your support load. Certificates have to be issued to users, certificates expire and to be renewed, user's computers are rebuilt and they lose their certificates, and users will inevitably have support-related questions about this new feature. One of the biggest decisions you will have to make is whether you are going to get your mail certificates from a trusted authority (such as Thawte, Verisign, etc.) or whether you are going to “roll your own."

If you have only a few users who require encryption or digital signatures, you are probably off getting a third-party certificate authority. On the other hand, if you are going to have many users who require certificates, you should consider deploying the Exchange 2000 KMS. The requirements for the Exchange 2000 KMS are as follows:

- There must be a Windows 2000 Enterprise CA installed and configured to issue Enrollment Agent (Computer), Exchange User, and Signature Only certificates.
- You cannot install the Exchange 2000 KMS on an Exchange 2000 server in a cluster.

![](img/729efc56f204a2ebffb8295c3a2dfdfb_402_png)

# Securing Exchange and Outlook Web Access - Chapter 7

Once the Key Management Server is installed, you will find two new objects in the Administrative Group that contains the Exchange 2000 Key Management Server. This is the Encryption Configuration object and the Key Manager. The Key Manager is used to issue certificates, revoke certificates, and recover lost keys. The Encryption Configuration object is used to configure the type of encryption clients that users in this administrative group require. Unless you are supporting older clients from Exchange 4.0 and 5.0, you should always choose S/MIME as the security message format.

# Following Best Practices

There are a number of best practices that I recommend all Exchange 2000 administrators follow to keep their Exchange organizations secure. Some of these are administrative practices, but others are simply things that you need to teach your user community about. The following is a list of best practices for keeping your Exchange data secure:

- Apply all W2K, E2K, IIS, and IE SPs and fixes.
- Apply Prohibit Send and Receive limits for all users.
- Apply Maximum incoming and outgoing message size for all users.
- Implement SSL for all Internet protocols.
- Update all Outlook clients to a minimum of Outlook 2000 or Outlook 2002 with the security updates.
- Perform daily reviews of System, Application, and Security logs.
- Ensure that daily backups are performed and that the backup tapes are always secure.
- Apply NTFS security to all data directories and log directories, including IIS logs.
