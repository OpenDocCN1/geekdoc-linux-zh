# Improving the protection of wireless networks 249

There are some legacy routers that will not allow you to disable WPS. In those cases, you have two options:

+   1. Update the router's firmware to see if the new update gives you the option to disable WPS.
2. Change your router immediately.

Now, let's look at a little-known wireless feature that may bring some vulnerabilities to your network: Universal Plug and Play (UPnP).

# ## UPnP – the problem

UPnP was also created with the idea of making life easier for users, as it enables the sharing of data between devices on a given network.

The problem is that this was created mostly for sharing data between trusted devices at a home network, therefore UPnP does not do authentication and attackers know how to exploit this.

One of the features of UPnP is port forwarding, and attackers can leverage that vulnerability to take control of computers and use them as proxies during DDoS attacks. This was the case in the famous Mirai attack in which this technique prevented security systems from identifying the command and control servers, as thousands of infected machines around the world were used as proxies between the "bot" machines and the real command and controls servers.

Other examples of malicious trojans that leverage UPnP vulnerabilities include the banking trojan Pinkslipbot, also known as QakBot or QBot. These trojans are very dangerous as they use a keylogger to capture keystrokes and send financial information and credentials to remote command and control servers.