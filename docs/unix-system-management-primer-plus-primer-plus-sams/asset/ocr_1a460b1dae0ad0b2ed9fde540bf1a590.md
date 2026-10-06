In Listing 3.1, machines on network 1.2.3.0/24 are desktop workstations, machines on net-work 1.2.4.0/24 are compute servers, and everything else is loaded using the generic config-ration class. Every rule runs the set_root_pw script after installation, which lets the administrator set the root password manually.

# Jumpstart Installs Get Even Easier

All Sun servers now come preconfigured to boot from the network using Jumpstart. This prefigu-ration means that if you already have a rule set representing a Netra t105 with 1GB of RAM and one 18GB hard drive, you could order 10 Netras, connect them to the network, plug them all in, and Jumpstart install a preconfigured Solaris distribution automatically, without ever touching a key-

# **3.1** A Sample Solaris Jumpstart Rules File

```
# Example Solaris Jumpstart Rules File
network 1.2.3.0 - desktop_workstation set_root_pw
network 1.2.4.0 - compute_server set_root_pw
any - generic_server set_root_pw
```

The most significant limitation to Jumpstart is its network requirements. At least one boot server must be present on every subnet for your network, because Jumpstart clients (the servers you are loading) broadcast requests to the network look-ing for servers; broadcast traffic is usually used to local subnets. This can become a sig-nificant cost barrier to organizations with many different subnets and a management nightmare as well, since you would be managing not one, but several boot servers. The install servers, however, can be located anywhere on your network, though most people prefer to perform both functions on the same system.

# Consolidate Boot Servers

You can consolidate boot servers on multiple subnets in the same physical location by installing mul-iple network interfaces on a single boot server. Each interface could be connected to a different subnet, providing access from all of your subnets.

# Using Red Hat Kickstart

Red Hat Kickstart can install the Red Hat Linux operating system Red Hat on any machine from scratch. Kickstart shares many Jumpstart features, including partitioning, package select-ion, and post-installation scripts. But, like Jumpstart, Kickstart has its strengths and weaknesses.

On the upside is Kickstart's large number of data transfer options. With Jumpstart, NFS is your only option. With Kickstart, you can transfer packages and configurations to your client via NFS, FTP, CD-ROM, or another partition on the client's hard disk. The FTP option alone is