
# CHAPTER 19 Simple Mail Transfer Protocol (SMTP) 503

**Mail transport agent (MTA)** Handles the process of getting the mail from one site to another. Sendmail and Postfix are popular examples of MTA.

**Mail delivery agent (MDA)** Responsible for distributing and sorting received messages on the local machine to the appropriate user mailbox. The Procmail program is a popular solution for handling the actual mail delivery (MDA) component of e-mail. This is because of its advanced filtering mechanism, as well as its secure design from the ground up.

> NOTE Some mail systems integrate all three components. For example, Microsoft Exchange Server integrates the MTA and MDA functionalities into a single system. (If you consider the Outlook Web Access interface to Exchange Server, it is also an MUA.) IBM Domino also works in a similar fashion. Postfix, on the other hand, works as an MTA only, passing the task of performing local mail delivery to another external program. This delineation of tasks allows the use of other tools or solutions for tasks such as delivering mailbox storage mechanisms.

![](img/9f6657924397c33f088db5321b751a83_519_0.png)

# Installing the Postfix Server

We chose the Postfix mail server in this discussion for its ease of use and because it was written from the ground up to be simpler than Sendmail. (The author of Postfix also argues that the simplicity has led to improved security.) Postfix provides most of the functionalities Sendmail program has—in fact, the typical installation procedure for Postfix is to be a drop-in replacement for Sendmail binaries completely.

Postfix is the default mail server program on most modern Linux distros. In the following sections, we show how to install Postfix using the built-in package management (Red Hat's RPM or Debian's dpkg) mechanism of the distribution. This is the recommended method. We also show how to build and install the software from your source code.

# Installing Postfix via DNF in Fedora, CentOS, or RHEL

To install Postfix via DNF on Fedora, CentOS, or RHEL distros, simply use the dnf package manager as follows:

```
[root@fedora-server]# dnf -y install postfix
```

Once the command runs to completion, you should have Postfix installed. You can use the chkconfig utility to make sure your Postfix service starts automatically during boot. Type:

```
[root@fedora-server]# chkconfig postfix on
```

# Linux Linux Administration: A Beginner's Guide

On systemd-enabled distros, the equivalent command is:

```
[root@fedora-server]# systemctl enable postfix
```

Finally, you can flip the switch and actually start the Postfix process. With a default configuration, it won't do much, but it will confirm that the installation worked as expected:

```
[root@fedora-server]# service postfix
[root@fedora-server]# systemctl start postfix.service
```

> TIP You may find yourself inheriting or managing an existing Red Hat-based distro that has both popular MTAs (Sendmail and Postfix) installed or you may decide to install a new MTA. If you switch the mail subsystem that is running on such a system from Sendmail to Postfix, you can use alternatives to switch the default MTA. Run the command like so: alternatives --config

# Installing Postfix via APT in Ubuntu

Postfix can be installed in Ubuntu using the Advanced Packaging Tool (APT). Ubuntu, unlike Linux distributions, does not ship with any MTA preconfigured and you will need to install and set up one. To install Postfix in Ubuntu, run this command:

```
master@ubuntu-server~$ sudo apt-get -y install postfix
```

You will be prompted to select your Postfix server configuration type during the installation process. The available types are:

- No configuration: This option will leave the current configuration unchanged.
- Internet with smarthost: Mail is sent and received directly via SMTP.
- Outgoing mail is sent using a smarthost.
- Satellite system: All mail is sent to another machine, called smarthost, for delivery.
- Local only: The delivered mail is for local users. The system does not need network connectivity for this option.

The install process will also create the necessary user and group accounts that Postfix needs.

# Installing Postfix from Source Code

It is likely that your Linux distribution has not yet packaged the latest version of Postfix and therefore it is not available in the repository. If you need the latest version for whatever reason (new features, bug fixes, and so on), you will need to obtain and build the software from source. By downloading the source code from www.postfix.org, the stable version of postfix that we use in this section is postfix-3.0.2.tar.gz. Once you have the file downloaded, use the tar command to update the contents:

```
[root@server src]# tar xvzf postfix-3.0.2.tar.gz
```

Once Postfix is unpacked, change into the postfix-3.0.2 directory and run the make command, like so:

```
[root@server src]# cd postfix-3.0.2
[root@server src]# make
```

The complete compilation process will take a few minutes but should work. Please note if the compile step fails with an error unable to find "db.h" or any "db" reference, there is a good chance your system does not have Berkeley DB tools installed. Although it is possible to compile Berkeley DB tools it is not recommended as Postfix will fail if the version of DB used in Postfix is different from system libraries. To fix this, install the libdb-devel package and run the make step again. You can install the needed package using dnf as follows:

```
# dnf -y install lib-devel
```

If you already have sendmail installed on the system and want to use Postfix to replace your current Sendmail program, you might want to make a backup of the Sendmail binaries:

```
[root@server -]# mv /usr/bin/sendmail /usr/bin/sendmail.old
[root@server -]# mv /usr/bin/newaliases /usr/bin/newaliases.old
[root@server -]# mv /usr/bin/mailq /usr/bin/mailq.old
```

Now you need to create a user and a group under which Postfix will run. You may find some distributions already have these accounts defined; so the process of adding a user will result in another:

```
[root@server postfix-*]# useradd -M -d /var/spool/postfix -s /sbin/nolog postfix
[root@server postfix-*]# groupadd -r postfix
[root@server postfix-*]# groupadd -r postdrop
```

# Beginner's Guide

You're now ready to execute the make install step to install the actual software. Postfix includes an interactive script that prompts for values of where things should go. Stick to the defaults by simply pressing the ENTER key at each prompt.

```
[root@server postfix-3.*]# make install
```

With the binaries installed, it's time to deal with configuring the service for automatic startup and shutdown.

The version of Postfix includes a nice shell script that handles the start-up and shutdown process. For the sake of consistency, you can wrap it into a standard start-up script that can be managed via chkconfig (or other startup mechanism). Using the techniques you learned from Chapter 6, you can create a shell script called /init.d/postfix. You can use the following code listing for the postfix script:

```
#!/bin/sh
# Postfix
# chkconfig
  35 99 01
#
  /etc/init.d/functions
 [ -f /usr/sbin/postfix ] || exit 0
# See how we were called.
case "$1" in
start)
  echo "Starting postfix:"
  /usr/sbin/postfix start
  echo "done"
  touch /var/lock/subsystems/postfix

stop)
  echo -n "Stopping postfix:"
  /usr/sbin/postfix stop
  echo "done"
  rm -f /var/lock/subsystems/postfix

*)
  echo "Usage: postfix start|stop"
  exit 1
esac
exit 0
```

With the script in place, double-check that its permissions are correct with a quick chmod:

```
[root@server postfix-3.*]# chmod 755 /etc/init.d/postfix
```
