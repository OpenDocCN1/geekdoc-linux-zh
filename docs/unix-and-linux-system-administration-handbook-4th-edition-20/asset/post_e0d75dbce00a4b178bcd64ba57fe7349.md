
# Network installations with JumpStart

The syntax of the rules file is simple but powerful. Systems can be identified by network, hostname, model, domain name, or by many other attributes. The following rules file specifies one profile for systems on the 192.168.10.0 network and another profile for SPARC systems that have 2–4 GiB of memory:

```
network 192.168.10.0 - profile_a -
arch sparc && memory size 2048-4096 begin profile end
```

In the network example, there are no custom scripts, and the installation profile called profile_a is used. The other example scripts call begin and a profile named profile_b.

Profile files are also simple. Keywords (of which there are many) specify files and installation types. A sample profile might look something like this:

```
install_type initial_install
system_type standalone
partitioning default
filesys any 512 swap
cluster SUNWPCall # Specify size /swap
```

An initial_install starts with a clean slate, as opposed to performing an upgrade. This profile uses a disk partitioning scheme. The cluster SUNWPCall line identifies an “installation group” of packages to install—in this case, all available Solaris packages.

The sysidcfg file, which preconfigures other aspects of the installation, consists of lines of the form

```
keyword=value
```

Keywords are insensitive and, except for the network_interface keyword, can only be used once. If a keyword appears more than once, only the first instance takes effect.

Some keywords depend on others and are enclosed in curly braces. These dependent keywords cannot be used unless the corresponding parent (independent) keyword has been specified. Table 12.2 on the next page lists the independent keywords.

As an alternative to sysidcfg, a limited set of preconfiguration options can also be specified through DHCP or a network service such as DNS. However, we recommend the use of sysidcfg because of the limited number of options available through the alternative pathways.

The following sysidcfg example configures a system called that has one network interface.

- + 1. Google “Custom JumpStart and Advanced Installations” to access Sun’s guide, which contains full details on the rules and profiles files.

## Table 12.2 Independent keywords for the JumpStart syscidcfg file

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

After you've set up the rules file, the sysidcfg file, and copy them all to the /jumpstart/config directory and run Sun check, which validates the configuration. The check script should be run from the config directory, and is mandatory; check a rules file that certifies JumpStart the files are syntactically acceptable. Do not skip.

```
solaris $ cp /jumpstart/config/* /jumpstart/config/
solaris $ check
rules file is syntactically acceptable
```

## Network installations with the Automated Installer

At the end of the process, your /jumpstart/config should look something like this:

```
solaris $ ls -l
```

AI simplifies the process by automating the configuration. In this case, we use `addadm` to create a new service.
