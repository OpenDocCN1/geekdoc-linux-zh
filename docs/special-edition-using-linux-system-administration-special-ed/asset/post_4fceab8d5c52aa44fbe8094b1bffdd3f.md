
Figure 16.2 illustrates the route a message takes from the mail user agent until it is handed to a mail delivery agent for delivery.

![](img/6c13bcf02a08ad7923caab46f051d96a_334_0.png)

In addition to routing mail, sendmail also receives and delivers SMTP mail and provides for mail aliases.

To receive SMTP mail from the Internet or within the intranet, sendmail is run as a daemon which listens to TCP port 25. sendmail is automatically started at system boot up by the startup scripts in `/etc/rc.d/init.d`. The following code is typical of the code used in `/etc/rc.d/init.d` to start sendmail during the boot process:

```bash
if [ -f /etc/sysconfig/sendmail ] ; then
        . /etc/sysconfig/sendmail
else
        DAEMON=yes
        QUEUE=1h
fi
[ -f /usr/sbin/sendmail ] || exit 0
# See how we were called.
case "$1" in
    start)
        # Start daemons.
        echo -n "Starting sendmail: "
        /usr/bin/newaliases > /dev/null 2>&1
        for i in virtusertable access domaintable mailertable ; do
            if [ -f /etc/mail/$i ] ; then
                makemap hash /etc/mail/$i < /etc/mail/$i
            fi
        done
        /usr/sbin/sendmail $([ "$DAEMON" = yes ] && echo -bd) \
                $([ -n "$QUEUE" ] && echo -q$QUEUE)
        ;;
```

The script first checks whether the file `/etc/sysconfig/sendmail` exists. If it does, it sources its contents. This file sets the values of two environment variables: DAEMON and QUEUE. If DAEMON is set to yes, it means sendmail should run in daemon mode. The value of the QUEUE variable tells sendmail how often it should process the mail queue. For example, if the contents of `/etc/sysconfig/sendmail` is the following:

```
DAEMON=yes
QUEUE=15m
```

then the sendmail program needs to be invoked with two arguments: -bd to indicate that the program should run in daemon mode and listen to TCP port 25 for incoming SMTP mail and -q15m to indicate a queue processing interval of 15 minutes:

```bash
/usr/sbin/sendmail -bd -q15m
```

Prior to starting up the sendmail program, the script runs two other programs, newaliases and makemap.

The program `/usr/sbin/newaliases` is a link to `/usr/sbin/sendmail`. When sendmail is invoked with the program name newaliases it rebuilds the aliases database.

The makemap program creates hash or dbm format database files from sendmail configuration files. The above script calls makemap with the argument hash, which tells it to build the databases in a hash table format. The script checks whether the following text files exist and if they do they are converted to hash table files: virtusertable, access, domaintable, and mailertable.

## SENDMAIL FILES AND DIRECTORIES

The sendmail package uses numerous files and directories for configuration and processing purposes:

- `/usr/sbin/sendmail`
- `/etc/sendmail.cf`
- `/usr/bin/newaliases`
- `/usr/bin/hoststat`
- `/usr/bin/purgestat`
- `/var/spool/mqueue`
- `/usr/bin/mailq`
- `/var/spool/mqueue/.hoststat`
- `/etc/aliases`
- `/usr/lib/sendmail.hf`
- `/etc/sendmail.st`

We will discuss each of these files in turn.

### `/usr/sbin/sendmail`

In Linux the sendmail executable program is located in the `/usr/sbin` directory. It is setuid root, which means that regardless of who launches the program, it runs as the root user. For security reasons the directories `/`, `/usr`, and `/usr/sbin` should be owned by root, and have the mode 755. This means that only the root user can change the contents of these directories.

This will prevent the replacement of the sendmail binary by a malicious user who can then take advantage of the fact that sendmail always runs as the root user to compromise system security.

### `/etc/sendmail.cf`

When sendmail starts it reads its configuration from the file `/etc/sendmail.cf`. The location of the sendmail.cf file is hard coded into the sendmail binary file. For this reason, there are only two ways to change the location of the sendmail configuration file:

- Move the file to a new location and create a link back to `/etc` using the command:

  ```bash
  # ln -s <new location of configuration file> /etc/sendmail.cf
  ```

- Recompile the sendmail package after altering the sendmail source code.

### `/usr/bin/newaliases`

The newaliases command is not a distinct file but rather is a link to the sendmail executable. If, for some reason, the newaliases link does not point to your sendmail executable, you can re-create the link as follows:

```bash
# rm -f /usr/bin/newaliases
# ln -s /usr/sbin/sendmail /usr/bin/newaliases
```

When sendmail is invoked as the newaliases command, it has the effect of starting sendmail with the -bi argument which causes sendmail to rebuild the aliases hash table or db file.

The actual role of newaliases is discussed earlier in this chapter in the section on mail aliases.

### `/usr/bin/hoststat`

The hoststat command is not a distinct file but rather is a link to the sendmail executable in the same way that newaliases is. If, for some reason, the hoststat link does not point to your sendmail executable, you can re-create the link as follows:

```bash
# rm -f /usr/bin/hoststat
# ln -s /usr/sbin/sendmail /usr/bin/hoststat
```

When sendmail is invoked as the hoststat command, it has the effect of causing sendmail to display a list of the last mail transaction with every remote host that has been communicated with.

For the hoststat command to work, you must perform several preparatory steps:

1. The `HostStatusDirectory` option must be set in the sendmail.cf file.
2. A `.hoststat` directory must be created in the `/var/spool/mqueue` directory with the command:

   ```bash
   # mkdir /var/spool/mqueue/.hoststat
   ```

### `/usr/bin/purgestat`

The purgestat command is not a distinct file but rather is a link to the sendmail executable in the same way that newaliases is. If, for some reason, the purgestat link does not point to your sendmail executable, you can re-create the link as follows:

```bash
# rm -f /usr/bin/purgestat
# ln -s /usr/sbin/sendmail /usr/bin/purgestat
```

When sendmail is invoked as the purgestat command, it flushes all information in the HostStatusDirectory directory tree.

### `/var/spool/mqueue`

The `/var/spool/mqueue` directory is the default mail queue directory for sendmail. This directory should be owned by root and have permission mode set to 700.

The Q entry in the sendmail.cf file defines the location of the sendmail queue directory. The default value of this entry is `/var/spool/mqueue`. Normally there is no need to change this, unless you have a very unusual sendmail configuration.

As it operates, sendmail creates mail files in `/var/spool/mqueue` with prefixes. These prefixes have specific meanings as outlined in Table 16.1.

| Prefix | Description |
| --- | --- |
| lf | Lock files |
| qf | Control files for messages |
| df | Data files for messages |
| tf | Temporary versions of control files used during rebuilding of queue files |
| xf | Transcript files for the current session |

### `/usr/bin/mailq`

The mailq command is not a distinct file but rather is a link to the sendmail executable in the same way that newaliases is. If, for some reason, the mailq link does not point to your sendmail executable, you can re-create the link as follows:

```bash
# rm -f /usr/bin/mailq
# ln -s /usr/sbin/sendmail /usr/bin/mailq
```

When sendmail is invoked as the mailq command, sendmail launches with the -bp argument which causes sendmail to display the current contents of the `/var/spool/mqueue` directory.

### `/var/spool/mqueue/.hoststat`

If you enable the `HostStatusDirectory` option in sendmail.cf, the default value of the entry is `/var/spool/mqueue/.hoststat`. This directory contains one file for every host that sendmail has communicated with recently which is used by the hoststat command to display the last transaction with each host.

### `/etc/aliases`

Mail aliases are stored in the file `/etc/aliases`. A sample aliases file is usually created when sendmail is first installed. The sample file is also provided with the sendmail source distribution. The aliases file contains required aliases as well as custom aliases for your site. Required aliases include an alias for the postmaster email address.

If you are installing a sendmail system from scratch, you should copy the aliases file from the sendmail source distribution's `lib/aliases` directory to `/etc/aliases` and then edit it to suit the needs of your site.

The newaliases program converts the `/etc/aliases` text file to a hash file or dbm database format. sendmail uses the database version of the file instead of the actual `/etc/aliases` text file. The default format for the aliases database is the ndbm format. The path to the aliases file is defined by the AliasFile entry in sendmail.cf file.

### `/usr/lib/sendmail.hf`

The sendmail.hf file is the help file used by the SMTP HELP command. The path to this file is set by the HelpFile option in sendmail.cf file.

### `/etc/sendmail.st`

If you create an empty `/etc/sendmail.st` file using the following command:

```bash
touch /etc/sendmail.st
```

then sendmail will collect statistics about your mail traffic. The file itself does not change or grow in size but simply indicates to sendmail to start collecting statistics. The path to this file is set by the S entry in the sendmail.cf file.

## The sendmail.cf Configuration File

The sendmail configuration file is `/etc/sendmail.cf`. The location of this file is compiled into the sendmail executable. sendmail reads it every time it starts.

> **Tip**
>
> If you want to configure sendmail quickly and get it up and running, read the next section "Configuring sendmail with m4" first, and later come back to this section to learn the gory details of sendmail's configuration file.
