# CHAPTER 7 | Networks, Firewalls, and More

# rsync

The rsync service is frequently used for backups, as it can synchronize the data on two systems. The power of rsync comes from how it only transfers changed data over a network connection. Data transferred over rsync can be encrypted with the help of the SSH service.

# Samba

Samba is the Linux implementation of Microsoft file and printer sharing. SELLinux booleans in this area allow you to enable major Samba features. These features include the ability to act as a domain controller, and to read and write to shared directories, to use NFS directories, to share user home directories, and more.

# SASL Authentication Server

The Simple Authentication and Security Layer (SASL) server is another method to secure network authentication through the files of the shadow password suite. SELLinux disables such access by default.

# SELinux Service Protection

The SELinux service protection category allows you to disable SELLinux protection for a wide variety of applications and services, from the Amanda backup service to Xen for virtual machines.

# SpamAssassin

If you want SpamAssassin software to have access to the latest databases of unwanted e-mail, you'll want to allow the associated daemon to have network access.

# Squid

Squid is the standard Linux Web proxy server. As with SpamAssassin, you'll want to allow the associated daemon to have network access.

# SSH

SELinux policies related to SSH can enable administrative and host-based access. While administrative access via SSH is often the only secure way to administer remote systems, host-based access is inherently insecure.

# Universal SSL Tunnel

The Secure Sockets Layer (SSL) is one way to secure a tunnel for communication over a public network as the Internet. While it's frequently run as part of the extended internet super server, a SELinux boolean allows it to be more securely as a separate daemon.

# User Priv

Short for user privileges, the SELinux booleans in this section can support access by regular users to commands needed by some power users. These booleans support access from the record command to shared network directories, access to the ping command, and more.