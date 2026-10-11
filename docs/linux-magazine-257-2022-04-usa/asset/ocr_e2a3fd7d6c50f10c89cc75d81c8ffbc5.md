![](bbox=[0.09, 0.1, 0.92, 0.35])

Open the link to your Checkmk site in your browser. You can open the link shown on your terminal. Log in with ckadmin and the password you copied from the terminal. You will see an empty dashboard. Go to User in the sidebar on the left and, under Profile, click on *Change password* to change your password (recommended).

After that you can start adding hosts to your monitoring (Figure 4). In my case, I will add my router. Go to *Setup | Hosts* and click on *Add host*.

In my example, I only have to add the hostname *tplinkmodem.net*, because TP-Link set up the DNS for their devices and, thus, Checkmk can resolve the IP address for your hostname automatically. I recommend using this option, if available. If that is not the case, you will also need to add your device’s IP address by activating the checkbox next to *IPv4 address* and entering the IP address.

For my router, I want to work with SNMP, but by default, Checkmk as- sumes that you use the Checkmk agents to monitor systems. The Checkmk agents are great for monitoring servers, but on most network devices, you can- not install additional software. Thus, go to *Monitoring agents*, check the box *Checkmk agent/API integrations*, and choose *no agent*.

Next, check the box labeled SNMP (Figure 5). Choose your SNMP version—*SNMP v2 or v3* works in most cases. Because I did not change the SNMP community, I can leave the SNMP credentials box unchecked—by default, Checkmk assumes that the password is *public*. If that is not the case, you have to set the community string under *SNMP credentials*. Leave the other items unchanged.

Next, click on *Save & go to service con- figuration*. Checkmk will now automati- cally discover any relevant monitoring services on that host, and you should then see a list of *Undecided services*. Click on *Fix all* to monitor all of these relevant services (Figure 6). That will add all of the detected services to the monitoring and will also remove

![](bbox=[0.09, 0.65, 0.92, 0.93])