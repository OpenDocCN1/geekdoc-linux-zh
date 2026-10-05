(close the window or type exit at the command line) and fire up your browser (which we assume is Netscape. Enter that address into the Location field and press Enter. You will be prompted to log into Webmin.)

It is important to note that the user name and password you use to log into Webmin will determine the level of access you are granted. Webmin honors Linux privileges, so log as the root user. You should find yourself at the screen shown in Figure 10.3.

![](bbox=[0.292, 0.226, 0.873, 0.506])

The very first task to perform is to verify that you have Webmin secured from the world. Upon initial installation, it should be configured to accept connections only from the loopback interface, meaning that you can connect to it from your local machine (localhost) on IP address 127.0.0.1. You want to ensure that this is the case. If you were to log into Webmin from another machine on an unencrypted connection, the user name and password would travel the network in plain text, so that anyone with a packet sniffer would be able to configure your system for you very quickly. That would be a bad thing.

To verify that Webmin is listening on the loopback interface only, click the Webmin Configuration link, and then click Ports and Addresses. If the resulting display resembles Figure 10.4, you are ready to go. If it doesn't, make it do so, and then click Save.