# 274

# Chapter 19 • System Monitoring

```
# The authpriv file has restricted access.
authpriv.*                                     /var/log/secure
```

```
# Log all the mail messages in one place.
mail.*                                            /var/log/maillog
```

```
# Everybody gets emergency messages, plus log them on another
# machine.
  *.emerg
```

```
# Save mail and news errors of level err and higher in a
# special file.
uucp,news.crit                                 /var/log/spooler
```

Any line with a # in front of it is ignored and is a comment. Each line is an entry and consists of two fields. The first field lists the events to monitor. The second field lists what to do when that event has occurred.

Each event is in two parts, separated by a period. The first part is the facility, or type of program generating the event. The second part is the priority or severity of the event, ranging from debug to emerg.
There are twenty facilities available:

+   * auth
"* auth-priv
"* cron
"* daemon
"* kern
"* lpr
"* mail
"* mark
"* news
"* syslog
"* user
"* uucp
"* local0 through local1

There are eight priorities available:

+   * debug
"* info"