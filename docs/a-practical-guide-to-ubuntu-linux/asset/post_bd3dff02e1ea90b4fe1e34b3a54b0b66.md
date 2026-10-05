
# 736 CHAPTER 20 exim4: SETTING UP MAIL SERVERS, CLIENTS, AND MORE

dovecot init script After configuring Dovecot, start the Dovecot daemon(s) with the following command:

```bash
$ sudo service dovecot start
```

After modifying a Dovecot configuration file, give the same command, but replacing start with restart, to cause Dovecot to reread its configuration files.

# AUTHENTICATED RELAYING

If you travel with a portable computer such as a laptop, you may connect to the Internet through a different connection at each location where you work. Perhaps you travel for work, or may you just bring your laptop home at night.

This section does not apply if you always dial in to the network through your ISP. In case that, you are always connected to your ISP's network and it is as though you have moved your computer.

On a laptop you do not use a local instance of exim4 to send email. Instead, you use SMTP to connect to an ISP or to your company's SMTP server (a smarthost), which then relays your outgoing mail. To avoid relaying email for anyone, including malicious users who would send spam, SMTP servers restrict who they relay for, based on IP address. By implementing authenticated relaying, you can cause the SMTP server to authenticate, based on user identification. In addition, SMTP can encrypt communication when you send mail from your email client and use SMTP server.

An authenticated relay provides several advantages over a plain connection:

- You can send email from any Internet connection.
- The secure connection makes it more difficult to intercept email as it traverses the Internet.
- The outgoing mail server requires authentication, preventing it from being used for spam.

You set up authenticated relaying by creating an SSL certificate or using an existing one, enabling SSL in exim4, and telling your email client to connect to the SMTP server SSL. If you have an SSL certificate from a company such as VeriSign, you can skip the next section, in which you create a self-signed certificate.

# CREATING A SELF-SIGNED CERTIFICATE FOR exim4

Typically, installing Dovecot generates self-signed certificates. If necessary, use the following command to create SSL certificates for exim4. The keys are stored in exim.key and exim.crt in the /etc/exim4 directory. Apache uses a similar procedure for creating a certificate (page 93).

```bash
$ /usr/share/doc/exim4-base/examples/exim-gencert
[*] Creating a self signed SSL certificate for Exim!
```

This may be sufficient to establish encrypted connections but for secure identification you need to buy a real certificate!

Please enter the hostname of your MTA at the Common Name (CN) prompt!

Generating a 1024 bit RSA private key

```bash
+++++
writing new private key to `/etc/exim4/exim.key` +++++
```

You are about to be asked to enter information that will be incorporated into your certificate request.
What you are about to enter is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank.
For some fields there will be a default value,
If you enter '.', the field will be left blank.

- Country Code (2 letters) [US]: US
- State or Province Name (full name): California
- Locality Name (eg, city): San Francisco
- Organization Name (eg, company; recommended): Sobell Associates Inc.
- Organizational Unit Name (eg, section):
- Server name (eg, ssl.domain.tld; required!!!): sobell.com
- Email Address []: msg@sobell.com
[*] Done generating self signed certificates for exim!

> Refer to the documentation and example configuration files over `/usr/share/doc/exim4-base/` for an idea on how to enable TLS support in your mail transfer agent.

You can enter any information you wish in the certificate.

# ENABLING SSL in exim4

Once you have a certificate, create a file named exim4.conf.localmacros in the `/etc/exim4` directory (you have to work with root privileges). With the following contents, this file instructs exim4 to use SSL certificates:

```bash
$ cat /etc/exim4/exim4.localmacros
MAIN_TLS_ENABLE = 1
```

Because email will be relaying email, you need to add the name of the system you will be sending email from to the `dc_relay_nets` variable (page 726). Restart exim4 (page 716).

# ENABLING SSL IN THE MAIN CLIENT

Enabling SSL in a mail client is quite simple. For example, Evolution provides the Edit->Preferences->Mail Accounts->Email->Security Use Secure Connection combo box that allows you to choose the type of encryption you want to use: No encryption, SSL, or TLS encryption. Clicking the Check for Supported Types button (found below this combo box) queries the server and sets to use the type of security and authentication the server supports.

# CHAPTER SUMMARY

The exim4 daemon is an MTA (mail transfer agent). When you send a message, exim4 works with other software to get the email to the proper recipients. You can set up exim4 to send to an SMTP server that relays the email to its destination or you can send exim email directly to the SMTP servers for the domains receiving the email. By default, exim4 stores incoming messages in the spool directory, /var/mail/.

The /etc/exim4/update-exim4.conf file controls many aspects of how exim4 works. After you edit this file, you must use the exim4-update-conf command to apply the changes.

# EXERCISES

The exim4 daemon is an MTA (mail transfer agent). When you send a message, exim4 works with other software to get the email to the proper recipients. You can set up exim4 to send to an SMTP server that relays the email to its destination or you can send exim email directly to the SMTP servers for the domains receiving the email. By default, exim4 stores incoming messages in the spool directory, /var/mail/.

The /etc/exim4/update-exim4.conf file controls many aspects of how exim4 works. After you edit this file, you must use the exim4-update-conf command to apply the changes.

The /etc/exim4/update-exim4.conf file controls many aspects of how exim4 works. After you edit this file, you must use the exim4-update-conf command to apply the changes.

You can use SpamAssassin to grade and mark spam. You can use SpamAssassin to identify and mark spam and decide what to do with marked spam.

Other programs that can help include SquirrelMail, which provides mail services, and Mailman, which provides mailing lists. IMAP (Internet Access Protocol) and POP (Post Office Protocol) allow users to retrieve mail.

- 1. If you always dial in to the network through your ISP, you do not need authenticated relaying.
- 2. What are the advantages of an authenticated relay over a plain connection?
- 3. How do you set up authenticated relaying?
- 4. What is the purpose of a self-signed certificate in exim4?
- 5. What are the differences between a self-signed certificate and a real certificate?
- 6. Describe how to create a self-signed certificate for exim4.
- 7. How do you enable SSL in exim4?
- 8. How do you enable SSL in a mail client?
- 9. What is the role of the exim4 daemon?
- 10. What is the purpose of the /etc/exim4/update-exim4.conf file?
