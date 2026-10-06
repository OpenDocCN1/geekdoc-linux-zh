Motif Configuration (motif.conf) The Google Voice Service utilizes the XMPP protocol for signaling and supports XMPP clients connecting to its servers. The Asterisk Motif driver supports XMPP, Jingle, Google, and Google Talk implementations and are configured with the motif.conf file. The purpose here is to let your Asterisk system know that you intend to utilize Google Voice Service for communication and that calls will originate or terminate in the context defined in motif.conf. (The default motif.conf file contains descriptions of the configurable options, but these are beyond the scope of this chapter).

Let's start by backing up sample configuration file, creating a new, empty version, and then modifying its ownership and permissions:

```
[root@server ~]## mv /etc/asterisk/motif.conf.{original}
[root@server ~]## touch /etc/asterisk/motif.conf
[root@server ~]## chown asterisk.etc/asterisk/motif.conf
[root@server ~]## chmod 640 /etc/asterisk/motif.conf
```

Edit the new and empty /etc/asterisk/motif.conf and add the following contents:

```
[root@server asterisk]# vi /etc/asterisk/motif.conf

[google]
context=pstn-in
disallow=all
allow=ulaw
connection=google
```

The explanations for these settings are as follows:

+   [google]
Section title. This name is arbitrary, and will be referred to in the xmpp.conf file and in the dialplan to establish outgoing calls.
context=pstn-in
The name specified here, which is arbitrary, determines where incoming calls will enter the dialplan when they arrive on the context associated with this section.
connection=google
There are three different transports and protocol derivatives supported by chan-motif. They are, in order of preference: Jingle by ICE-UDP, Jingle, and Google-V1, referred to as ice-udp, google, and google-v1, respectively.

> NOTE Calling in Google Voice requires the G.711 ulaw codec.