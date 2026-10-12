
uucico.*: refused connect from .*
tftpd.*: refused connect from .*
login.*: *LOGIN FAILURE.* FROM .*root
login.*: *LOGIN FAILURE.* FROM .*guest

Most of the messages in this file are used to match log messages that result from someone probing your system with the Internet Security Scanner (ISS). ISS is a tool that can scan a set of IP addresses for potential security weaknesses. Though most of the security holes ISS checks for have been plugged over time, these log messages alert you to the fact that someone is checking the security of your system.

The *debug* and *wiz* keywords shown in the previous file will catch attempts by ISS to access *wiz* and *debug* services from the sendmail service. Likewise, *VRFY* is a command that ISS sends to requests of the sendmail service to ask for different user names. Other keyword phrases shown in the previous example match failed attempts to connect using different Linux network services (such as *rlogin*, *rshd*, *sendmail*, *uucico*, and so on).

## logcheck.ignore

Keywords in the /etc/logcheck*/logcheck.ignore file are used to find log messages that should be excluded (that is, ignored) by LogSentry and will therefore not appear in e-mail summaries. The keywords in this file reduce the number of log messages that are e-mailed to the administrator, making it easier to find the real problems. The following are some examples of keywords from the logcheck.ignore file.

cron.*CMD
cron.*RELOAD
cron.*STARTUP
ftp-gw.*: exit host
ftp-gw.*: permit host
ftpd.*ANONYMOUS FTP LOGIN
http-gw.*: exit host
http-gw.*: permit host
identd.*Successful lookup
identd.*from:
named.*Response from

Most of the entries in this file are used to match messages that represent the normal operation of various system services. The keywords shown in the previous example represent normal processing of *cron*, *ftp*, *http*, *identd*, and *named* features.

Notice that all of the keyword phrases shown in the preceding example include an asterisk (*). Wildcard. If you add your own keywords to this file, using asterisks and other wildcards can help you be specific about the log messages you exclude.

## logcheck.violations

There are certain words that imply negative behavior occurring on your computer. Though these words may not be associated with any particular attack, LogSentry notes messages containing these words and displays them under the following heading and e-mails them to the system administrator:

Security Violations
=----------------

The following is an example of some of the keywords that appear in the `logcheck.violations` file:

ATTACK
BAD
DEBUG
FAILURE
ILLEGAL
REFUSED
denied
failed
unapproved
attackAlert

Adding your own keywords to the file can help flag log messages that may be of particular concern for your computer. For example, you can add keywords that represent improper use of services that are not standard Linux features but can be accessed from the network.

## logcheck.violations.ignore

Use the `logcheck.violations.ignore` file to exclude messages that were matched from the `logcheck.violations` file, but are known to not represent security problems. By default, only the following entry is contained in this file:

stat=Deferred

The previous keyword causes LogSentry to ignore log messages from sendmail that represent e-mail messages that haven't been sent because the receiving server was temporarily unavailable. As you use LogSentry, you are likely to repeatedly encounter certain log messages that represent no security threat. Add keywords here (as specific as possible) to exclude those messages from appearing continuously in e-mail messages from LogSentry.

## Modifying syslog

The syslog service gathers the log messages of system activity that are used by LogSentry. Fedora, as well as most other Linux and UNIX systems, comes with syslog installed and operational by default. You can modify the `/etc/syslog.conf` file to tailor the behavior of `syslog` to best suit the way you use your system.

The syslog service is part of the `sysklogd` software package and is started automatically from the `/etc/init.d/syslog` start-up script. After that script has been run on your system, two daemon processes should be active on your system: `syslogd` and `klogd`. To see if they are running, type the following:

```bash
# ps ax | grep log
```

The /etc/syslog.conf file contains information that defines which activities are logged, and from which system. LogSentry monitors three of the log files created by syslog (in the /var/log directory): messages, secure, and maillog. The following lines in the /etc/syslog.conf file instruct syslog to create those log files:

* .info,mail.none;news.none;authpriv.none;cron.none /var/log/messages
* authpriv.* /var/log/secure
* mail.* /var/log/maillog

Services on your Fedora system produce messages of different levels. Message levels, from most critical to least critical, are listed in Table 14-4.

### Table 14-4: Message Levels

| Level | What It Means |
| :--- | :--- |
| debug | Detailed processing information |
| info | Purely informational |
| notice | Important, but not an error |
| warning | Potential error |
| err | Error condition |
| crit | Critical |
| alert | Immediate action needed |
| emerg | System unusable |

The line shown in the example indicates that all messages from the info level (* .info) and above are logged to the /var/log/messages file. However, messages of types mail, news, authpriv, and cron are excluded because they are sent to other log files. All authpriv (authpriv.*) messages are logged to the /var/log/secure file. mail messages (mail.*) are all logged to the /var/log/maillog file.

With this default configuration of syslog, LogSentry should catch all major security-related activities. There are a few situations, however, where you may want to modify the /etc/syslog.conf file. For example, if you are receiving a lot of Log messages for a particular type of service (such as ppp if you are having trouble with a dial-up connection), you may consider directing messages for that service to its own log file. Then, if LogSentry uncovers a problem, it's easier to go through only that log file for those messages relating to the problem service.

Another temporary change you may consider is if you need to debug a problem with your system. Changing * .info to * .debug temporarily can give you more details on a problem. (Make sure to change it back later, or `syslog` will chew up too much system resources.) After making changes to your `syslog` service, run `killall -HUP syslogd` to have the changes take effect.

## Using Password Protection

Passwords are the most fundamental security tool of any modern operating system and consequently, the most commonly attacked security feature. It is natural to want to choose a password that is easy to remember, but very often this means choosing a password that is also easy to guess. Crackers know that on any system with more than a few users, at least one person is likely to have an easily guessed password.

By using the “brute force” method of attempting to log in to every account on the system and trying the most common passwords on each of these accounts, a persistent cracker has a good shot of finding a way in. Remember that a cracker will automate this attack, so thousands of login attempts are not out of the question. Obviously, choosing good passwords is the first and most important step to having a secure system.

Here are some things to avoid when choosing a password:

- Do not use any variation of your login name or your full name. Even if you use varied case, append or prepend numbers or punctuation, or type it backwards, this will still be an easily guessed password.
- Do not use a dictionary word, even if you add numbers or punctuation to it.
- Do not use proper names of any kind.
- Do not use any contiguous line of letters or numbers on the keyboard (such as “qwerty” or “asdfg”).

## Choosing good passwords

A good way to choose a strong password is to take the first letter from each word of an easily remembered sentence. The password can be made even better by adding numbers, punctuation, and varied case. The sentence you choose should have meaning only to you, and should not be publicly available (choosing a sentence on your personal Web page is a bad idea). Table 14-5 lists examples of strong passwords and the tricks used to remember them.

### Table 14-5: Ideas for Good Passwords

| Password | How to Remember It |
| :--- | :--- |
| Mrcl7yo! | My rusty car is 7 years old! |
| 2emBp11b | 2 elephants make BAd pets, 1 is better |
| ItMc?G1b | Is that MY coat? Give it back |
