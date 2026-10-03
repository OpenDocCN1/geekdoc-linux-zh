
The next step is to ensure that sendmail does not get restarted automatically when the system is rebooted:

```
# systemctl disable sendmail
```

Sendmail is now switched off and configured to not auto-start when the system is booted. Optionally, to altogether remove sendmail from the system, run the following command:

```
# dnf remove sendmail
```

## 30.4 Firewall/Router Configuration

Since sending and receiving email messages involves network connections, the firewall must be configured to allow SMTP traffic. If firewalld is active, use the firewall-cmd tool as follows:

```
# firewall-cmd --permanent --add-service=smtp
```

It will also be essential to configure any other firewall or router between the server and the internet to allow connections on ports 25, 143, and 587 and, if necessary, to configure port forwarding for those ports to the corresponding ports on the email server.

With these initial steps completed, we can now install Postfix.

## 30.5 Installing Postfix on RHEL 9

By default, the RHEL 9 installation process installs postfix for most configurations. To verify if postfix is already installed, use the following rpm command:

```
# rpm -q postfix
```

If rpm reports that postfix is not installed, it may be installed as follows:

```
# dnf install postfix
```

The dnf tool will download and install postfix and configure a special postfix user in the /etc/passwd file.

## 30.6 Configuring Postfix

The main configuration settings for postfix are located in the /etc/postfix/main.cf file. Many resources on the internet provide detailed information on postfix, so this section will focus on the basic options required to get email up and running. Even though the dnf installation set up some basic configuration options, it tends to miss some settings and guess incorrectly for others, so carefully review the main.cf file.

The key options in the main.cf file are as follows:

```
myhostname = mta1.domain.com
mydomain = domain.com
myorigin = $mydomain
mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain
inet_interfaces = $myhostname
mynetworks = subnet
```

Other settings will have either been set up for you by the installation process or are only needed if you are feeling adventurous and want to configure a more sophisticated email system.

The format of myhostname is host.domain.extension. If, for example, your Linux system is named MyLinuxHost and your internet domain is MyDomain.com you would set the myhostname option as follows:

```
myhostname = mylinuxhost.mydomain.com
```

The mydomain setting is just the domain part of the above setting. For example:

```
mydomain = mydomain.com
```

The myorigin setting defines the name of the domain from which the output email appears to come from when it arrives in the recipient’s inbox and should be set to your domain name:

```
myorigin = $mydomain
```

One of the most crucial parameters, mydestination relates to incoming messages and declares the domains for which this server is the final delivery destination. Any incoming email messages addressed to a domain name, not on this list will be considered a relay request which, subject to the mynetworks setting (outlined below), will typically result in a delivery failure.

The inet_interfaces setting defines the network interfaces on the system via which postfix is permitted to receive email and is generally set to all:

```
inet_interfaces = all
```

The mynetworks setting defines which external systems are trusted to use the server as an SMTP relay. Possible values for this setting are as follows:

- **host** - Only the local system is trusted. Attempts by all external clients to use the server as a relay will be rejected.
- **subnet** - Only systems on the same network subnet can use the server as a relay. If, for example, the server has an IP address of 192.168.1.29, a client system with an IP address of 192.168.1.30 could use the server as a relay.
- **class** - Any systems within the same IP address class (A, B, and C) may use the server as a relay.

Trusted IP addresses may be defined manually by specifying subnets, address ranges, or referencing pattern files. The following example declares the local host and the subnet 192.168.0.0 as trusted IP addresses:

```
mynetworks = 192.168.0.0/24, 127.0.0.0/8
```

For this example, set the property to subnet so that any other systems on the same local network as the server can send email via SMTP relay. In contrast, external systems are prevented from doing so:

```
mynetworks = subnet
```

## 30.7 Configuring DNS MX Records

When you register and configure your domain name with a registrar, several default values will have been configured in the DNS settings. One of these is the so-called Mail Exchanger (MX) record. This record defines where email addressed to your domain should be sent and is usually set by default to a mail server provided by your registrar. If you are hosting your own mail server, the MX record should be set to your domain or the IP address of your mail server. The steps to make this change will depend on your domain registrar but generally involves editing the DNS information for the domain and either adding or editing an existing MX record so that it points to your email server.

## 30.8 Starting Postfix on a RHEL 9 System

Once the /etc/postfix/main.cf file is configured with the correct settings, it is now time to start up postfix. This can be achieved from the command line as follows:

```
# systemctl start postfix
```

If postfix was already running, make sure the configuration changes are loaded using the following command:

```
# systemctl reload postfix
```

To configure postfix to start automatically at system startup, run the following command:

```
# systemctl enable postfix
```

The postfix process should now start up. The best way to verify everything works is to check your mail log. This is typically in the /var/log/maillog file and should now contain an entry resembling the following output:

```
Mar 25 11:21:48 demo-server postfix/postfix-script[5377]: starting the Postfix mail system
Mar 25 11:21:48 demo-server postfix/master[5379]: daemon started -- version 3.3.1, configuration /etc/postfix
```

As long as no error messages have been logged, you have successfully installed and started postfix and are ready to test the postfix configuration.

## 30.9 Testing Postfix

An easy way to test the postfix configuration is to send email messages between local users on the system. To perform a quick test, use the mail tool as follows (where name and mydomain are replaced by the name of a user on the system and your domain name, respectively):

```
# mail name@mydomain.com
```

When prompted, enter a subject for the email message and then type the message body text. To send the email message, press Ctrl-D. For example:

```
# mail demo@mydomain.com
Subject: Test email message
This is a test message.
EOT
```

Rerun the mail command, this time as the other user, and verify that the message was sent and received:

```
$ mail
Heirloom Mail version 12.5 7/5/10. Type ? for help.
"/var/spool/mail/demo": 1 message 1 new
>N 1 root          Mon Mar 25 13:36  18/625   "Test email message"
&
```

Check the log file (/var/log/maillog) for errors if the message does not appear. Successful mail delivery will appear in the log file as follows:

```
Mar 25 13:41:37 demo-server postfix/pickup[7153]: 94FAF61E8F4A: uid=0 from=<root>
Mar 25 13:41:37 demo-server postfix/cleanup[7498]: 94FAF61E8F4A: message-id=<20190325174137.94FAF61E8F4A@demo-server.mydomain.com>
Mar 25 13:41:37 demo-server postfix/qmgr[7154]: 94FAF61E8F4A: from=<root@mydomain.com>, size=450, nrcpt=1 (queue active)
Mar 25 13:41:37 demo-server postfix/local[7500]: 94FAF61E8F4A: to=<neil@mydomain.com>, relay=local, delay=0.12, delays=0.09/0.01/0/0.02, dsn=2.0.0, status=sent (delivered to mailbox)
Mar 25 13:41:37 demo-server postfix/qmgr[7154]: 94FAF61E8F4A: removed
```

Once the local email is working, try sending an email to an external address (such as a GMail account). Also, test that incoming mail works by sending an email from an external account to a user on your domain. In each case, check the /var/log/maillog file for explanations of any errors.

## 30.10 Sending Mail via an SMTP Relay Server

An SMTP Relay service is an alternative to configuring a mail server to handle outgoing email messages. As previously discussed, several services are available, most of which can be found by performing a web search for “SMTP Relay Service”. Most of these services will require you to verify your domain in some way and will provide MX records with which to update your DNS settings. You will also be provided with a username and password, which must be added to the postfix configuration. The remainder of this section assumes that postfix is installed on your system and that all of the initial steps required by your chosen SMTP Relay provider have been completed.

Begin by editing the /etc/postfix/main.cf file and configure the myhostname parameter with your domain name:

```
myhostname = mydomain.com
```

Next, create a new file in /etc/postfix named sasl_passwd and add a line containing the mail server host provided by the relay service and the user name and password. For example:

```
[smtp.myprovider.com]:587 neil@mydomain.com:mypassword
```

Note that port 587 has also been specified in the above entry. Without this setting, postfix will default to using port 25, which is blocked by default by most SMTP relay service providers.

With the password file created, use the postmap utility to generate the hash database containing
