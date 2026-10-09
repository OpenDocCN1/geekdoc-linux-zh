
## Prerequisites

Install the dovecot package. The rpm installation script creates the self-signed certificates dovecot requires in the files named `/etc/pki/dovecot/certs/dovecot.pem` and `/etc/pki/dovecot/private/dovecot.pem`. Typically, you do not need to modify the dovecot configuration file (`/etc/dovecot/dovecot.conf`).

## Enable and start dovecot

Run systemctl to cause dovecot to start when the system enters multiuser mode and then start dovecot. Use the systemctl status command to make sure the service is running.

```bash
# systemctl enable dovecot.service
# systemctl start dovecot.service
```

After modifying a dovecot configuration file, give the same command, replacing `start` with `restart`, to cause dovecot to reread its configuration files.

## AUTHENTICATED RELAYING

If you travel with a portable computer such as a laptop, you might connect to the Internet through a different connection at each location where you work. Perhaps you travel for work, or maybe you just bring your laptop home at night.

This section does not apply if you always dial in to the network through your ISP. In that case, you are always connected to your ISP's network and it is as though you never moved your computer.

On a laptop you do not use a local instance of sendmail to send email. Instead, you use SMTP to connect to an ISP or to a company's SMTP server (a smarthost), which then relays your outgoing mail. To avoid relaying email for anyone, including malicious users who would send spam, SMTP servers restrict who they relay email for, based on IP address. By implementing authenticated relaying, you can cause the SMTP server to authenticate, based on user identification. In addition, SMTP can encrypt communication when you send mail from your email client and use an SMTP server.

An authenticated relay provides several advantages over a plain connection:

- You can send email from any Internet connection.
- The secure connection makes it more difficult to intercept email as it traverses the Internet.
- The outgoing mail server requires authentication, preventing it from being used for spam.

You set up authenticated relaying by creating an SSL certificate or using an existing one, enabling SSL in sendmail, and telling your email client to connect to the SMTP server using SSL. If you have an SSL certificate from a company such as VeriSign, you can skip the next section in which you create a self-signed certificate.

## CREATING A SELF-SIGNED CERTIFICATE FOR sendmail

The default location for SSL certificates is **/etc/pki/tls/certs** (PKI stands for public key infrastructure). Working with *root* privileges, give the command `make sendmail.pem` in this directory to generate the required certificates. Apache uses a similar procedure for creating a certificate (page 970).

```bash
# cd /etc/pki/tls/certs
# make sendmail.pem
... 
Generating a 2048 bit RSA private key
................................................................++++++
writing new private key to '/tmp/openssl.snxDr0'

You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [XX]:US
State or Province Name (full name) []:California
Locality Name (eg, city) [Default City]:San Francisco
Organization Name (eg, company) [Default Company Ltd]:Sobell Associates Inc.
Organizational Unit Name (eg, section) []:
Common Name (eg, your name or your server's hostname) []:sobell.com
Email Address []:mgs@sobell.com
..............................+++++++++
```

You can enter any information you wish in the certificate.

## ENABLING SSL IN SENDMAIL

Once you have a certificate, instruct **sendmail** to use it by uncommenting (removing the leading `d1` from) the following lines in **sendmail.mc**:

```
TRUST_AUTH_MECH(`EXTERNAL DIGEST-MD5 CRAM-MD5 LOGIN PLAIN')d1
define(`confAUTH_MECHANISMS', `EXTERNAL GSSAPI DIGEST-MD5 CRAM-MD5 LOGIN PLAIN')d1
```

These lines specify the authentication mechanisms.

Next, uncomment the following lines in **sendmail.mc** to tell **sendmail** where the certificate is:

```
define('confCACERT_PATH', '/etc/pki/tls/certs')d1
define(`confCACERT', `/etc/pki/tls/certs/ca-bundle.crt')d1
define(`confSERVER_CERT', `/etc/pki/tls/certs/sendmail.pem')d1
define(`confSERVER_KEY', `/etc/pki/tls/certs/sendmail.pem')d1
```

Encrypted connections are made in one of two ways: SSL (simpler) or TLS. SSL requires a dedicated port and has the client and the server negotiate a secure connection and continue the transaction as if the connection were not encrypted. TLS has the client connect to the server using an insecure connection and then issue a STARTTLS command to negotiate a secure connection. TLS runs over the same port as an unencrypted connection. Because many clients support only SSL, it is a good idea to instruct **sendmail** to listen on the SMTPS port. The final line you must uncomment in **sendmail.mc** instructs **sendmail** to listen on the SMTPS (SMTP secure) port:

```
DAEMON_OPTIONS(`Port=smtps, Name=TLSMTA, M=$\')dn1
```

### Enabling SSL in the Mail Client

Enabling SSL in a mail client is usually quite simple. For example, Evolution provides the *Edit**Preferences**Mail Accounts**Edit**Receiving Email**Security**Encryption Method* combo box that allows you to choose the type of encryption you want to use: No encryption, STARTTLS encryption, or SSL on a dedicated port. There is a similar combo box under the *Sending Email* tab. Alternately, you can specify the type of encryption you want to use when you set up Evolution.

## CHAPTER SUMMARY

The **sendmail** daemon is an MTA (mail transfer agent). When you send a message, **sendmail** works with other software to get the email to the proper recipients. You can set up **sendmail** to send email to an SMTP server that then relays the email to its destination or you can have **sendmail** send email directly to the SMTP servers for the domains receiving the email. By default, **sendmail** stores incoming messages in the mail spool directory, */var/spool/mail*.

The **sendmail.cf** file controls many aspects of how **sendmail** works. If you edit this file, restart the **sendmail** service to regenerate **sendmail.cf**. The system administrator can use the */etc/aliases* file and ordinary users can use *~/.forward* files to reroute email to one or more local or remote addresses, to files, or as input to programs.

You can use a program such as SpamAssassin to grade and mark email as to the likelihood of it being spam. You can then decide what to do with the marked email: You can look at each piece of potential spam and decide where to put it, or you can have your MUA automatically put potential spam in a special mailbox for spam.

Other programs that can help with email include *SquirrelMail*, which provides Webmail services, and *Mailman*, which provides mailing list support. *IMAP* (Internet Message Access Protocol) and *POP* (Post Office Protocol) allow users to retrieve and manipulate email remotely. The *Dovecot* system provides IMAP and POP servers.

## EXERCISES

- 1. By default, email addressed to *system* goes to *root*. How would you also save a copy in */var/logs/systemmail*?
- 2. How would Max store a copy of his email in ~/mbox and send a copy to max@example.com?
- 3. If your firewall allowed only the machine with the IP address 192.168.1.1 to send email outside the network, how would you instruct the local copy of sendmail to use this server as a relay?
- 4. What does dnl stand for in the m4 macro language? What are dnl commands used for?
- 5. SpamAssassin is installed on your mail server, with the threshold set to an unusually low value of 3, resulting in a lot of false positives. What rule could you give to your mail client to allow it to identify spam with a score of 5 or higher?
- 6. Describe the software and protocols used when Max sends an email to Sam on a remote Linux system.

### ADVANCED EXERCISES

- 7. Your company's current mail server runs on a commercial UNIX server, and you are planning to migrate it to Linux. After copying the configuration files across to the Linux system, you find that it does not work. What might you have forgotten to change?
- 8. Assume a script stores certain information in a variable named RESULT. What line could you put in the script that would send the contents of RESULT to the email address specified by the first argument on the command line?
- 9. Give a simple way of reading your email that does not involve the use of an MUA.
- 10. If you accidentally delete the /etc/aliases file, how could you easily re-create it (assuming that you had not restarted sendmail)?
