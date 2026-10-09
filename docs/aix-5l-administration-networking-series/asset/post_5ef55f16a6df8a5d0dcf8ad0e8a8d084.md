
## Secure Attention Key

The Secure Attention Key (SAK) feature of the Trusted Computing Base ensures that only trusted commands are available to a user logging in to the system over a serially attached terminal. Note that SAK is not available for sessions over the network.

To set up SAK, root must modify the /etc/security/login.cfg file and add sak_enabled=true to the entry of each TTY port that SAK is to be available on. Once that is done, a user who is authorized to use SAK and is logging on via that TTY can invoke the trusted communication path by entering the key sequence CTRL-X CTRL-R. That key sequence should be typed before the user name and password are entered.

After the user invokes SAK and then logs in to the system as usual, the trusted shell (tsh) is started for that user instead of the usual shell. The trusted shell is similar in syntax to the Korn shell (ksh), with a few key differences:

- Only trusted programs (those marked as trusted by TCB) may be executed.
- Functions and alias definitions are not supported.
- The IFS and PATH environment variables cannot be redefined.
- The history mechanism is not available.
- The only profile executed is /etc/tsh.profile; shell configuration scripts in the user’s home directory are not run.

## The Auditing Subsystem

When discussing security, it is often not sufficient to check periodically to see if someone left the barn door open. It is much better to be actively notified that the door has been opened. AIX 5L includes an auditing subsystem that can track and log any number of predefined or custom system activities. By enabling auditing, you can easily monitor a wide range of security-related events. Note that, by default, auditing is disabled. The log files associated with auditing can grow rapidly, and the overhead created by the auditing process can have a slight but measurable impact on system performance.

### Audit Categories

The AIX auditing subsystem provides four general categories that may be monitored and logged.

### Events

An *event* is a system activity, usually defined at the system call level. Every time a command is executed, a number of system calls are made. Each of those system calls corresponds to an event and will be recorded by the auditing process. The name of the event, the command that caused the event, the user executing the command, the date and time, and the success or failure of the event will all be logged.

### Classes

A *class* is simply a group of events. There can be one or more events in a class, and grouping related events makes administration and interpretation of the auditing logs easier. Note that AIX is limited to 31 classes (plus the ALL class, which includes all system events).

### Objects

An *object* is a file. When a specific file is defined as an audited object, all attempts at reading, writing, and executing the file will be recorded.

### Users

The *user category* defines the specific events and classes to be audited for a particular user account. The number of events recorded can be increased or decreased in accordance with the perceived trustworthiness of a user.

### BIN Versus STREAM

The auditing subsystem can be run in two modes, BIN or STREAM. Each mode has its advantages, and both can be used if desired.

The BIN, or binary mode, sends auditing data to two alternating “bins” and writes its data to the file `/audit/trail` in a compact, binary format. It is best suited for long-term storage of auditing records.

To convert this file into a readable format, the **auditpr** command must be run:

```sh
# /usr/sbin/auditpr < /audit/trail
```

The STREAM mode writes audit records to the file `/audit/stream.out`, processing the audit information as it is generated. This file is in plain text and can be read as it is written. Note, though, that this file is erased each time auditing is restarted. Thus, STREAM mode is best suited for real-time monitoring of audited events.

### Auditing Configuration

All configuration files for the auditing subsystem are located in the `/etc/security/audit` directory.

```sh
# ls -l /etc/security/audit
total 56
-rw-r----- 1 root audit     37 Sep 30 1997 bincmds
-rw-rw---- 1 root audit   2116 Nov 06 16:37 config
-rw-rw---- 1 root audit  12236 Nov 06 22:00 events
-rw-rw---- 1 root audit    340 Sep 30 1997 objects
-rw-r----- 1 root audit     54 Sep 30 1997 streamcmds
```

The `/etc/security/audit/config` file is arranged into stanzas, each defining an aspect of the auditing subsystem’s behavior. The start stanza sets the mode that auditing will run in when started—BIN, STREAM, or both:

```ini
start:
  binmode = on
  streammode = off
```

The next two stanzas define locations and other behaviors of each of the two modes. For the BIN mode, the names and locations of the two bins and the output file may be defined. The STREAM stanza contains only the location of the file containing the audit stream processing command.

```ini
bin:
  trail = /audit/trail
  bin1 = /audit/bin1
  bin2 = /audit/bin2
  binnsize = 10240
  cmds = /etc/security/audit/bincmds

stream:
  cmds = /etc/security/audit/streamcmds
```

The various classes are detailed in the next stanza. By default, ten classes are defined in the following format; you are free to modify these existing classes or add your own.

```ini
classes:
  general = USER_SU, PASSWORD_Change, FILE_Unlink, FILE_Link, FILE_Rename, FS_Chdir, FS_Chroot, PORT_Locked, PORT_Change, FS_Mkdir, FS_Rmdir
```

The final stanza, `users`, contains the names of users that are to be audited, with the specific classes to audit for those users.

```ini
users:
  root = general
```

Users may be selected for auditing by manually adding them to this file, or by selecting the audit classes to monitor in appropriate fields of the SMIT **mkuser** or **chuser** screens:

```sh
# smit chuser
    AUDIT classes                    [general,objects,files] *
```

Audit classes assigned to files must be defined in the `/etc/security/audit/objects` file. Each stanza in this file lists the name of the object to be audited, the operation to be audited (read, write, and/or execute), and the event associated with that operation.

```ini
/etc/security/passwd:
    r = "S_PASSWD_READ"
    w = "S_PASSWD_WRITE"
```

### Starting and Stopping Auditing

The auditing subsystem is controlled by the `/usr/sbin/audit` command. After performing the necessary configuration, execute this command:

```sh
# /usr/sbin/audit start
```

The preceding command will start system auditing. If auditing in STREAM mode is requested, note that any previous data in the `/audit/stream.out` file will be cleared. If you want to have auditing active at each system start-up, IBM recommends that the **audit start** command be placed in the `/etc/rc.file`, so that events are monitored early in the start-up process.

To query the status of the auditing subsystem, run the command:

```sh
# /usr/sbin/audit query
```

If auditing is not active, the following information will be printed:

```
auditing off
    bin processing off
    audit events:
            none
    audit objects:
            none
```

If auditing is active, the PID of the auditing process will be displayed, along with a list of the events, classes, and objects being monitored. To stop auditing, execute the command:

```sh
# audit shutdown
```

This command should be added to your /etc/rc.shutdown script to ensure a clean termination of the auditing process. Auditing can be paused and restarted by specifying off and on as arguments to the audit command.

## Additional Security Tools

A tremendous number of open source and free software tools are available for AIX. These tools can help secure your systems and ensure the integrity of the data stored within. Several of the more popular tools are listed in the following sections.

Note that while many of the tools listed are available in a compiled, ready-to-install format, it is a good policy to build programs from the source when possible.

### John the Ripper

One of the most important things that you can do to protect your systems is to help your users develop good password habits. Users may not want this help, but it is critical that they understand the need for it and for the creation of strong passwords to protect their accounts.

John the Ripper is a password-cracking tool. It takes as its input a list of encrypted passwords and tries to determine their unencrypted values. If John the Ripper can determine a user’s password, that password is probably not very strong.

The homepage for John the Ripper is http://www.openwall.com/john/. The latest release of John can be downloaded in source form from that site, or in a compiled LPP format from http://www.build.de/pub/.

### Swatch

Swatch, “The Simple WATCHer,” is a Perl application that continually monitors log files, looking for patterns defined in a configuration file. When the pattern is detected, swatch can perform a number of actions, such as executing a program or e-mailing the detected error to a specified address. Swatch automates the tedious process of constantly reading log files, separating the important entries from the noise.

Swatch can be downloaded from http://eta.cs.colorado.edu/~swatch/. It requires Perl, which is included with AIX 5L.

### Tripwire

Tripwire is a file integrity monitoring tool, available both free and in a commercial version. Along with the features provided by the TCB, Tripwire offers a number of additional features and reporting capabilities. It is also available for a wide variety of platforms, and is thus an excellent solution for heterogeneous data centers. The commercial version provides centralized configuration, monitoring, and reporting. For more information about Tripwire, see http://www.tripwire.com/. Instructions for building the free version of Tripwire on AIX can be found at the IBM eServer
