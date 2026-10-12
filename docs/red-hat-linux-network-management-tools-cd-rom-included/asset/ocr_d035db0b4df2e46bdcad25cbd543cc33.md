automatically limit certain system processes so that the system doesn't become overloaded.

# Listing 7.4 Sample agent configuration

```
#
# Sample Configuration
# Monitor these processes..
#

proc_mountd
proc_nfsd
proc_lpsched
#
# Monitor load average above 2.0..
#
load 2
#
# Make sure we have a least 50 MB in root
# and 100 MB in /usr
#
disk /      50000
disk /usr    100000
#
# Execute the following programs to obtain
# output via the UCD mib...
#
exec .1.3.6.1.4.1.2021.255.1 top /usr/bin/top
exec .1.3.6.1.4.1.2021.255.2 ps /bin/ps -e
pass .1.3.6.1.4.1.2021.255.3 /usr/local/perl /etc/snmp/message.pl
```

# Command-line Options

The agent provides a number of command-line options, as listed in Table 7.4. Because the agent in most instances will be started automatically when the system boots, some of these options should be changed in the start up file if they are to become permanent. However, some of the options only make sense when used on the command line.

By default, when snmpd is started, it uses well-known SNMP port 161. This must be changed if other agents are running on the same system or if you are using a master agent. The -p option has been provided for this purpose. The snmpd command will use this option, followed by the port number, to listen for incoming SNMP requests.

Several options can be used to assist in any debugging efforts that must be done with the agent. The -a option displays the IP