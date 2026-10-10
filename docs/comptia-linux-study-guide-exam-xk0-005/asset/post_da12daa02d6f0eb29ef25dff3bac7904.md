
## Real World Scenario
### Booting School VMs with Shell Scripts

A school environment is an excellent setting for using guest virtual machines, especially in computer science classes. VMs provide an economical and highly flexible solution.

On the servers, guest VMs are configured to employ either temporary or permanent storage, depending on class needs. For example, students who do not need long-term storage for their files on the VM are provided with guest virtual machines with transitory virtual disks. Students who do need to store and later access their files, such as programming students, are provided with guest machines with persistent storage.

These guest virtual machines are booted as needed via scripts. The scripts can be initiated by an instructor prior to class or scheduled via a cron job (covered in Chapter 26, “Automating Jobs”) or even via systemd timers (systemd was covered in Chapter 6, “Maintaining System Startup and Services”).

In the classroom, either thin clients or student (or school-provided) laptops are available for accessing the guest virtual machines. The configuration and deployment of such machines simplifies many school computing environment complications and typically lowers associated costs.

## Kickstarting with Anaconda

You can quickly and rather easily bootstrap a new system (physical or virtual) using the *kickstart installation method*. This RHEL-based technique for setting up and conducting a system installation consists of the following:

1. Create a kickstart file to configure the system.
2. Store the kickstart file on the network or on a detachable device, such as a USB flash drive.
3. Place the installation source (e.g., ISO file) where it is accessible to the kickstart process.
4. Create a boot medium that will initiate the kickstart process.
5. Kick off the kickstart installation.

## Creating the Kickstart File

A *kickstart file* is a text file that contains all the installation choices you desire for a new system. While you could manually create this file with a text editor, it is far easier to use an *anaconda file*. For Red Hat–based distros, at installation, this file is created and stored in the /root directory and is named anaconda-ks.cfg. It contains all the installation choices that were made when the system was installed.

> Ubuntu distributions do not create anaconda files at system installation. Instead you have to install the `system-config-kickstart` utility (the package name is `system-config-kickstart`) and use it to create your kickstart file. Ubuntu has a native bootstrapping product called `preseeds`. It may be wise to use it, as opposed to the Red Hat-based kickstart method. Also, openSUSE distributions have their own utility called `AutoYaST`, which is another bootstrap alternative to kickstart.

An example of a Rocky Linux 8 distribution’s anaconda file is shown snipped in Listing 29.4.

### Listing 29.4: Looking at the anaconda-ks.cfg file

```
# cat /root/anaconda-ks.cfg
#version=RHEL8
# Use graphical install
graphical

repo --name="AppStream" --baseurl=file:///run/install/sources/mount-0000-cdrom/AppStream

%packages
@workstation-product-environment
@gnome-apps
@graphical-admin-tools
@office-suite
@system-tools
kexec-tools

%end

# Keyboard layouts
keyboard --xlayouts='us'
# System language
lang en_US.UTF-8

# Network information
network  --bootproto=dhcp --device=enp0s3 --ipv6=auto --activate
network  --hostname=localhost.localdomain

# Use CDROM installation media
cdrom

# Run the Setup Agent on first boot
firstboot --enable

ignoredisk --only-use=sda
autopart
# Partition clearing information
clearpart --none --initlabel

# System timezone
timezone America/New_York --isutc

# Root password
rootpw  --iscrypted  $6$Q./K9AvLGaoptbn4g$0caapjRhps6RRx9pkyNuCL5gj@3Em4mkWSMmaVCfI2Rzg12o8RNU2lCLr3MUGFTsCGjrq48S1TBCL2Uwz26K4N0
%addon com_redhat_kdump --enable --reserve-mb='auto'

%end

%anaconda
pwpolicy root --minlen=6 --minquality=1 --notstrict --nochanges --notempty
pwpolicy user --minlen=6 --minquality=1 --notstrict --nochanges --emptyok
pwpolicy luks --minlen=6 --minquality=1 --notstrict --nochanges --notempty
%end
```

Notice in Listing 29.4 that the root password is stored in this file. If other user accounts are created at installation time, those are stored here as well. While the values are encrypted, the file should still be kept secured so as not to compromise any of your virtual or physical systems this file is used to bootstrap.

In order to create the kickstart file for a system installation, start with the anaconda file and copy it for your new machines. Typically ks.cfg is used as the kickstart filename. After that, open the file in a text editor and make any necessary modifications.

Kickstart files use a special syntax, and unfortunately there are no man pages describing it. Your best option is to open your favorite web browser and enter Kickstart Syntax Reference to find a Fedora or Red Hat documentation site.

![](img/c0a399aca0d18f8822d714ad0a173123_865_0.png)

> Don’t let kickstart file typographical errors cause installation problems.
> Besides giving the file a team review, use the *ksvalidator* utility to find syntax issues in a kickstart file.

## Storing the Kickstart File

For regular physical system installations, typically a configured kickstart file is stored on removable media (such as a USB flash drive) or somewhere on the network, if you plan on using a PXE or TFTP boot process. For virtual machine creation, you can store it locally on the host system. In any case, make sure the file is properly protected.

## Placing the Installation Source

The installation source is typically the ISO file you are employing to install the Linux distribution. However, you can also use an *installation tree*, which is a directory tree containing the extracted contents of an installation ISO file.

Often for a regular physical system, the ISO is stored on removable media or a network location. However, for a virtual machine, simply store the ISO or installation tree on the host system. You can even place it in the same directory as the kickstart file, as was done on the system shown in Listing 29.5.

### Listing 29.5: Viewing the *ks.cfg* and ISO files’ location

```
# ls /VM-Install/
ks.cfg ubuntu-20.04.1-live-server-amd64.iso
#
```

## Creating a Boot Medium

For a physical installation, the method and medium you choose depend on the various system boot options as well as the type of system on which you will be performing the installation. A simple method for servers that have the ability to boot from USB drives or DVDs is to store a bootable live ISO on one of these choices.

For a virtual machine installation, such as a virtual machine on a KVM hypervisor, there is no need to create a boot medium. This just gets easier and easier!

## Kicking Off the Installation

After you have everything in place, start the kickstart installation. For a physical system, start the boot process, reach a boot prompt, and enter a command like **linux ks=hd:sdc1:/ks.cfg**, depending on your hardware environment, your bootloader, and the location of your kickstart file.

For a virtual system, you can simply employ the *virt-install* command if it’s available on your host machine. Along with the other options used to create a virtual machine, you add two options similar to these:

```
--initrd-inject /root/VM-Install/ks.cfg
--extra-args="ks=file:/ks.cfg console=tty0 console=ttyS0,115200n8"
```

If desired, you can create a shell script with a loop and have it reissue the `virt-install` command multiple times to create/install as many virtual machines as you need.

## Initializing with Cloud-init

`Cloud-init` is a Canonical product (the same people who produce the Ubuntu distributions). It provides a way to bootstrap virtualized machines. On its Cloud-init.io website, Canonical describes it best: "Cloud images are operating system templates and every instance starts out as an identical clone of every other instance. It is the user data that gives every cloud instance its personality and cloud-init is the tool that applies user data to your instances automatically."

The cloud-init service is written in Python and is available for cloud-based virtualization services, such as Amazon Web Services (AWS), Microsoft Azure, and Digital Ocean as well as with cloud-based management operating systems, like OpenStack. And your virtual machines don’t have to be in a cloud to use cloud-init. It can also bootstrap local virtual machines using VMM (hypervisor) products like VMware and KVM. In addition, it is supported by most major Linux distributions. It is called an *industry standard* for a reason.

Cloud-init allows you to configure the virtual machine’s hostname, temporary mount points, and the default locale. Even better, pregenerated OpenSSH private keys can be created to provide encrypted access to the virtualized system. Customized scripts can be employed to run when the virtual machine is bootstrapped. This is all done through what is called `user-data`, which is either a string of information or data stored in files that are typically Yet Another Markup Language (YAML)-formatted files.

![](img/c0a399aca0d18f8822d714ad0a173123_866_0.png)

If you would like to take a look at the cloud-init utility, you can install it through the `cloud-init` package (package installation was covered in Chapter 13). It is available on most major Linux distributions.

The `/etc/cloud/cloud.cfg` file is the primary cloud-init configuration file. The command-line utility name is, as you might suspect, the `cloud-init` command. An example of using `cloud-init` to get help is shown in Listing 29.6.

### Listing 29.6: Employing the `-h` option to get help on the cloud-init command

```
$ cloud-init -h
usage: /usr/bin/cloud-init [-h] [--version] [--file FILES] [--debug] [--force]

{init,modules,single,query,dhclient-hook,features,analyze,develop,
collect-logs,clean,status} ...

optional arguments:
  -h, --help            show this help message and exit
```
