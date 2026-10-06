# Assigning Guest Accounts

Samba always assigns the permissions level of a valid user on the Linux system to clients who use the server. In the case of share security, the user is assigned a guest account (the nobody account by default).

If the guest account value isn't set, Samba goes through a fairly complex set of rules to determine which user account to use. The result is that it hard to ensure which user permissions will be assigned in each account. That's why user security is recommended if you want to provide more specific user access to your Samba server.

### Performance Options

Theocket Options option

The Socket Options option lets you pass options to the protocols Samba uses to communicate. The following options are set by default: TCP_NODELAY, SO_RCBUF=8192, and SO_SNDBUF=8192. The first option disables Nagle's algorithm, which is used to manage the transmission of TCP/IP packets. The other two set the maximum size of the socket receive and send buffer to 8192, respectively. These options are set to improve performance (reportedly up to ten times without setting these options). In general, you shouldn't change these options.

### Printing Options

The printing options are used to define how printer status is presented. For the overwhelming majority of Linux systems, the printing value is set to cups. You can use printing styles from other types of operating systems, such as UNIX V (sys), ARX (aix), HP UNIX (unix), and Berkeley UNIX (bsd), to name a few. LPring (lpring), offered by many UNIX systems, is also included. Other printing options enable you to redefine the location of basic printing commands (lpq, lpr, and so on) and printing files (such as the name of the printcap file).

### Browse Options

A browse is a list of computers that are available on the network to SMB servers. Clients use this list to find computers that are on their own LAN and also computers in their workgroups that may be reachable through networks.

In Samba, browsing is configured by options described later in this section and implemented by the nmbd daemon. If you are using Samba for a workgroup within a single LAN, you probably don't need to concern yourself with the browsing options. However, if you are using Samba to provide services across several physical subnets, you might want to consider configuring Samba as a domain master browser. Here are some points to think: