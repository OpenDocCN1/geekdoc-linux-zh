![](bbox=[0.2, 0.09, 0.55, 0.4])

FIGURE 16.26
Configuring your DNS servers for name server lookups.

As with the /etc/resolv.conf file, the DNS tab requires the proper DNS domain or ISP domain and name server IP addresses. It also enables the user to disable any existing DNS servers, whether local or otherwise, defined under the text file. Then, when the user is connected to the ISP, only that user's DNS server is used.

+   5. Click the Gateway tab to display the screen shown in Figure 16.27. You can edit the settings in this tab to define which gateway your machine will use for routing purposes to other networks.

Rather than attempting to define the gateway by hand or configure additional default gateways using a tool such as netcfg, you can provide kppt with either a default gateway or a static gateway going through another host.

+   6. Click the Login Script tab to display the screen shown in Figure 16.28.
+   This tab includes settings that are often the most difficult to configure properly.

If you chose to use the script-based method of connecting, you will need to properly insert the value requested by the ISP's server. These steps involve a series of Expect and Send requests. Usually an ogin: and an ord: value suffice for connecting. The former stands for login, and the latter for password. It is also wise to add a timeout variable in case your script does not work or the ISP does not recognize your input.