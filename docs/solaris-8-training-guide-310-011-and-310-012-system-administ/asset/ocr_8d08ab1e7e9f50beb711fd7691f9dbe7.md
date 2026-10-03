# /etc/hosts

The /etc/hosts file was described in Chapter 13, “The Solaris Network Environment.” The /etc/hosts file is the local file that associates the names of hosts with their IP addresses. The boot server references this file when trying to match an entry from the local /etc/ethers file in response to a RARP request from a client. In a name service environment, this file would be controlled by NIS. See Chapter 18, “Name Services,” for more information on how this file can be managed by NIS.

# /tftpboot

/tftpboot is a directory that contains the inetboot.SUN4x.Solaris_8-1 file that is created for each JumpStart client when the add_install_client script is run.

The client’s IP address is expressed in hexadecimal format. This link points to a boot program for a particular Solaris release and client architecture.

When booting over the network, the JumpStart client’s boot PROM makes a RARP request, and when it receives a reply, the PROM broadcasts a TFTP request to fetch the inetboot file from any server that responds and executes it. See how this directory is configured in the section titled “Setting Up Clients.”

# /etc/dfs/dfstab

The /etc/dfs/dfstab file lists local file systems to be shared to the network. This file is described in detail in Chapter 17, “The NFS Environment.”

# /etc/bootparams

The /etc/bootparams file contains entries that network clients use for booting. JumpStart clients retrieve the information from this file by issuing requests to a server running the rpc.bootparamd program. See the section titled “Setting Up Clients” later in this chapter for more information on how this file is configured.