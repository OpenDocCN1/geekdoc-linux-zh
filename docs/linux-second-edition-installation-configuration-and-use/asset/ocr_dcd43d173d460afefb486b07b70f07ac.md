# sendmail AND fetchmail OFFLINE CONFIGURATION 365

used to answer emails automatically ('on holiday'), to sort emails into different files, and so on. More information can be found in the extensive text and in the Offlinemailing Mini-HOWTO.

A powerful alternative to procmail is deliver expects the messages to be delivered in the standard input channel. To make these messages arrive in the mailbox of the addressee, the name must be specified as a parameter (deliver name).

# Script for automatic mail delivery via PPP

The next step is now to coordinate PPP connection establishment and sending and receiving of email by means of a central script. This allows you to use your local email program on your computer (be it Pine or Neptune) whenever you want. If you want to send your own email messages or check new mail has arrived, you execute the offlinemail program introduced below as root.(The script cannot be executed by normal users, since the commands for establishing a PPP connection require root privileges).

The program code for offlinemail is surprisingly short. As soon as the script is running satisfactorily, you should delete the -v options, which provide additional information during the test phase. The call to sendmail is needed, in spite of the active sendmail, to use the short period when the Internet connection is open for immediate transmission of temporarily stored emails. (Depending on the configuration, sendmail checks only once every 15 minutes whether temporarily stored emails can be sent).

```
#! /bin/sh
# offlinemail
# ppp-on
if . /ppp-on; then
echo "send mail"
/usr/sbin/sendmail -q -v
echo "read mail"
fetchmail -v
else
echo "error"
fi
./ppp-off\```
```

The script can only be executed by root. Thus ..fetchmailrc must be located in the home directory of root. To ensure that email is nevertheless delivered to hofer and not to root, you must insert the keywords is hofer in .fetchmailrc.

The following lines show how offlinemail works in practice:

```
root@offlinemail
dialing .. trying to establish ppp .............. ppp is up!
send mail
Running JAA00712 (sequence 1 of 1)
hof@jupiter.galactic.network ... Connecting to provider.de via relay...
220 provider.de SMTP/smap Ready.
>>> HELO jupiter.galactic.network```
```