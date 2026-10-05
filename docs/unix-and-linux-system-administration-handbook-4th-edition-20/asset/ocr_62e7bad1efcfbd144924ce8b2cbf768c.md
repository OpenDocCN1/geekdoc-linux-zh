# 17.3 DNS FOR THE IMPatient

Before we start with the details of DNS, let's take a brief detour to address everyone’s most frequently asked questions:

+   - How do I add a machine to a network that's using a name server?
- How do I configure that new machine as a client of DNS?

What follows is a cookbook-style recipe that does not define or explain any terminology and probably does not fit exactly with your local policies and procedures. Use it with caution and refer to RFC1912, Common DNS Operational and Configuration Errors.

# Adding a new machine to DNS

If your network is set up to the Dynamic Host Configuration Protocol (DHCP) you may not need to perform any manual configuration for DNS. When a new computer is connected, the DHCP server informs it of the DNS servers it should use for queries. Hostname-to-IP address mappings for the outside world were most likely set up when the DHCP server was configured and automatically entered through DNS dynamic update.

For networks that do not use DHCP, the following recipe shows how to update the DNS configuration by copying and modifying the records for a similar computer.

**Step 1**: Choose an unused hostname and IP address for the new machine in conjunction with local syncdams or your upstream ISP.

**Step 2**: Identify a similar machine on the same subnet. You’ll use that machine’s records as a master for the new ones. In this example, we use a machine called template.example.com on the subnet 208.77.188/24 as the master.

**Step 3**: Log in to the master server machine. If you don’t know which machine is the master server, you probably should not be messing with it, but you can use the **dig** ( SOA domainname) to identify it. You can also use **drill** if dig is not installed.

**Step 4a**, for sites binding BIND servers:

+   - Find the master server configuration file, usually /etc/named.conf.
- Within the **options** statement in **named.conf**, find the **directory** line that tells you zone data files are kept at your site (see page 603). The zone files contain the actual host and IP address data.

+   - From the **zone** statements, the filenames for the forward zone file and reverse zone file appropriate for your new IP address (page 612).
- Verify from the **zone** statements that this server is fact the master server (type **master**, not **slave** or some value) for the Domain. If it’s not, you’re on the wrong server! The forward zone statement in **/etc/named.conf** should look something like this: