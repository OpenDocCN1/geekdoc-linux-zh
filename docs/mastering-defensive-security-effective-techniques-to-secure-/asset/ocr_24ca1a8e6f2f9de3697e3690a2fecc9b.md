Additionally, researchers also found some correlation between the MAC address and/or the serial number of the router, enabling an attacker to calculate the PIN based on those values.

![](bbox=[0.237, 0.175, 0.762, 0.003781])

Figure 8.9 – WPS data pasted on the back of the router

As seen in the preceding figure, those values can be located on a sticker on the back of the router, but an attacker can remotely gather them by leveraging the vulnerabilities of the probe request packets, which are unencrypted and broadcasted by the router, meaning anyone can receive and read them, and they may contain the MAC address as well as the serial number. If you want know more about probe request vulnerabilities, see Chapter 5, Cybersecurity Technologies and Tools, under the Advanced wireless tools for cybersecurity section.

# WPS – the solution

You may be surprised to know that WPS is enabled by default on most routers, so you may even have this vulnerability at home knowing it.

So, the best recommendation here is to completely disable WPS from your router (step-by-step instructions will be provided in the User's safety guide for wireless networks section).

If some reason you need to have WPS enabled, leave the PCB enabled and make sure you disable the PIN option (as it is more vulnerable).

Also make sure that you update your router's firmware to ensure that your router contains the latest WPS fixes and security updates.