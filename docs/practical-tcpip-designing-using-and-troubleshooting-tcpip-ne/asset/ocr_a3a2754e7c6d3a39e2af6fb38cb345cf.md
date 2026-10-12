# ## 14.10 URLs, machine names, and the DNS

In Module 14.1 we said that a URL (Uniform Resource Locator) consists of four parts:

*protocol-scheme:// host-address [:port] pagename*

and we'll look at some of these in a little more detail here.

# ### Protocol scheme

This is **HTTP** for normal Web transfers, and **HTTPS** for secure Web transfers (Module 14.18). This field is not case-sensitive.

# ### Host address component of a URL

This is the address of an individual machine – either its IP number or its name. As usual, if you specify a name, the client uses the DNS to convert the name to an IP number, and your Web client will then use the IP number to connect to the server. Of course, if the name isn't in the DNS you will get an error.

In Module 11.3 we saw that the DNS can contain multiple MX records, to support multiple e-mail servers. The DNS also allows a machine or hostname to have several different IP address entries ("A" records) meaning that several different machines share this name. You can see that **www.ibm.com** has four different addresses, and presumably, four different servers:

```
```
alice# host www.ibm.com
www.ibm.com    A    129.42.17.99
www.ibm.com    A    129.42.18.99
www.ibm.com    A    129.42.19.99
www.ibm.com    A    129.42.16.99
```
```

Just as with e-mail, this gives us a form of load balancing. Instead of returning the entries in the same order every time, the DNS server round-robins them in successive DNS responses, so that each entry gets an equal number of turns at being top in the list:

```
```
alice# host www.ibm.com
www.ibm.com    A    129.42.19.99
www.ibm.com    A    129.42.16.99
www.ibm.com    A    129.42.17.99
www.ibm.com    A    129.42.18.99
alce# host www.ibm.com
www.ibm.com    A    129.42.16.99
www.ibm.com    A    129.42.17.99
www.ibm.com    A    129.42.18.99
www.ibm.com    A    129.42.19.99
```
```

Because each successive Web connection will go to a different server, the load is shared more or less equally across the four servers. However, unlike with MX records, if the first host that's tried isn't available, you got an error: successive hosts are not tried.