# 7.5  Lab – configuring your Windows PC to use DNS

Now we’ll do the basic DNS configuration for a PC on a typical small site connected to the Internet that relies on the DNS servers operated by the site’s ISP and has no internal DNS servers.
The only settings you *must* enter are one DNS server address and the hostname; if you don’t enter at least one server address your PC won’t use DNS. (Windows automatically fills in the hostname. See Module 8.14 for more detail. It is Windows that insists you enter a name here; DNS doesn’t care.)

Enter the IP number of the DNS server(s): Control Panel > Network > Protocols > TCP/IP > DNS > DNS Service Search Order > Add ... (Figure 7.5).

![](bbox=[0.15, 0.27, 0.92, 0.55])

You can enter up to three servers. As with Linux, servers closer to the top of the list are used first; the **Up** and **Down** buttons let you change the order of the servers, so you can set your own preference for the order in which the servers are used. Modified settings take effect as soon as you press **OK** or **Apply**; you don’t have to reboot. (**Apply** is the same as **OK** but it doesn’t close the window. **Apply** is useful when you are experimenting with the settings: if you leave the Network window and come back to it, it will be open at the appropriate place.)
As usual you can verify the changes using *ipconfig/all* (Figure 7.6) or *wnipcfg* (Figure 7.7).

![](bbox=[0.15, 0.71, 0.92, 0.95])