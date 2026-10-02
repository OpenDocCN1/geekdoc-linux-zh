
The next step is checking the fingerprint of the new key. Type the following command to get the fingerprint of the US-CERT key:

```
gpg --fingerprint us-cert@us-cert.gov
```

GPG prints the fingerprint, as follows:

```
pub 2048R/F0E187D0 2018-09-08 [expires: 2019-10-01]
Key fingerprint = 049F E3BA 240B 4CF1 3A76 06DC 1868 49EC F0E1 87D0
uid US-CERT Operations Key <us-cert@us-cert.gov>
```

At this point, you need to verify the key fingerprint with someone at the US-CERT organization.

If you think that the key fingerprint is good, you can sign the key and validate it. Here's the command you use to sign the key:

```
gpg --sign-key us-cert@us-cert.gov
```

GPG asks for confirmation and then prompts you for your passphrase. After that, GPG signs the key.

![](img/322157d1fa7d965f05bcd68ed0ffc36b_410_0.png)

Because key verification and signing are potential weak links in GPG, be careful about what keys you sign. By signing a key, you say that you trust the key to be from that person or organization.

## Signing a file

You may find signing files to be useful if you send a file to someone and want to assure the recipient that no one tampered with the file and that you did in fact send the file. GPG makes signing a file easy. You can compress and sign a file named message with the following command:

```
gpg -o message.sig -s message
```

To verify the signature, type

```
gpg --verify message.sig
```

To get back the original document, type

```
gpg -o message --decrypt message.sig
```

Sometimes, you don’t care about keeping a message secret, but you want to sign it to indicate that the message is from you. In such a case, you can generate and append a clear-text signature with the following command:

```
gpg -o message.asc --clearsign message
```

This command appends a clear-text signature to the text message. Here’s a typical clear-text signature block:

```
-----BEGIN PGP SIGNATURE-----
Version: GnuPG v1.4.2 (GNU/Linux)
iD8BQFDEhAtahWlHhs4pygRAhiqAJ9Jq0pPMgKVBuokDyUZaEYVsp6RIQCfaoBm
9zCwrSA9mo2DXJvbKS3ri8=
=2uc/
-----END PGP SIGNATURE-----
```

When a message has a clear-text signature appended, you can use GPG to verify the signature with the following command:

```
gpg --verify message.asc
```

If you indeed signed the message, the last line of the output says that the signature is good.

## Encrypting and decrypting documents

To encrypt a message meant for a recipient, you can use the --encrypt (or -e) GPG command. Here’s how you might encrypt a message for US-CERT by using its GPG key:

```
gpg -o message.gpg -e -r us-cert@us-cert.gov message
```

The message is encrypted with the US-CERT public key (without a signature, but you can add the signature with the -s command).

When US-CERT receives the message.gpg file, the recipient must decrypt it by using US-CERT’s private key. Here’s the command that someone at US-CERT can use:

```
gpg -o message --decrypt message.gpg
```

Then GPG prompts for the passphrase to unlock the US-CERT private key, decrypts the message, and saves the output in the file named message.

If you want to encrypt a file that no one else has to decrypt, you can use GPG to perform symmetric encryption. In this case, you provide a passphrase to encrypt the file with the following GPG command:

```
gpg -o secret.gpg -c somefile
```

GPG prompts you for the passphrase and asks you to repeat the passphrase (to make sure that you didn’t mistype anything). Then GPG encrypts the file, using a key generated from the passphrase.

To decrypt a file encrypted with a symmetric key, type

```
gpg -o myfile --decrypt secret.gpg
```

GPG prompts you for the passphrase. If you enter the correct passphrase, GPG decrypts the file and saves the output (in this example) in the file named myfile.

## Monitoring System Security

Even if you secure your system, you have to monitor the log files periodically for signs of intrusion. You may want to use Tripwire (a good tool for detecting any changes made in the system files) so that you can monitor the integrity of critical system files and directories. Your Linux system probably doesn’t come with the Tripwire File Integrity Manager package; you have to buy it from www.tripwire.com. After you purchase and install Tripwire, you can configure it to monitor any changes in specified system files and directories on your system.

Periodically examine the log files in the /var/log directory and its subdirectories. Many Linux applications, including some servers, write log information by using the logging capabilities of syslogd or rsyslogd. On Linux systems, the log files written by syslogd and rsyslogd reside in the /var/log directory. Make sure that only the root user can read and write these files.

![](img/322157d1fa7d965f05bcd68ed0ffc36b_412_0.png)

The syslogd configuration file is /etc/syslog.conf, and the rsyslogd configuration file (existing on many newer systems) is /etc/rsyslog.conf. The default configuration of syslogd generates the necessary log files, but if you want to examine and understand the configuration file, type man syslog.conf or man rsyslog.conf for more information.

## Securing Internet Services

For an Internet-connected Linux system, or even one on a TCP/IP local-area network (LAN) that’s not connected to the Internet, a significant threat is that someone could use one of many Internet services to gain access to your system. Each service — such as mail, web, and FTP — requires running a server program that responds to client requests arriving over the TCP/IP network. Some of these server programs have weaknesses that an outsider could use to log in to your system — maybe with `root` privileges. Luckily, Linux comes with some facilities that you can use to make the Internet services more secure.

![](img/322157d1fa7d965f05bcd68ed0ffc36b_413_0.png)

Potential intruders can employ a *port-scanning tool* — a program that attempts to establish a TCP/IP connection at a port and then looks for a response — to check which Internet servers are running on your system. Then, to gain access to your system, intruders can potentially exploit any known weaknesses of one or more services.

### Turning off stand-alone services

To provide Internet services such as web, email, and FTP, your Linux system has to run server programs that listen to incoming TCP/IP network requests. Some of these servers start when your system boots, and they run all the time. Such servers are *stand-alone servers*. The web server and mail server are examples of stand-alone servers.

Another server, `xinetd`, starts other servers that are configured to work under `xinetd`. Some Linux systems use the `inetd` server instead of `xinetd` to start other servers.

Some servers can be configured to run on a stand-alone basis or under a super server such as `xinetd`. The `vsftpd` FTP server, for example, can be configured to run as a stand-alone server or to run under the control of `xinetd`.

![](img/322157d1fa7d965f05bcd68ed0ffc36b_413_1.png)

In Debian and Ubuntu, use the `update-rc.d` command to turn off stand-alone servers, and use the `invoke-rc.d` command to start or stop servers interactively. To get a clue about the available services, type `ls /etc/init.d`, and look at all the script files designed to turn services on or off. You have to use these filenames when you want to turn a service on or off. To turn off Samba service, for example, type **update-rc.d -f samba remove**. If the service was already running, type **invoke-rc.d samba stop** to stop the service. You can use the `invoke-rc.d` command to stop any service in a similar manner.

![](img/322157d1fa7d965f05bcd68ed0ffc36b_414_0.png)

In Fedora and SUSE, you can turn stand-alone servers on and off by using the `systemctl` command. You can get the names of the service scripts by typing `ls /etc/init.d`. Then you can turn off a service (such as Samba) by typing `sudo systemctl stop smb`. If the service was already running, type `/etc/init.d/smb stop` to stop the service. You can run scripts from the `/etc/init.d` directory with the `stop` argument to stop any service in a similar manner.

### Configuring the Internet super server

In addition to stand-alone servers such as web and mail servers, the servers `inetd` and `xinetd` servers have to be configured separately. These servers are *Internet super servers* because they can start other servers on demand.

![](img/322157d1fa7d965f05bcd68ed0ffc36b_414_1.png)

Type `ps ax | grep inetd` to see which Internet super server — `inetd` or `xinetd` — your system runs.

Debian and Ubuntu use `inetd`, and Fedora and SUSE use `xinetd`.

![](img/322157d1fa7d965f05bcd68ed0ffc36b_414_2.png)

The `inetd` server is configured through the `/etc/inetd.conf` file. You can disable a service by locating the appropriate line in that file and commenting it out by placing a pound sign (`#`) at the beginning of the line. After saving the configuration file, type `/etc/init.d/inetd restart` to restart the `inetd` server.

Configuring the `xinetd` server is a bit more complicated. The `xinetd` server reads a configuration file named `/etc/xinetd.conf` at startup. This file in turn refers to configuration files stored in the `/etc/xinetd.d` directory. The configuration files in `/etc/xinetd.d` tell `xinetd` which ports to listen to and which server to start for each port. Type `ls /etc/xinetd.d` to see a list of the files in the `/etc/xinetd.d` directory on your system. Each file represents a service that `xinetd` can start. To turn off any of these services, edit the file in a text editor, and add a `disable = yes` line in the file. After you make any changes in the `xinetd` configuration files, you must restart the `xinetd` server; otherwise, the changes don’t take effect. To restart the `xinetd` server, type `/etc/init.d/xinetd restart`. This command stops the `xinetd` server and then starts it again. When the server restarts, it reads the configuration files, and the changes take effect.

### Configuring TCP wrapper security

A common security feature of `inetd` and `xinetd` is their use of the TCP wrapper to start various services. The *TCP wrapper* is a block of code that provides an access-control facility for Internet services, acting like a protective package for your message. The TCP wrapper can start other services, such as FTP and Telnet, but before starting a service, it consults the `/etc/hosts.allow` file to see whether
