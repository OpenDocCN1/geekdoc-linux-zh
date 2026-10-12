# **LINUX VOICE MODEM SUPPORT**

If you are the fortunate owner of a vgetty-supported voice modem, such as the Elsa MicroLink 56K Internet modem, you can download, install, and use the *vgetty* command to monitor the modem and have your system provide voice, data, and fax services. Edit the file /etc/mgetty+sendfax/voice.conf, create your answering voice messages in /var/spool/voice/messages, and then use a vgetty /etc/inittab entry such as
S0:345:respawn:/sbin/vgetty try52

To host voice messages, you will need to use the *wavtopvf* and *pvfspeed* commands to convert your voice sound files into a format used by the modem, like this:

```
# wavtopvf mmessage.wav mmessage.pvf ; pvfspeed -S 7200 mmessage.pvf ; pvftormd Elsa 4 >mmessage.rmd
```

To play your outgoing message (which should be stored in /var/spool/voice/messages with the name *standard*.rmd), use the following command line (needed to convert sound formats so we can play it):

```
# rmdtopvf mmessage.rmd ; pvfspeed -s 8000 ; pvftobasic >/dev/audio
```

This technique can be used to listen to any messages left by callers (which end up in the /var/spool/voice/incoming directory).

Browse to http://alpha.greene.net/vgetty/ to download *vgetty* and its documentation. Also, look at the *Linux Answering machine HOWTO* at http://linuxxinda.virtualave.com/iamhowto.html.

The next step is to create a user named *ppp* and then to assign a password to it. Although it is possible to allow remote users to log in and start *pppd* from the command line (assuming that you have set *pppd* to SUID root), the *pppd* daemon can be started automatically by creating a short shell script and then assigning the shell script to the user for the default shell in the user's /etc/passwd entry, like this:
ppp:x:500:500::/home/ppp:/usr/local/bin/dopppdoppp
Made executable with *chmod +x* it would contain the following:
exec /usr/sbin/pppd -detach

Using this approach, *pppd* will start automatically after the *ppp-dial-in* user connects and logs in (perhaps using the *ppp-on* scripts or other clients on the remote computer). The file options under the /etc/ppp directory should include general dial-in options for PPP service on your system, and specific options files (such as *options.ttyS1* for this example) should be created for each enabled dial-in port. For example, /etc/ppp/options could contain

```
asyncmap 0
netmask 255.255.255.0
proxyarp
lock
crtscts
modem
```