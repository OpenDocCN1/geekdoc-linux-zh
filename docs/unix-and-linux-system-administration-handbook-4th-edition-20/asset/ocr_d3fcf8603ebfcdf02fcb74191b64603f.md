# Table 12.2 Independent keywords for the JumpStart syscidcfg file

| Keyword | What it specifies |
|---|---|
| keyboard | Keyboard layout and language |
| name_service | Service configuration for NIS, DNS, or LDAP |
| network_interface | Connection details: hostname, IP address, etc. |
| nfs4_domain | Domain to use for NFS version 4 |
| root_password | Encrypted root password |
| security_policy | Kerberos network authentication |
| service_profile | Available network services |
| system_locale | System language |
| terminal | Terminal type |
| timeserver | Network date and time server |
| timezone | System time zone |

```
keyboard=US-English
system_locale=en_US
timezone=US/Mountain
terminal=sun-cmd
timeserver=time.nist.gov
name_service=DNS [domain=solaris.booklar.atrust.com]
name_server=192.168.2.10
search=atrust.com,booklar.atrust.com]
nfs4_domain=dynamic
root_password=m4QPFOWNY
network_interface=e1000g0 [hostname=sake
default_route=192.168.10.254
ip_address=192.168.10.155
netmask=255.255.255.0]
```

If you're distributing the syscidcfg file to many clients, the IP address of your course need to differ between systems. You can leave out the network interface details to force them to be configured the first time the system boots. Or, to obtain a network address from DHCP rather than assigning statically, use the line
network_interface=e1000g0 (dhcp)

After you've set up the rules file, the syscidcfg file, and copy them all to the /jumpstart/config directory and run Sun check, which validates the configuration. The check script should be run from the config directory, and is mandatory; check a rules file that certifies JumpStart the files are syntactically acceptable. Do not skip this step or JumpStart will not work.

```
solaris $ sudo cp /jumpstart/s10parc/Solaris_10/Misc/jumpstart_sample/
/jumpstart/config
solaris $ sudo ./check
Validating rules...
Validating profile_A...
The custom JumpStart configuration is ok.
```