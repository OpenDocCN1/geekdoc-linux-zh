# 2.13.4 Fortify sendmail to Resist DoS Attacks

> DANGER LEVEL

There are many DOS attacks that simply flood the system with packets, called packet storms. There are others that are intended to run a system out of resources besides bandwidth, such as disk space or kernel table. A popular way to do this is to send you massive amounts of junk e-mail to fill your disk and waste your CPU time, process table slots, and so on. Regardless of whatever the goal is to cripple your system or bother your users with phony get-rich-quick schemes, there are to resist.

If mail is sent very rapidly, in the process of forking off a child to handle each piece of e-mail, sendmail may run the system out of processes. This is because sendmail does not wait for one to finish processing a piece of e-mail before starting the next, and next, etc. Sendmail. recommends the variable values shown in Table 2.4 as a starting point in tuning your recommendations to be more resistant to DoS and spammer attacks. Most or all of these recommendations will be applicable to later versions of sendmail too. These values should be set in /etc/sendmail.mc. If a "M4" variable listed, say confMIN_FREE_BLOCKS, is not already in the /etc/sendmail.mc file, it should be defined similarly to

```
define(`confMIN_FREE_BLOCKS`, `100`)
```

Then issue the following shell command to convert the /etc/sendmail.mc file into the /etc/sendmail.cf

```
m4 /etc/sendmail.mc > /etc/sendmail.cf
```

Sendmail may be restarted so that it uses the new values. On Red Hat and its progeny, this is done with the following command. On other systems, such as Slackware, a system reboot is an easy way to restart sendmail; sending a HUP signal and issuing the sendmail invocation that is used in /etc/rc.d/rc.M(found with grep) is an alternative.

/etc/rc.d/init.d/sendmail restart

Many more sendmail configuration improvements are addressed in “Sendmail” on page 122.