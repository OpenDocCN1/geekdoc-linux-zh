# Automating Ignite-UX installations

For PA-RISC systems, edit the file /etc/opt/ignite/inst_boottab. Lines in this file are of the form:

```
IP_address:MAC_address:datetime_last_used [:reserve]
```

The IP_address field assigns an IP address for the new client to use while installing services. The optional MAC_address field identifies a specific machine; if you leave it out, any client can use this IP address (but note the interaction with the reserve keyword). The third field is used and maintained by Ignite-UX; leave it blank when adding entries.

If the keyword reserve is present in the last column, the IP address is reserved for the use of the client whose MAC address appears in field two. If reserve is not specified, field two shows the last MAC address that was used by IP address.

The /etc/boottab and /etc/dhcptab files, used to boot Itanium systems, have a very different format. The files are well commented and littered literally with examples, which we will not repeat here. (Note that a single daemon, bootpd, serves both BOOTP and DHCP requests on HP UX systems). DHCP is the boot method for Itanium systems as it can provide anonymous clients. See comments in /etc/boottab and /etc/dhcpv6 for full details.

Once you've configured Ignite-UX server as discussed above, clients can boot over the network. On the client side, interrupt the boot process, enter the EFI Boot Manager, and add a network device. The client will request an IP address, and the Ignite-UX server will respond and begin the installation.

This method works best for systems that share a subnet with the Ignite-UX server. For configurations in which the client is not on the server's subnet, HP lists a number of options in the Ignite-UX Administration Guide.

# Automating Ignite-UX installations

Ignite-UX network boot configuration is a prerequisite for automated installation, but configuring Ignite-UX without specifying automatic boot details results in an interactive installation. Ignite-UX can also

+   - Use the saved configuration from a previous installation to automate future installations.

+   - Rely on configuration files that can be set up per client, per release, or at the whim of the administrator.

+   - Specify default values for some configuration options, such as DNS servers, and leave others to be selected during interactive installation.

The automated installation files are located in /opt/ignite/data, and several examples and sample configurations are included in the Ignite-UX installation package. The release and example subdirectories are a good place to get started.