# PART V

associated with that variable is on the right. The command is issued without any parameters. Hence, typing `env` might get you a list similar to this one:

```
```text
svr01: /home/dpitss$ env
HOSTNAME=svr01.mk.net
LOGNAME=dpitts
MAIL=/var/spool/mail/dpitss
TERM=vt100
HOSTTYPE=i386
PATH=/usr/local/bin:/usr/bin:/bin:.:/usr/local/java/bin
HOME=/home2/dpitss
SHELL=/bin/bash
LS_OPTIONS=--8bit --color=tty -F -T 0
PS1=h: \w$
PS2=>
MANPATH=/usr/local/man:/usr/man/preformat:/usr/man:/usr/lib/perl5/man
LESS=-IM
OSTYPE=Linux
SHLVL=1
```
```

# ex

ex is a symbolic link to the `vim` editor. In this mode, the `vim` editor emulate the ex line editor.

# fax

Use fax to create, transmit, receive, display, or print a fax. This complex shell script is the driver program for the `efax` software package and provides an easy-to-use way to send or receive fax documents under Linux.

# faxq

Use `faxq` to list faxes in the fax-sending queue. This program is part of the `mgetty+sendfax` software package for allowing Linux logins and fax transmission and reception.

# faxrm

Use `faxrm` to delete faxes in the sending queue. You can use this program, part of `mgetty+sendfax`, to delete faxes waiting to be sent.

# faxrunq

`faxrunq` sends spooled faxes from the fax queue. This program, run by the `root` operator or process, sends faxes waiting in the fax queue, usually the `/var/spool/fax` directory.