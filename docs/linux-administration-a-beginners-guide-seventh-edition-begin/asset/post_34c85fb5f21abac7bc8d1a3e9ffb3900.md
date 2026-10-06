
# Linux Administration: A Beginner's Guide

| Path | Summary | Description |
| --- | --- | --- |
| /etc/asterisk/ | Configuration files | Contains dozens of configuration files used to describe the functionalities of the Asterisk system and to run it. The configuration files include **extensions.conf**, **sip.conf**, and **modules.conf**, which will explore more in the next section. |
| /usr/lib64/asterisk/modules/ | Component module libraries | Contains all of the modules loadable in the Asterisk system, as the various applications, codecs, formats, and channels. |
| /usr/sbin | Binary files | Contains the executable binary files to launch the Asterisk system. |
| /var/log/asterisk | Asterisk log files | Contains the Asterisk messages, errors, and CDR information. You can control the type of information logged to the various log files and the verbosity and detail level using the **logger.conf** configuration file. |

**Table 21-5** Asterisk File Structure

In general, most configuration files include a [general] section that contains the options that will apply to all other sections in the configuration file unless they are overridden specifically. The definitions for the SIP peers and users are also included in the **sip.conf** file.

All section names are encased in square brackets, including device names. Anything that follows a section name (or device definition, which for our purposes is essentially the same thing) is applied to that section.

# CHAPTER 21 Voice over Internet Protocol (VoIP)

The following is a simplified example of the sip.conf file necessary for a basic configuration. We will start with a description of the [general] section and then follow with configurations for the SIP phones (Local Extensions) and connection to the SIP provider.

```
[general]
disallow=all
allow=ulaw
allow=alaw
allow=gsm
qualify=yes
caninvite=no
```

The explanations for these settings are as follows:

- * **disallow=all**: Disables the use of all codecs. Before specific codecs are enabled in order of preference.

- * **allow=ulaw**: Enables a codec based on the μ-law algorithm that is used primarily in North America and Japan. The μ-law algorithm is a 64-Kbps pulse-code modulation (PCM) codec and a variant of the ITU-T G.711 standard. It imposes a minimal load on the CPU.

- * **allow=alaw**: Enables a codec based on the A-law algorithm that is used in Europe and the rest of the world. Requires even less CPU processing power than μ-law. In the United States, it is used by convention for international connections if at least one party uses it. Another ITU-T G.711 variant.

- * **allow=gsm**: Enables the GSM 06.10 codec, which is the preferred codec for Asterisk. It operates at 13 Kbps, employs lossy compression, and has no licensing requirements, and offers excellent CPU-related performance.

- * **qualify=yes**: When enabled, SIP NOTIFY messages will periodically be sent to the remote peer to determine both its availability and the latency of its replies.

- * **caninvite=no**: Prevents the two endpoints from connecting to each other directly, which is normal behavior when SIP. This forces Asterisk to remain in the transmission path, which is necessary to detect DTMF signals. Some SIP providers require this setting for various reasons such as billing, call control, recording, and so on.

# 548 Linux Administration: A Beginner's Guide

The next configuration section describes configurations for the SIP phone(s) that will be attached to the new server:

```
[sip-phone]
type=friend
context=internal
host=dynamic
secret=your_secret
```

The explanations for these settings are as follows:

- [sip-phone] Section title. This is typically the label of the phone or, in telephony-speak, the extension or phone number. All lines between this section title and the next apply to this section only. With the secret, this name will be used for authentication by the SIP client and be referred to in the dialplan when incoming calls to be routed to this phone.

- type=friend Definition of the connection type. Type friend is a combination of user and peer types, since the remote host can connect to this host and vice versa. From the viewpoint of Asterisk, a user is configured to enter the dialplan, and a peer is created for calls leaving the dialplan (via the Dial() operation).

- context=internal The name specified here, which is arbitrary, determines where outgoing calls from the devices associated with this section will enter the dialplan.

- host=dynamic The host option is used to define where the client exists on the network when Asterisk needs to send a call to. The default setting is host-dynamic, which is applicable if the client has a dynamic IP address. Otherwise, this option can be defined specifically by defining something like host=192.168.1.100.

- secret=<your_secret> Sets the password. For authentication together with the name (title) of this section.

The final sample [provider] section describes connecting Asterisk server to an Internet service provider (ITSP). This connection is often referred to as SIP trunking.

The first step is to configure the SIP registration if you are interested in receiving calls from the PSTN through the ITSP. This will authenticate your Asterisk to the system and register its IP address so that the provider knows where to send calls.

Registration statements have the following format:

```
register => user[:secret[:auth]]
```

# 21 Voice over Internet Protocol (VoIP) 549

The following is a simplified example of the sip.conf file necessary for a basic configuration. We will start with a description of the [general] section and then follow with configurations for the SIP phones (Local Extensions) and connection to the SIP provider.

```
[general]
disallow=all
allow=ulaw
allow=alaw
allow=gsm
qualify=yes
caninvite=no
```

The explanations for these settings are as follows:

- * **disallow=all**: Disables the use of all codecs. Before specific codecs are enabled in order of preference.

- * **allow=ulaw**: Enables a codec based on the μ-law algorithm that is used primarily in North America and Japan. The μ-law algorithm is a 64-Kbps pulse-code modulation (PCM) codec and a variant of the ITU-T G.711 standard. It imposes a minimal load on the CPU.

- * **allow=alaw**: Enables a codec based on the A-law algorithm that is used in Europe and the rest of the world. Requires even less CPU processing power than μ-law. In the United States, it is used by convention for international connections if at least one party uses it. Another ITU-T G.711 variant.

- * **allow=gsm**: Enables the GSM 06.10 codec, which is the preferred codec for Asterisk. It operates at 13 Kbps, employs lossy compression, and has no licensing requirements, and offers excellent CPU-related performance.

- * **qualify=yes**: When enabled, SIP NOTIFY messages will periodically be sent to the remote peer to determine both its availability and the latency of its replies.

- * **caninvite=no**: Prevents the two endpoints from connecting to each other directly, which is normal behavior when SIP. This forces Asterisk to remain in the transmission path, which is necessary to detect DTMF signals. Some SIP providers require this setting for various reasons such as billing, call control, recording, and so on.

The next configuration section describes configurations for the SIP phone(s) that will be attached to the new server:

```
[sip-phone]
type=friend
context=internal
host=dynamic
secret=your_secret
```

The explanations for these settings are as follows:

- [sip-phone] Section title. This is typically the label of the phone or, in telephony-speak, the extension or phone number. All lines between this section title and the next apply to this section only. With the secret, this name will be used for authentication by the SIP client and be referred to in the dialplan when incoming calls to be routed to this phone.

- type=friend Definition of the connection type. Type friend is a combination of user and peer types, since the remote host can connect to this host and vice versa. From the viewpoint of Asterisk, a user is configured to enter the dialplan, and a peer is created for calls leaving the dialplan (via the Dial() operation).

- context=internal The name specified here, which is arbitrary, determines where outgoing calls from the devices associated with this section will enter the dialplan.

- host=dynamic The host option is used to define where the client exists on the network when Asterisk needs to send a call to. The default setting is host-dynamic, which is applicable if the client has a dynamic IP address. Otherwise, this option can be defined specifically by defining something like host=192.168.1.100.

- secret=<your_secret> Sets the password. For authentication together with the name (title) of this section.

The final sample [provider] section describes connecting Asterisk server to an Internet service provider (ITSP). This connection is often referred to as SIP trunking.

The first step is to configure the SIP registration if you are interested in receiving calls from the PSTN through the ITSP. This will authenticate your Asterisk to the system and register its IP address so that the provider knows where to send calls.

Registration statements have the following format:

```
register => user[:secret[:auth]]
```
