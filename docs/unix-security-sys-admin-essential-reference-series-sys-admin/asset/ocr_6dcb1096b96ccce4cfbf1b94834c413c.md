If you are using some sort of security software, you need to add the name and IP address of this new host to those config files, as well. An example is the tcp_wrappers package that is used by the inetd program to control which hosts may connect to the system. The configuration of tcp wrappers is stored in two files, /etc/hosts.allow and /etc/hosts.deny. These files control which hosts are allowed and denied access, respectively. These actions are performed by the function addsecurity in Listing 16.1. If you are using another package, you can change this function to suit your needs.

# Adding Hosts to the news Configuration

Apart from adding the host to the sys file as described in the UUCP configuration, you also need to add the name of the new host to another file, nntp_access. This file controls which hosts may access the news spool through NNTP (Listing 16.8). This action is performed by the function addnews lan in Listing 16.1.

Next, the host is added to the basic network configuration and services. A mail is sent to root notifying it of this successful addition. If your network needs more adaptations, you can add functions to the program to perform them.

# Adding Hosts to the mail Configuration

There is no need to change the mail configuration when adding a host to the LAN. As sendmail is configured to use named, it will automatically detect when a new host is added to the configuration.

# Listing 16.8 An example nntp_access file.

```
#
# Sample NNTP access file. "read" implies "xfer".
# Note that "default" must be the first entry in the
# table. Order is important. Put the most restrictive
# entried just behind "default"
#
# by default, nothing is allowed
default        no     no
#
# hosts on the localnet can read and post
fsis.reaseau.nl  both   post   *
```