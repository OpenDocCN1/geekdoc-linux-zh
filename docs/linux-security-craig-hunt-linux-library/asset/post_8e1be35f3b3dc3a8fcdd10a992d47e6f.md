
For example, consider the client/server conversation in Listing 6.4.

## Listing 6.4 POP3 session: conventional (USER/PASS) authentication

```
[ramon]$ telnet pop3.example.com 110
Trying 209.1.78.12 ...
Connected to pop3.example.com.
Escape character is '^]'.
+OK QPOP (version 3.1b6) at pop3 starting. <3606.975375600@redhat>
USER ramon
+OK Password required for ramon.
PASS mysecret
+OK ramon has 1 visible messages (0 hidden) in 890 octets.
```

The main security flaw with the implementation in Listing 6.4 is the fact that the user must supply a password as part of the authentication sequence. This exposes a piece of secret material to eavesdropping over the public Internet, especially considering that some POP3 clients can be configured to automatically contact the server periodically to check for newly arrived e-mail.

In order to alleviate this risk, the POP3 protocol developers amended the original standard with a challenge/response mechanism by which the POP3 server presents the client with a challenge (the current decimal value of the system clock). It is then up to the client to generate an MD5 one-way hash of the challenge, appended to the authentication password that the POP3 administrator has assigned to the user. The client then returns the result of the hash in the APOP line. If the server successfully replicates the response at its end and it matches the one returned by the client, then the authentication is successful, and the user is allowed to retrieve messages from their mailbox.

In the example in Listing 6.5, username ramon is attempting to log on to pop3.example.com to read his mail.

## Listing 6.5 POP3 session: APOP authentication

```
[ramon]$ telnet pop3.example.com 110
Trying 209.1.78.12 ...
Connected to pop3.example.com.
Escape character is '^]'.
+OK QPOP (version 3.1b6) at pop3 starting. <3606.975375600@pop3>
APOP ramon 59df6759df98s7d9fs7d9f75d9f758g
+OK ramon has 1 visible messages (0 hidden) in 890 octets.
```

The POP3 server in Listing 6.5 presents the user with the challenge (a string of characters that they must use in their reply):

`<3606.975375600@pop3>`

which the client appends to the password to form the following string:
`<3606.975375600@pop3>mysecret`

It then proceeds to feed this string to the MD5 algorithm, which produces a hash value of
`s9df67$s9df798$s7d9f57d9f7s9df758g`

Note that the robustness of this approach comes from the fact that it is mathematically infeasible to obtain the original *seed* from the MD5 hash. Therefore, even if the eavesdropper knows the challenge that the POP3 server sent to the client, the risk of having them reverse the MD5 function to obtain the seed is minimal.

The next section walks you through the process of installing the Qualcomm Qpopper package, including how to configure the APOP authentication method.

### Installing the Qpopper Software

The Qpopper package is not typically installed by default on most Linux distributions, but it can be easily obtained in RPM format and installed using the Linux *rpm* utility, as follows:

```
[ramon]$ sudo rpm -i qpopper-3.1b6-3k.i586.rpm
```

This command installs the server binary and the man pages, as well as a limited set of documentation. The next section shows you how to set up the POP3 server, as well as its extended authentication feature.

### Configuring the Qpopper Software

The latest version of Qpopper at the writing of this book (3.1) does not automatically create an *xinetd* entry in order to spawn itself automatically. To make sure this happens, simply create the file */etc/xinetd.d/qpopper* with the contents in Listing 6.6.

## Listing 6.6 Contents of the /etc/xinetd.d/qpopper file

```
service pop3
{
    socket_type           = stream
    wait                  = no
    user                  = root
    server                = /usr/sbin/in.qpopper
    log_on_success        ++ USERID
    log_on_failure        ++ USERID
}
```

The directives in Listing 6.6 ensure that your server listens to requests for the POP3 service (TCP port 110) with the `/usr/sbin/in.qpopper` as the daemon.

If you are using `inetd` instead of `xinetd`, simply enter the following in your `inetd.conf` file:

```
pop3 stream tcp nowait root /usr/sbin/in.qpopper in.qpopper
```

The next step in the configuration is creating a username (e.g., `pop`) to own the authentication database (user/password associations) for APOP (see Figure 6.1). In this figure, `linuxconf` is being used on Red Hat to create a POP3 administrative account.

![](img/3258bbaf790525f8c4eb25fabff7844a_186_0.png)

You should change the owner of the POP3-supplied `popauth` utility to be `pop`, and make it `suid pop` using the following commands:

```
[ramon]$ cd /usr/sbin
[ramon]$ sudo chown pop popauth
[ramon]$ sudo chmod u+s popauth
```

The very first time you run the `popauth` utility, you use it to create the authentication database, as follows:

```
[ramon]$ sudo popauth -init
```

You must make sure that the newly created authentication database file is only readable by the `pop` user:

```
[ramon]$ ls -1 /etc/pop.auth
-rw-------  1 pop popusers 1544 Nov 27 22:08 /etc/pop.auth
```

At this point, you have a fresh installation of Qpopper that is ready to be populated with new POP3 users. The next section explains how to do just that.

## Using the Qpopper Software

As you add new users to your server, you also need to allow them to use APOP authentication to your POP3 server. This requires an entry in `/etc/pop.auth` for each new user. To add these entries, simply issue a `popauth` command like:

```
[ramon]$ sudo popauth -user ramon
Changing only APOP password for ramon.
New password: mysecret
Retype new password: mysecret
```

Note that this example used the `sudo` command to run `popauth` as root, but in fact, the command could have been executed by user `pop` as well. If you need to revoke a user's POP3 access, simply delete that user from the database using the following command:

```
[ramon]$ sudo popauth -delete ramon
```

Once users have been added to `/etc/pop.auth`, they can change their own passwords, invoking the `popauth` utility as their own user, with no command-line options, as follows:

```
[ramon]$ popauth
Changing only APOP password for ramon.
Old password: mysecret
New password: newsecret
Retype new password: newsecret
```

This section discussed the POP3 protocol, its security shortcomings, and how you can get around them. The next section discusses the implementation of the IMAP protocol, an alternative to POP3 that is gaining a great deal of popularity in the Linux server community.

## IMAP

While POP3 is still the most popular mail-retrieval protocol, one of its fundamental shortcomings is the fact that messages have to be downloaded to the user's computer (the client) in order to have access to them. This makes it difficult for the user to select which messages they want to see before actually downloading them. It also makes it a challenge to read mail from multiple clients, while still keeping the mailbox in sync. The Internet Mail Access Protocol (IMAP) was developed at Stanford University circa 1986 to address this shortcoming, as well as to add a host of other improvements to the ubiquitous POP3 protocol.

IMAP is a true client/server protocol that is independent of the transport used to access the mail server. It also allows you to access different mail folders on the remote server, regardless of your identity and the user that owns the remote mailbox. While this offers unprecedented flexibility, it also introduces some concern and increases the risk of malicious eavesdropping of the mail traffic as it is being received from the IMAP server. More importantly, in the absence of any encryption between the client and the server, the username/password exchange will be in the clear as well.

If your needs are such that you can benefit from offering IMAP services to your mail users, the next section guides you through the process of installing the IMAP server software without jeopardizing the security of your server or the privacy of the mail contents and the user authentication exchange.

### Installing the IMAP Server Software

The University of Washington's IMAP server is the most popular and most actively supported IMAP package available for Linux. While it's not typically installed by default on most Linux distributions, it can be easily obtained in RPM format and installed using the Linux *rpm* utility:

```
[ramon]$ sudo rpm -i imap-2000-3.1386.rpm
```

This command installs the server binary and the man pages, as well as a limited set of documentation. The next section shows you how to set up the secure IMAP server, and how to enable it on xinetd and inetd.

### Configuring the Secure IMAP Server

The imapd-2000 package uses OpenSSL for its secure transport options (imapd). In order to configure the SSL service, simply create a self-signed certificate using the following commands:

```
[ramon]$ cd /usr/share/ssl/certs
[ramon]$ sudo make imappd.pem
```

This results in the creation of the file /usr/share/ssl/certs/imappd.pem, which contains both the key and the certificate that imapd-2000 will use to add SSL protection to the IMAP exchanges. Note that IMAP inserts two files in the /etc/xinetd.d directory, as shown in the steps in Listing 6.7.
