of a Linux operating system in a common way. For example, if you wanted to install a directory with employee benefits information, you could add a post-installation script that adds the appropriate cp commands to copy files from a network server.

# CERTIFICATION OBJECTIVE 2.04

# Administration with the Secure Shell

Red Hat Enterprise Linux installs the Secure Shell (SSH) packages by default. The RHCSA requirement with respect to SSH is simple; you need to know how to use it to access remote systems. Therefore, in this section, you’ll examine how to use the ssh command to access remote systems as a client.

As suggested earlier, the stage is already set by the default installation of SSH on standard installations of RHEL 6. While firewalls are enabled by default, the standard RHEL 6 firewall leaves port 22 open for SSH access. Related configuration files are stored in the /etc/ssh directory. Detailed server configuration is part of the RHCE requirements. Related client commands are scp and sftp, also covered in this section.

The Secure Shell daemon is secure because it encrypts messages. In other words, users who are listening on a network can’t read the messages that are sent between SSH clients and servers. And that’s important on a public network like the Internet. RHEL incorporates SSH version 2, which includes a key exchange algorithm, which is the enhancement relative to SSH version 1.

# Configure an SSH Client

The main SSH client configuration file is /etc/ssh/ssh_config. Individual users can have custom SSH client configurations in their ~/.ssh/config files. There are four directives included by default. First, the Host * directive applies the other directives to all connections.

```
Host *
```

This is followed by a directive that supports authentication using the Generic Security Services Application Programming Interface for client/server authentication:

```
GSSAPIAuthentication yes
```