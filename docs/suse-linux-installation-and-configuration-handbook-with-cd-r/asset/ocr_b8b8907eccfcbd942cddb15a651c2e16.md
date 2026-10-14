12. Press Continue to save and apply your changes.

13. An /etc/sendmail.cf file will be created for you. Start sendmail by typing the following:

```
#/sbin/init.d/sendmail start
```

sendmail now should be all configured and running. You must attempt to manually configure sendmail to feel the amount of pain that using YaST avoided! Just use any mail program and have it use your machine as the mail server.

# Expert Mode for Configuring sendmail

So, you tried the presets, but you now want more. This is where the expert mode comes in handy. You will be asked to enter the parameters that will be used to configure sendmail for you. To use the expert mode, follow these steps:

+   1. Log in as root.
+   2. Run YaST.
+   3. Navigate to System administration, Network configuration, Configure sendmail and press Enter.
+   4. The sendmail configuration module pops up (refer to Figure 20.1).
+   5. Highlight the expert mode and press Enter.
+   6. The sendmail Expert Mask appears (see Figure 20.2).

FIGURE 20.2
Expert mode for configuring sendmail with YaST

![](bbox=[0.33, 0.7, 0.88, 0.9])

7. The first field is the Domain names for local delivery. sendmail needs to know which email is to be sent locally, and therefore should be stored locally. Enter a list of all the domains that are considered local. This usually is localhost and your hostname.

8. The next field is the Host for all outward Email. If you are on a slow connection, you can have your outgoing emails delivered to another email server that handles sending them for you. This could be your ISP's mail server. Just enter the address of that server here. You should define the protocol to be used, as well. For example, if your ISP's mail server is SMTP and is called mail.isp.com, the entry would be smtp:mail.isp.com.