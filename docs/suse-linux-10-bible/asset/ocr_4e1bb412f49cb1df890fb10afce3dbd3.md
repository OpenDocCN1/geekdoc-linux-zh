To set up your proxy configuration, select the Network Services icon after starting YaST, and select Proxy from the right pane. Next, enter your server addresses for your HTTP and FTP proxy services. If you need to configure a specific port number on your proxy, you can add this by appending a colon to the host name with the port number (see Figure 9-6).

![](bbox=[0.176, 0.233, 0.683, 0.537])

Figure 9-6: Configuring local proxy settings

# Using NTP Time Services

Network Time Protocol (NTP) synchronizes your machine with a centralized time server of your choosing. Time servers available on the Internet are usually a secondary source to a machine that acts as a central time server. Central (or primary) time servers are usually linked to an extremely accurate clock mechanism. To specify an NTP time source, select the Network Service icon in the left pane after starting YaST, and then select the NTP Client option from the right pane.

Selecting the NTP Client option causes you to be prompted for the host name of an NTP source (see Figure 9-7). An excellent list of NTP primary and secondary sources are available at www.eecis.udel.edu/-mills/ntp/clock2b.html. To ensure that your system automatically synchronizes itself with an NTP server, you should select the Booting option button—the default is Never, which effectively disables the NTP by your system.