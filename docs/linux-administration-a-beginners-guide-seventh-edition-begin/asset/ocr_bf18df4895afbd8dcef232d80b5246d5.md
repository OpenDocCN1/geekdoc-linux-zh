# 548 Linux Administration: A Beginner's Guide

The next configuration section describes configurations for the SIP phone(s) that will be attached to the new server:

```
[sip-phone]
type=friend
context=internal
host=dynamic
secret=your_secret>
```

The explanations for these settings are as follows:

+   [sip-phone] Section title. This is typically the label of the phone or, in telephony-speak, the extension or phone number. All lines between this section title and the next apply to this section only. With the secret, this name will be used for authentication by the SIP client and be referred to in the dialplan when incoming calls to be routed to this phone.

+   type=friend Definition of the connection type. Type friend is a combination of user and peer types, since the remote host can connect to this host and vice versa. From the viewpoint of Asterisk, a user is configured to enter the dialplan, and a peer is created for calls leaving the dialplan (via the Dial() operation).

+   context=internal The name specified here, which is arbitrary, determines where outgoing calls from the devices associated with this section will enter the dialplan.

+   host=dynamic The host option is used to define where the client exists on the network when Asterisk needs to send a call to. The default setting is host-dynamic, which is applicable if the client has a dynamic IP address. Otherwise, this option can be defined specifically by defining something like host=192.168.1.100.

+   secret=<your_secret> Sets the password. For authentication together with the name (title) of this section.

The final sample [provider] section describes connecting Asterisk server to an Internet service provider (ITSP). This connection is often referred to as SIP trunking.

The first step is to configure the SIP registration if you are interested in receiving calls from the PSTN through the ITSP. This will authenticate your Asterisk to the system and register its IP address so that the provider knows where to send calls.

Registration statements have the following format:

```
register => user[:secret[:authuser]]@host[:port]/extension
```