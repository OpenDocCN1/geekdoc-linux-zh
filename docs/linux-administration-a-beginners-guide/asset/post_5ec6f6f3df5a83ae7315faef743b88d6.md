
## Table 21-2. Options Available with lp

Most of the time, the only parameter you'll use with `lp` is `-P`, which is helpful when you need to print to a printer other than your default.

| 1pr Options | Description |
| :--- | :--- |
| `-P` | Send job to another printer (not the default printer). |
| `-m` | Send mail upon completion of the job. |
| `-r` | Remove the file once it's been spooled for printing. (This parameter may not be used together with the `-8` option.) |
| `-8` | Instead of making a copy of the file for the spool, use symbolic links instead. Note: If you use this option, you cannot change the file in any way until the print job is complete; however, this is a handy option for very large files. |
| `#n` | Specifies number of copies to print of each file listed; *n* is the number of copies. |
| `-l cols` | Indent the printed output by *cols* number of columns. |

### lprm

The `lprm` tool allows you to remove print jobs that have entered the print queue but have not yet started printing yet. Here are the command line parameters for `lprm`:

| lprm Parameters | Description |
| :--- | :--- |
| `-P` *printername* | Specifies which printer (*printername*) from which the print job should be removed. Otherwise, the default printer (the first one listed in the /etc/printcap file) is assumed. |
| `-` | Removes all jobs that the user owns from the specified printer. |
| *Number* | Removes job *Number* from the queue. If you aren't sure what your job number is, use the `lpr` command to see what the print queue says. |

Here's an example of an `lprm` command to remove job number 17 from the printer named zaphod:

```bash
[root@ford /root]# lprm -P zaphod 17
```

### lpq

The `lpq` program lists all jobs queued for the printer in the order in which they will be printed. Typically, the first job listed is actively printing. The exception is, of course, when there is a problem with the printer itself.

The only command-line parameter needed with `lpq` is the `-P` option, which is used to specify which printer's queue you want to see. The default for `lpq` is the first printer listed in the `/etc/printcap` file. Here's an example that shows what's listed in the queue for the printer zaphod:

```bash
[root@ford /root]# lpq -P zaphod
```

### SUMMARY

This chapter explained how to set up the printer server software (`lpd`) under Linux, and described the corresponding client tools for use along with the software. Printing is a mostly automated task; once it's set up, it rarely needs additional attention. In fact, most problems with printing generally concern the printer itself.

This chapter also presented the process of setting up a basic printer configuration, how to set up printers for network usage, and even for use with remote printers hosted by Windows-based servers. These options give you substantial flexibility in print operations! For instance, a server I managed not too long ago tied together several generations of printers. By taking advantage of the filtering available in `lpd`, with Samba's `smbj1ant` tool and the Netatalk application (which allows access to AppleTalk printers), I was able to unify all printing services to one server and make them available to all users regardless of operating system.

## CHAPTER 22

## DHCP

Configuring IP addresses for a handful of servers is a fairly simple task. However, manually configuring IP addresses for an entire department, building, or enterprise of heterogeneous systems can be daunting.

The Linux DHCP (Dynamic Host Configuration Protocol) client and server can assist with these tasks. The client machine is configured to obtain its IP address from the network. When the DHCP client software is started, it broadcasts a request onto the network for an IP address. If all goes well, a DHCP server on the network will respond, issuing an address and other necessary information to complete the client's network configuration.

Such dynamic addressing is also useful for configuring mobile or temporary machines. Folks who travel from office to office can plug their machines into the local network and obtain an appropriate address for their location.

In this chapter, we'll cover the process of configuring a DHCP server and client. This includes compiling and installing the necessary software and then stepping through the process of writing a configuration file for it. At the end of the chapter, we'll step through a complete sample configuration.

> **TIP:** DHCP is a standard. Thus, any operating system that can communicate with other DHCP servers and clients can work with the Linux DHCP tools. One common solution that includes using the Linux DHCP server component is in office environments where there are a large number of Windows based clients. The Windows systems can be configured to use BOOTP (Boot Protocol), obtaining their IP address. This reduces the need for yet another Windows NT server and the associated licensing costs surrounding it.

### The Roots of DHCP

Long before the fad of network computers (NCs), and back when disk storage space was at a premium cost, network workstation manufacturers built machines with no local hard drives, mounting them from a shared server instead. These “diskless” machines would boot using a protocol known as BOOTP (Boot Protocol), obtaining their addresses from a server. The Dynamic Host Configuration Protocol (DHCP) was originally derived from the BOOTP protocol. In fact, much of the DHCP protocol was taken directly from BOOTP.

### The Mechanics of DHCP

When a client is configured to obtain its address from the network, it asks for an address in the form of a DHCP request. A DHCP server listens for client requests. Once a request is received, it checks its local database, and it issues an appropriate response. The response always includes the address and can include name servers, a network mask, and a default gateway. The client accepts the response from the server and configures its local settings accordingly.

The DHCP server maintains a list of addresses it can issue. Each address is issued with an associated “lease,” which dictates how long a client is allowed to use the address before it must contact the server to renew the address. When the lease expires, the client is not allowed to use the address.

The implementation of the Linux DHCP server includes several key features common to many DHCP server implementations. The server can be configured to issue any free address from a pool of addresses or to issue a specific address to a specific machine. In addition to serving DHCP requests, the Linux DHCP server also serves BOOTP requests.

### The DHCP Server

DHCPD, the DHCP server, is responsible for serving IP addresses and other relevant information upon client request. Since the DHCP protocol is broadcast-based, a server will have to be present on each subnet for which DHCP service is to be provided.

#### Downloading, Compiling, and Installing a DHCP Server

The ISC DHCP server is the de facto implementation for Unix machines. This version is released with many Linux distributions. If it has not been found in a distribution, the source for the ISC DHCP server can be obtained from the ISC site at http://www.isc.org. As of this writing, the most current version of the server is 3.0p10.

Once the package is downloaded, unpack the software as shown. For this example, assume the source directory is `/usr/local/src`:

```bash
[root@delirium src]# tar -xvzf dhcp-3.0p10.tar.gz
```

Enter the directory and configure the package with the `configure` command:

```bash
[root@delirium dhcp-3.0p10]# ./configure
```

Currently, `--with-nsupdate` is the only optional parameter available to the `configure` command. This option is invoked if Bind 8.2 is installed, and dynamic DNS support is desired in the DHCP server.

To compile and install, issue the `make; make install` commands:

```bash
[root@delirium dhcp-3.0p10]# make; make install
```

#### Configuring the DHCP Server

The primary configuration file of the ISC DHCP server is `/etc/dhcpd.conf` by default. The configuration file encapsulates two ideas:

- A set of declarations to describe the networks, hosts, or groups attached to the system and possibly the range of addresses issuable to each respective entity. Multiple declarations can be used to describe multiple groups of clients. Declarations can also be nested in one another when multiple concepts are needed to describe a set of clients or hosts.
- A set of parameters that describe the behavior of the server and configure appropriate responses. Parameters can be global, or local to a set of declarations.

> **NOTE:** Since every site has a unique network with unique addresses, it is necessary that every site be set up with its own configuration file. If this is the first time you are dealing with DHCP, you might want to start with the sample configuration file presented toward the end of this chapter and modify it to match your network's characteristics.

Like most configuration files in UNIX, the file is ASCII text and can be modified using your favorite text editor. The general structure of the configuration file is as follows:

```text
Global parameters:
Declaration1 {
    [parameters related to declaration1]
    [nested sub declaration]
}
Declaration2 {
    [parameters related to declaration2]
    [nested sub declaration]
}
...
```

As the above outline indicates, a declaration block groups a set of clients. Different parameters can be applied to each block of the declaration.
