# ## Chapter 8

# # DNS Service

# ### Configuring a DNS Client (Resolver)

Typically, the Red Hat installation program asks you about your DNS server and automatically configures the necessary resolver configuration file. However, often it is necessary to change the resolver configuration to reflect any changes to the DNS server you use. For example, if you configure your resolver during Red Hat installation and later change ISPs, you must manually reconfigure it. Here is how.

If you plan to use your ISP’s DNS server to resolve names and IP addresses, ask your ISP for the hostname and the IP address of its DNS servers. After you have the required information, you can configure the resolver as follows:

+   1.  First, modify the resolver configuration file called /etc/resolv.conf. Listing 8-1 shows a typical /etc/resolv.conf file for a domain called nitec.com.

# **Listing 8-1**  _The resolver configuration file /etc/resolv.conf_

```
# Default Domain
domain nitec.com

# Default search list
search nitec.com
```