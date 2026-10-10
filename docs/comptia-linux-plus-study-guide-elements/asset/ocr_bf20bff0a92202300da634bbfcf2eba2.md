# Configuring Basic Printing

![](bbox=[0.15, 0.12, 0.3, 0.25])

If you’re configuring a workstation with a local printer that you don’t want to share or if you want to configure a workstation to use printers shared via LPD or some other non-IPP printing protocol, you shouldn’t need to adjust /etc/cups/cupsd.conf. If you want to access remote IPP printers, however, you should at least activate browsing by setting the directive Browsing On, as described shortly. You shouldn’t have to modify your location definitions unless you want to share your local printers.

The /printers location, shown here, controls access to the printers themselves. Features of this example include the following:

**Directive order** The `Order` `Deny,Allow` line tells CUPS in which order it should apply allow and deny directives—in this case, allow directives to modify deny directives.

**Default policy** The `Deny` from `All` line tells the system to refuse all connections except those that are explicitly permitted.

**Browsing control lines** The `BrowsesAllow` lines tell CUPS from which other systems it should accept browsing requests. In this case, it accepts connections from itself (127.0.0.1), from systems on the 192.168.1.0/24 network, and from systems connected to local subnets (@LOCAL).

**Access control lines** The `Allow` lines give the specified systems nonbrowse access to printers—that is, those systems can print to local printers. In most cases, the `Allow` lines will be the same as the `BrowsesAllow` lines.

You can also create a definition that uses `Allow` from `All` and then creates `BrowseDeny` and `Deny` lines to limit access. As a general rule, *though*, the approach shown in the preceding example is safer. Locations other than the /printers location can also be important. For instance, there’s a root ( /) location that specifies default access permissions to all other locations and an /admin location that controls access to CUPS administrative functions.

Before the location definitions in cupsd.conf are a few parameters that enable or disable browsing and other network operations. You should look for the following options specifically:

**Enabling browsing** The `Browsing` directive accepts `On` and `Off` values. The CUPS default is to enable browsing (Browsing On), but some Linux distributions disable it by default.

**Browsing access control** The `BrowseAddress` directive specifies the broadcast address to which browsing information should be sent. For instance, to broadcast data on your printers to the 192.168.1.0/24 subnet, you’d specify `BrowseAddress` 192.168.1.255.

Once you’ve configured a CUPS server to give other systems access to its printers via appropriate location directions, and once you’ve configured the client systems to use browsing via `Browsing` `On`, all the systems on the network should autodetect all the printers on the network. There’s no need to configure the printer on any computer except the one to which it’s directly connected. All printer characteristics, including their network locations and PPD files, are propagated automatically by CUPS. This feature is most important in configuring large networks with many printers or networks on which printers are frequently added and deleted.