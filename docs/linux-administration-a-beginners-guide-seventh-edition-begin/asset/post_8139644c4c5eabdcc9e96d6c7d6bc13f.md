
# Linux Administration: A Beginner's Guide

Connect to the Asterisk console and reload the SIP configuration:

```
server*CLI> sip reload
Reloading SIP
```

> TIP You can quickly connect to the running Asterisk process and execute Asterisk commands without always connecting to the native Asterisk console. To do this, you would use the -rx option followed by the subcommand that you want to execute.

For the full command to run the sip reload sub-command is
# asterisk -rx "sip reload"
And, to show the current dialplan, you would run
# asterisk -rx "dialplan show"

From the Asterisk console, list the available SIP endpoints. You would see the two SIP phones that you have configured in the sip.conf file in the console output. You will notice that the Host is ("Unspecified") and the status is UNKNOWN to indicate that the device is offline.

```
server*CLI> sip peers
```

| Name/username | Host | Dyn | Forport | Comedia | ACL | Port | Status | Description |
|---|---|---|---|---|---|---|---|
| 1001 | (Unspecified) | D | Auto | (No) | No | 0 | UNKNOWN |
| 1002 | (Unspecified) | D | Auto | (No) | No | 0 | UNKNOWN |

2 sip peers [Monitored: 0 online, 2 offline unmonitored: 0 online, 0 offline]

# Dialplan Configuration (extensions.conf)

A stock dialplan ships with the Asterisk package is stored in the /etc/asterisk/extensions.conf file. It contains many parameters/settings in its default and unmodified state; but since these are not needed for this exercise, we will rename or backup the original file and create a new one from scratch:

```
[root@server -]# mv /etc/asterisk/extensions.conf extensions.conf.original
```

After that, create a new empty version of this file and modify its ownership and permissions:

```
[root@server -]# touch /etc/asterisk/extensions.conf
[root@server -]# chown asterisk.asterisk /etc/asterisk/extensions.conf
[root@server -]# chmod 640 /etc/asterisk/extensions.conf
```

Use text editor to edit the new and /etc/asterisk/extensions.conf file and add the following contents:

```
[general]
;
[internal]
; Dialing between internal phones (extensions) - Alice and Bob
```

![](img/9f6657924397c33f088db5321b751a83_577_0.png)

## Download and Install the X-Lite Smartphone
Follow these steps to obtain and configure the X-Lite softwares on each of the client systems or devices from which you want to run the SIP clients:

- 1. Launch your favorite browser and go to www.counterpath.com/x-lite-download/.
- 2. Click the Download button for the operating system of the computer on which you want to install the softphone.
- 3. Follow the instructions to install the software.
- 4. Launch the X-Lite software.
- 5. Repeat Steps 1–4 on the second system that will be running the X-Lite software and acting as the second extension.

![](img/9f6657924397c33f088db5321b751a83_578_0.png)

## Configure the SIP Extensions
Once you have downloaded and installed the SIP client just described, you can follow the instructions in these next sections to test your basic PBX. First, we'll configure the SIP extensions.

- 1. Set up your SIP accounts. Go to Preferences -> Account Settings.

# CHAPTER 21 Voice over Internet Protocol (VoIP)

- 2. Fill out the screen shown next with the following values:
User ID: 1001
Domain: sip.server.com
Password: herSecret
Display name: Alice

![](img/9f6657924397c33f088db5321b751a83_579_0.png)

- 3. Click OK to save the configuration in the sip.conf file and attempt to connect to the Asterisk server. You will see the following screen:

![](img/9f6657924397c33f088db5321b751a83_579_1.png)

- 4. Upon successfully connecting the SIP client to the server, you might observe following on the Asterisk console:

```
server*CLI> -- Registered SIP '1001' at sip.server.com:5060
```

- 5. Repeat the previous Steps 1-4 to configure the second X-Lite client (Bob). Substitute all the information for Alice (User ID: 1001, Password: herSecret, Display name: Alice) with Bob's correct information (User ID: 1002, Password: hisSecret, Display name: Bob).

Before continue to the next section, you can run the following commands on the Asterisk server to verify the configuration of the software and ensure that they are registered:

```
server*CLI> sip peers
```

| Name/username | Host | Dyn | Forport | Comedia | ACL | Port | Status | Description |
|---|---|---|---|---|---|---|---|---|
| 1001 | 192.168.1.101 | D | Auto | (No) | No | 5060 | OK | Allowed |
| 1002 | 192.168.1.102 | D | Auto | (No) | No | 5060 | OK | Allowed |

2 sip peers [Monitored: 0 online, 2 offline unmonitored: 0 online, 0 offline]

The X-Lite client will show the status as Available.

![](img/9f6657924397c33f088db5321b751a83_580_0.png)

> NOTE The status information may look different on your version of softphones (and hardphones).

Test Scenario: Dial from Alice (Extension 1001) to Bob (Extension 1002), First Phone Call

At this point, you have set up the Linux server, installed the Asterisk software, configured the network and firewalls to allow SIP and RTP communications, configured SIP extensions, and registered SIP phones to the Asterisk server. The reward for your work is to hear the first phone ring!

We will test the scenario of calling between the two extensions (Alice and Bob). So let the fun begin.

For this scenario, we'll call Bob's extension from Alice's extension:

- 1. Launch both softphones, ensure that they are both registered to the Asterisk server, and check that the status is set to Available.
- 2. On Alice's softphone (1001), enter 1002 on the keypad.
- 3. You should hear and observe Bob's phone ringing and showing the caller ID of Alice as the caller:

![](img/9f6657924397c33f088db5321b751a83_581_0.png)

- 4. Ensure you are able to speak into one of the phones and get good audio from the other phone, and vice versa.
- 5. Hang up. Then make a few test calls.

# Outside Connection—VoIP Trunking)

Outside connectivity simply means enabling the capability to communicate with devices of your private network or LAN. This capability, generally known as VoIP trunking, greatly extends the practical uses of the server, because it not only allows users to make calls to others outside of the private location, but also allows your internal users to be reachable from outside. Asterisk supports a number of technologies to interconnect to outside networks, and these fall into two main categories depending on whether the connectivity is digital or analog:

- Connectivity using a VoIP gateway If you own a PSTN line (regular telephone line provided by your local telecom provider, also known as plain telephone service, or POTS), you can connect it to your Asterisk server to make and receive calls. Calling the ATA, you will need a device to connect your PSTN line to your Asterisk system. This device is called a VoIP gateway. These devices work as a bridge between the VoIP network and the PSTN. Depending on where the voice traffic originates from, the VoIP gateway will convert the voice traffic into the the proper form for receipt by the destination network (IP or PSTN). The VoIP gateway may be a stand-alone device connected to your LAN, such as the Cisco SPA122, or a PCI card installed in your Linux server from a manufacturer such as Digium, Sangoma, AudioCodes, or Media5.

- Connectivity through an Internet telephony service provider It is still possible to connect to outside networks if you do not own a traditional PSTN line. This is achieved by interconnection to one of an increasing number of ITSPs. Asterisk supports various protocols for interconnecting with the service providers, including SIP and XMPP. ITSPs provide various services, including but not limited to inbound calling, outbound calling, or both. Your choice of ITSP will ultimately depend on the service you require, your budget, and the call quality offered by the ITSP. Most ITSPs will provide Asterisk configuration to help you get to their service as quickly as possible. In this section, we will walk through a common setup that will help you get started for SIP and XMPP technologies. The configuration may differ depending on which ITSP you use and its specific implementation.

Regardless of the method you use to achieve connectivity, Asterisk seeks these methods as channels, like the SIP channels we set up, and controls them through the dialplan.

> NOTE To connect to plain old telephones, you still need at least one service provider.
