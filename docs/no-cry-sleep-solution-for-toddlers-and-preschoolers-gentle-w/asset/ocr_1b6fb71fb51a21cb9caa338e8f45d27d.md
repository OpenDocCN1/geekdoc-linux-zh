# lpd.conf

The general configuration for LPRng, including the lpd print server, is handled in the /etc/lpd.conf file. Here you can specify features that apply to all printers and print management. You should think of these more as default features, as any of them can be overridden in a printer’s printcap entry. The lpd.conf file installed with LPRng contains an extensive list of configuration parameters. They are all commented out, prefixed with # signs. Each parameter is preceded by a comment describing the parameter. The entry itself lists the default value given by the parameters, preceding the entry with the term default. The entry for the connect_timeout parameter is shown here:

```
# Purpose: connection timeout for remote printers
# default connect_timeout=10 (INTEGER)
```

To create your own timeout entry, it is best to add your own entry below, as shown here. Notice that the preceding # and the term default are missing from the new entry. The connection timeout for remote printers is now set at 20. This can be overridden by a printer’s printcap file entry.

```
# Purpose: connection timeout for remote printers
# default connect_timeout=10 (INTEGER)
connect_timeout=20
```

Parameters can also be flags that you can turn on or off. An off flag is noted with an attached @ sign. In the following example, the allow_user_logging parameter is a flag that allows users to request login information. By default, it is turned off. The following example turns it on:

```
# Purpose: allow users to request logging info using lpr -mhost&port
# default allow_user_logging@ (FLAG off)
allow_user_logging
```

# LPRng Access Controls: lpd.perms

LPRng provides access control rules for controlling how remote users access your print server, and thereby the printers it controls. These rules are placed in the /etc/lpd.perms file and can be used to refuse print services to specific hosts or users. Such rules consist of an action and a set of keys. The keys specify criteria to be met, and if they met, their associated action is taken. In each rule, you have one action and one or more keys. If there are several keys, all their criteria must be met for the action to take place. An example of a key would be to specify the IP address of a host. In addition, you have to specify the kind of service that is being requested, such as a printing or connection request. The action is usually either ACCEPT or REJECT. Keys operate as flags or variables. To specify a host, you assign the address to the HOST key, using an assignment operator. For a user, you use USER, and for IP addresses, IPIP. The kind of service is specified by the SERVICE key. For a printing request, the value you assign is the lpd code P. The following example specifies a host as the key and will REJECT any request from that address:

```
REJECT SERVICE=P HOST=192.168.0.57
```