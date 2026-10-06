worth it; with a high-bandwidth connection, you could easily install an entire distribution of Red Hat Linux over the network, using one of the many Red Hat mirrors on the Internet. All you have to do is provide a URL to the proper configuration file.

# Site Mirrors

A mirror is a site on the Internet that contains a copy of all or part of another site. Its purpose is to spread copies of heavily accessed data, such as software distributions, across the Internet so not everyone overloads a single site with requests for data. Red Hat has many different mirrors across the Internet, visit http://www.RedHat.com/mirrors.html for a comprehensive list.

The Kickstart configuration file can contain a great deal of hardware configuration information, because Linux must support an extraordinary amount of third-party hardware. The Kickstart config file also contains many directives for partitioning, network configuration, and software packages to be installed. Listing 3.2 shows a typical Kickstart configuration file.

# LISTING 3.2 A Sample Red Kickstart Configuration File

```
# Installation Language
lang en us
# Use DHCP to obtain a network address
network --bootproto dhcp
# Install over the network from an NFS share
nfs --server installer.example.com --dir /usr/local/Red Hat/i386
# Use US keyboard configuration
keyboard as us
# zero out the master boot record
zerombr yes
# format all existing partitions
clearpart --all
# partition information
# /home --will grow to use the rest of the disk, up to 8000 MB
part /boot --size 35
part swap --size 128
part / --size 200
part /user --size 4000
part /home --grow --maxsize 8000
# perform the installation
install
# use a generic 3-button PS/2 mouse
mouse a generic3ps/2
# set your timezone
timezone --utc EST5EDT
# skip X configuration since this is a server
skippx
# set the root password
rootpw changeme
# reboot after installation
reboot
```