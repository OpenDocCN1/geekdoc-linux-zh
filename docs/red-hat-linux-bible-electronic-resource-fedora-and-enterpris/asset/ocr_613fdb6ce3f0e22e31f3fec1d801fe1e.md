+   * Creating DNS Configuration files (`named.conf` and `/var/names/*`)
+   * Starting the `named` daemon
+   * Monitoring `named` activities

In the example configuration, you set up a primary master DNS server and a slave DNS server. The primary holds the authoritative records for the domain. The secondary is there to share requests for information about the domain, particularly in case the primary goes down.

# ## Identifying your DNS servers

If you didn't have your DNS servers set up at the time that you purchased your domain name with a registration authority, you might have just "parked" the domain name there until you configured your DNS servers. Whenever you're ready to set up your DNS servers, return to that registration authority and provide the following information about your DNS servers:

+   * DNS server IP addresses (the static IP addresses of your DNS servers, probably primary and slave)
+   * DNS server host names (often `ns1.yourdomain.com`, where you replace `yourdomain.com` with your domain name for the primary; the slave host name is `ns2.yourdomain.com`)

You should register both the primary and slave DNS servers. After you update this record, that information typically takes a day or two to propagate throughout the Internet. Once your DNS servers are registered, you also need to tell the registration authority to use those DNS servers as the authority for addresses in your domain. The registration authority probably offers an online form you can fill out to identify your DNS servers.

# ## Creating DNS configuration files (`named.conf` and `/var/names/*`)

In configuring a DNS server, you're actually creating definitions that apply to a particular *zone* in the public DNS tree, as well as several local zones that apply to your computer and local network. To create a useful DNS server for your example small-office environment, you have the following zones:

+   * **Public DNS server zone**—The DNS server is authoritative for the domain that you're serving. This zone serves the names and IP addresses for your public servers. In the example `named.conf` file shown in the next section, you need to replace the name `yourdomain.com` with the domain that you're creating. These records become accessible to everyone on the Internet.
+   
+   * **Private DNS server zone**—So each computer on the private network doesn't need to know the IP addresses for other computers on your private network, a zone is added in the example `named.conf` file to let the DNS server resolve these addresses. The names and IP addresses (which are private) are available only to computers on your LAN.