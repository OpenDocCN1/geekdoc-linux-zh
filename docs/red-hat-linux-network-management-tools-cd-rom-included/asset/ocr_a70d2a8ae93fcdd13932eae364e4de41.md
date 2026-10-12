This file contains agent configuration information and the default path; the filename is `/etc/snmp/conf/snmpdx.rs rc`. Because the master agent is started at system boot time, these options should be changed in the `/etc/init.d/init.snmpdx` system startup file so that they may be permanent. However, it is recommended that any changes to the startup file be tested before the startup file is executed on a system reboot.

Why change the location of the files? Well, in some sites, the standard practice is to use a special file system location that has been previously set up and is commonly available across every system on the network. Further, this area might be archived more regularly than other file systems and, as a result, be used to store all configuration files for third-party tools. For this reason, using this area can be more beneficial than using the default location. Also, if you want to test new configurations that may exist in other locations and with different filenames, these options can help as well.

The `-h` option is useful because it displays the help summary of the master agent. Running the `snmpdx` master agent command with the `-h` option will display the available command-line options and their associated arguments:

```
# /usr/lib/snmp/snmpdx -h
Usage: snmpdx [-h]
    [-H]
    [-r relay_agent_name (default relay-agent)]
    [-p port (default 161)]
    [-r resource-file (default /etc/snmp/conf/snmpdx.rsrc)]
    [-e access-control-file (default /etc/snmp/conf/snmpdx.acl)]
    [-c config-dir (default /etc/snmp/conf)]
    [-i pid-file (default /var/snmp/snmpdx.st)]
    [-o enterprise-oid-file (default /etc/snmp/conf/enterprises.oid)]
    [-y]
    [-m GROUP | SPLIT (default GROUP)]
    [-d trace-level (range 0..4, default 0)]
```

The master agent provides the capability for messages to be displayed by using the `-d` option. This option can be very useful when debugging agent configurations or operational problems. Four debugging levels are supported that range from 0 (no debugging) to 4 (full debugging). The fourth level of debugging includes agent configuration information, decoding of each SNMP message PDU,