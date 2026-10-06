
# Linux Administration: A Beginner's Guide

Disconnected mode works by allowing users to retain cached copies of their mail stores. When the client is connected, any incoming/outgoing e-mail is immediately recognized and synchronized; however, when the client is disconnected, changes made on the client are kept until reconnection, when synchronization occurs. Because the client retains only a cached copy, a user can move to a completely different client and resynchronize his or her e-mail.

By using IMAP, your mail server will provide all three modes of access. After all is said and done, deploying and supporting both POP and IMAP is a good idea. It allows the users to choose whatever mail client and protocol best suits them.

There are several Free and Open Source Software (FOSS) mail servers that implement POP and IMAP. Some of Dovecot, University of Washington IMAP server (UW IMAP), Cyrus IMAP server, and Courier IMAP server. This chapter covers the installation and configuration of the popular Dovecot server software. This particular mail server has been available for many years. The installation process is also easy.

# POP3 and IMAP Protocol Basics

Like the other services discussed so far, POP3 and IMAP each need a server process to handle requests. The POP3, POP3S, IMAP, and IMAPS servers listen on ports 110, 995, 143, and 993, respectively.

Each request to respond from the server is in clear-text ASCII, which means it's easy for us to test the functionality of the server using Telnet. This is especially useful for quickly debugging mail server connectivity/availability issues. Like an SMTP server, you can interact with a POP3 or IMAP server using a short list of commands. Although there are many POP commands, here are a couple worth mentioning:

- USER
- PASS
- LOGIN
- LIST
- STATUS
- EXAMINE/SELECT
- CREATE/DELETE/RENAME
- LOGOUT

And a few noteworthy IMAP commands are the following:

Later in this chapter, we'll use some of these commands and walk through the connection and login process into a POP3 server and an IMAP server. This will allow us to verify that the server does in fact work.

# CHAPTER 20 Post Office Protocol and Internet Mail Access Protocol (POP and IMAP)

## Dovecot (IMAP and POP3 Server)

The Dovecot POP3 and IMAP server software is well regarded and is used in many production sites around the Dovecot world. It is a well-tested implementation and readily available in the mainstream Linux distros.

Dovecot provides its IMAP and POP3 functions through the following main processes. Collectively, these processes provide various services that make up the Dovecot ecosystem.

- Master process: As its name implies, the master process is the primary/overseer process. It is responsible for starting and keeping all the other processes running as needed. It reads the settings/options in the configuration files and exports the values to the other processes. The master process is responsible for collecting and managing all logging information Dovecot generates. The master process runs under the dovecot executable.
- Login processes: The login processes listen for connection requests for the POP3 and IMAP protocols and implement the minimum handshake protocol requirement before a user logs in successfully. You can find the login processes running under imap-login and pop3-login executables.
- Authentication (auth) process: Once the processes complete the underlying POP3 or IMAP protocol handshake and setup, control is passed on to the appropriate authentication process. The auth process is responsible for performing the actual user authentication (Simple Authentication and Security Layer [SASL] functions) to verify that the user is who she says is. The authentication processes run under a similarly named auth executable.
- Mail processes (IMAP, POP3): After authentication is successfully completed, the desired mail process kicks in and provides the user access to mailboxes. The mail process is the actual workhorse that implements the POP3 and IMAP protocol details. The IMAP process runs under an executable called imap, and the POP3 process runs under an executable named pop3.

# Installing Dovecot

Most Linux distributions have prepackaged binaries for Dovecot in the dist repositories. For example, it can be installed in Fedora/CentOS/RHEL using dnf like so:

```bash
root@fedora-server ~# dnf -y install dovecot
```

On Debian-like systems, as Ubuntu, Dovecot's IMAP and POP3 functionality is provided in two separate packages: dovecot-imapd and dovecot-pop3d, respectively. They can be installed by using Advanced Packaging Tool (APT) like so:

```bash
master@ubuntu-server:~# sudo apt-get -y install dovecot-imapd dovecot-pop3d
```

During the package installation on Debian-based distros, you will be prompted to create self-signed certificates for IMAP and POP3 over SSL/TLS. Select Yes when prompted. You will also be prompted for the commonName of the hostname to use for the self-signed certificate. Input the correct hostname for your system and select Ok to continue.

# Installing Dovecot from Source

Begin by downloading the latest Dovecot IMAP and POP3 server software to /usr/local/src. The latest version can be found at http://dovecot.org/download.html. Once it is downloaded, unpack it as follows:

```bash
@root@server # tar xzvf dovecot-2.2.20.tar.gz
```

This will create a new directory under which all the source code will reside. For the version we are using, you will see a new directory called dovecot-2.2.20. Changed into the directory as follows:

```bash
@root@server # cd dovecot-2.2.20/
```

The defaults with the Dovecot server work well for most installations. If you are interested in tuning the build process, open the makefile (found in the current directory) with an editor and read through it. The file is well documented and shows what can be turned on or off.

As most other enterprise-grade software of its caliber, Dovecot offers you many configurable features that you can turn on or off during the configuration and build process. In addition to the build options, we will enable a couple of simple but important tweaks.

First, we want to make sure the Dovecot server that we build from is able to support secure communication using the OpenSSL libraries. For this, we need to make sure proper libraries (libssl) are available on the system and that the appropriate option is specified during configuration. For Red Hat-like distros as Fedora, CentOS, and RHEL, make sure that the openssl-devel package is installed. And for Debian-based distros like Ubuntu, make sure you have the libssl-dev package. Secondly, we specify a prefix of /usr/local/dovecot to specify the install location for all Dovecot-related files. Let's begin. Configure the build environment with the custom options:

```bash
@root@server docot-2.2.20]# ./configure --with-ssl=openssl --prefix=/usr/local/dovecot
```

# # CHAPTER 20 Post Office Protocol and Internet Mail Access Protocol (POP and IMAP)

Begin the software compilation by running:

```bash
@root@server docot-2.2.20]# make
```

The entire build/compile process might take only a few minutes. Once make completes without any errors, you can install Dovecot under the prefix directory by running:

```bash
@root@server docot-2.2.20]# make install
```

The preceding command will result in Dovecot binaries being installed under the following directories: /usr/local/dovecot/bin, /usr/local/dovecot/sbin, and /usr/local/dovecot/libexec. The executables should be run only by root, ensure you make limited to nonprivileged access to them accordingly.

# Dovecot Configuration Files and Options

Dovecot provides you, the system administrator, with a wide range of configuration options to help you meet the mailing needs of your end users. The software is helpfully modularized; you can easily pick and choose which modules you want to customize.

The primary configuration file for Dovecot is dovecot.conf, which mainstream Linux distro store under /etc/dovecot/. Using an include directive (include conf/*.conf) some Linux doves go further and organize (split) various files that control different aspects of Dovecot under the /etc/dovecot/conf/ subdirectory.

Table 20-1 shows the location and a brief description of some Dovecot configuration files.

| Dovecot Configuration File | Description |
| :--- | :--- |
| /etc/dovecot/dovecot.conf | Dovecot's main configuration file |
| /etc/dovecot/conf/10-auth.conf | Configuration file for the different authentication modules |
| /etc/dovecot/conf/10-mail.conf | Stores mailbox locations and namespaces |
| /etc/dovecot/conf/10-master.conf | Stores options for various Dovecot services |
| /etc/dovecot/conf/90-plugin.conf | Stores plugin-specific settings. |
| /etc/dovecot/conf/10-ssl.conf | Stores SSL-related settings |
| /etc/dovecot/conf/20-imap.conf | Stores IMAP-specific configuration options |
| /etc/dovecot/conf/20-pop3.conf | Stores POP3-specific configuration options |
