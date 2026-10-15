Server-side components can all be located on the same machine. The servers are release- and platform independent. For example, a SPARC-based Solaris 9 boot and install server can offer installation services for x86 Solaris 10 clients.

Since netboot parameters can be included in DHCP responses, you can use a DHCP server as an alternative to a dedicated JumpStart boot server. DHCP is probably the better option for x86 systems that use PXE booting and for client systems on a different subnet from the install server. We discuss only the same-subnet case here; refer to docs.sun.com/doc/817-5504 for more details.

Setting up an install server is straightforward. The setup tools are on the Solaris CD or DVD media. Insert the Solaris medium into the drive on the install server and run commands such as the following to configure a simple install server:

```
solaris$ sudo mkdir -p /jumpstart/s10sparc
solaris$ cd /cdrom/cdrom0/Solaris_10/Tools
solaris$ sudo ./setup_install_server /jumpstart/s10sparc
```

Here, we transfer the SPARC installation files to the /jumpstart/s10sparc directory on the install server. The setup_install_server script copies the files and adds the appropriate hooks for network-based installations. If only CD media are available, use the add_to_install_server command to replicate the contents of multiple CDs to the server.

Several files configure the automated installation tasks:

+   - A rules file identifies clients and assigns installation profiles.
+   - Individual profile files specify disk partition layout, packages to install, and other system details.
+   - A sysidcfg file provides preconfigured answers to installation questions.
+   - Optionally, shell scripts can run before and after the installation process.

When a client requests a network installation, JumpStart uses the rules file to identify it according to attributes such as the client's hostname, subnet, or model. If the attributes match, JumpStart reads installation details from the appropriate profile, answers installation questions with sysidcfg, and executes any custom scripts before and after installation.

The first step in creating a JumpStart configuration is to create a directory to hold all the various configuration files:

```
solaris$ sudo mkdir -m 755 /jumpstart/config
```

This directory must be shared through NFS or HTTP so that clients can access it. For example, to share by NFS, add the line

```
share -F nfs /jumpstart
```

to /etc/dfs/dfstab and run shareall to initiate NFS service.