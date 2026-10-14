
```
keyboard us
#System mouse
mouse
#System timezone
timezone America/Los_Angeles
#Root password
rootpw --disabled
#Initial user
user ubuntu --fullname "ubuntu" --password insecure
#Reboot after installation
reboot
#Use text mode install
text
#Install OS instead of upgrade
install
#Use CDROM installation media
cdrom
#System bootloader configuration
bootloader --location=mbr
#Clear the Master Boot Record
zerombr yes
#Partition clearing information
clearpart --all --initlabel
#Disk partitioning information
part / --fstype ext3 --size 1 --grow --asprimary
part swap --recommended
#System authorization information
auth --useshadow --enablemd5
#Firewall configuration
firewall --disabled
#Do not configure the X Window System
skipx
# This section was added by hand
preseed base-installer/kernel/override-image string linux-server
preseed pkgsel/language-pack-patterns string
preseed pkgsel/install-language-support boolean false
%packages
@ standard
@ ubuntu-server
```

As I did with the preseed file, I set up a single / partition with the --grow option so that it filled the entire drive (actually I just toggled that setting within the GUI). Then I copied this ks.cfg file to the same Web server I used before. One other great thing about using this Kickstart file is that I don’t have to manually enter a lot of settings at boot. In fact, all I need to do is replace the file preseed option that is already there with an option that points to my Kickstart file. Boot the CD-ROM and then press F6 to

These settings already are managed in a Kickstart file in the %packages section, but if they weren’t you could set this setting with

```
preseed --owner tasksel tasksel/first multiselect \
standard, ubuntu-server
```

## Account options

Two other major additions in the Kickstart syntax provide extra options for account management. Because Ubuntu disables the root user by default, the rootpw Kickstart command now can take the --disabled option. This disables the root password and gives the first user root privileges from sudo.

The Ubuntu Kickstart file has also added a user command to add settings for the initial user. The syntax for this command is

```
user --disabled | username [--fullname "Firstname Lastname"] \
--password insecure [--iscrypted]
```

This command either takes the --disabled option to disable an initial user altogether or takes as options the username, optionally the user’s full name, and finally the password. By default the password is in plain text, but you can optionally list the MD5 hash for the password; just be sure to add the --iscrypted option so that Kickstart knows.

## Limitations

Currently the Ubuntu Kickstart does not implement the full range of features of Red Hat’s Kickstart. These limitations are one reason for advocating a combination of Kickstart and preseeding. The Kickstart file can take care of the base configuration, and where features aren’t available, they can be supplemented by preseed options. Here is a list of major features not yet implemented in Ubuntu’s Kickstart:

- There is no LDAP, Kerberos 5, Hesios, or Samba authentication.
- There are no bootloader --linear, --nonlinear, or --lba32 options for lilo.
- There is no lilocheck command.
- Ubuntu handles system upgrades outside of the Kickstart file.
- Partitioning in Ubuntu’s Kickstart is not yet as full-featured. As a result, if you have more sophisticated partitioning in mind, I recommend supplementing this with preseed options. Here are the current partitioning limitations:
  - Can partition only the main disk
  - No LVM configuration
  - No bad sector checks
  - No RAID partitions
- You cannot restrict a partition to a particular disk or specify the starting or ending cylinder.
- There is no support for a supplemental driver disk during install.
- The device command is not supported.
- Firewall configuration is not supported.
- There is no automated discovery of Kickstart source via DHCP; you must specify Kickstart source explicitly.
- NFS and local disk are not supported as installation sources.
- The xconfig --monitor option is not supported (selects a specific monitor name).
- Package groups in Ubuntu and Red Hat have different names and under Ubuntu, package groups reference Ubuntu tasks instead.
- You cannot exclude packages in the %packages section.
- You can use shell scripts only in pre- and post-installation sections.

## Run Custom Commands during the Install

Like preseeding, Kickstart supports running custom commands during the install. Also like preseeding, this is done via a pre-install and a post-install script. In a Kickstart file these are defined in %pre and %post sections. Any shell commands you place in those sections will be executed immediately before or after the install process, respectively. A nice feature of these scripts in Kickstart is that they can span multiple lines as long as they stay within the %pre or %post section.
