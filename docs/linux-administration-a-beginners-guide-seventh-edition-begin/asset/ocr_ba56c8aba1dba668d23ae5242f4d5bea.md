# 504 Linux Administration: A Beginner's Guide

On systemd-enabled distros, the equivalent command

```
[root@fedora-server ~]# systemctl enable postfix.service
```

Finally, you can flip the switch and actually start the Postfix process. With a default configuration, it won't do much, but it will confirm that the installation worked as expected:

```
[root@fedora-server ~]# service postfix
```

On systemd-enabled distros, the equivalent command is

```
[root@fedora-server ~]# systemctl start postfix.service
```

> TIP You may find yourself inheriting or managing an existing Red Hat-based distro that has both of the popular MTAs (Sendmail and Postfix) installed or you may decide to install a new MTA. If you switch the mail subsystem that is running on such a system, from Sendmail to Postfix, you can use the alternatives to switch the default MTA provider. Run the command like so and the prompts:
# alternatives --config mta

# Installing Postfix via APT in Ubuntu

Postfix can be installed in Ubuntu using Advanced Packaging Tool (APT). Ubuntu, unlike Linux distributions, does not ship with any MTA software preconfigured and running. You will need to install and set up one. To install the Postfix MTA in Ubuntu, run this command:

```
master@ubuntu-server:~$ sudo apt-get -y install postfix
```

+   You will be prompted to select your Postfix mail server configuration type during the installation process. The available types are
* No configuration This option will leave the current configuration unchanged. Mail is sent and received directly via SMTP.
* Internet with smarthost Mail is received directly via SMTP or by running a utility like fetchmail. Outgoing mail is sent using a smarthost.
* Satellite system All mail is sent to another machine, called a smarthost, for delivery.
* Local only The only delivered mail is for the local users. The system does not need any sort of network connectivity for this option.

We will use the first option, No configuration, on our sample Ubuntu server. The install process will also create the necessary user and group accounts that Postfix needs.