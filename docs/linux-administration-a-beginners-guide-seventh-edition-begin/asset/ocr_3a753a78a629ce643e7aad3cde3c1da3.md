# CHAPTER 21 Voice over Internet Protocol (VoIP)

TIP At this stage, we recommend that you disable SELinux on Fedora/RHEL/CentOS server before continuing to the next steps. You can use the setenforce command to temporarily do this:

```
# setenforce 0
```

# Configuring the PBX

Now that you have a fully installed Asterisk server and verified that it is running, you will proceed to configure your first PBX. There are a number of technologies supported by Asterisk to configure the local extensions and the connection to the outside world, such as SIP, XMPP, IAX2, and so on.
For the scope of the chapter, we will focus on SIP connectivity. Configuring SIP phone to work with Asterisk is not complex. However, because there are so many options in both Asterisk and the configuration of the particular telephone set or softphone, which can get confusing. What we are going to do, is give you the VoIP phone selected for the exercises (and equipped with enough background knowledge to configure most SIP phones available today). We are not claiming that this is the best way, or only way, but we hope it will form a foundation from which to take a basic configuration and tweak until you get the solution you need.

> NOTE We did not use GUI implementation in this chapter because we want to expose you to the nuts and bolts of the Asterisk project. You may decide to pick any GUI of your choice afterwards. However, in production environments, using a GUI is discouraged on Asterisk servers because it is a waste of resources and can hammer performance of your VoIP platform.

We'll build up a PBX by a very simple configuration consisting of only two SIP phones and a connection to the PSTN to make calls to mobile phones and landlines, as shown in Figure 21-3. This configuration may not be capable of all that yet, but it is a good foundation to start with and serve as a reasonable demonstration of how incoming and outgoing calls are routed through the dialplan.
The configuration in Figure 21-3 consists of

+   - One Asterisk server
- Two SIP extensions: Alice, at extension 1001, and Bob, at extension 1002
- One outside connection using Google Voice Service
- One local phone number from the ITSP to receive calls from the PSTN (for example, with caller ID 1-408-555-1212)