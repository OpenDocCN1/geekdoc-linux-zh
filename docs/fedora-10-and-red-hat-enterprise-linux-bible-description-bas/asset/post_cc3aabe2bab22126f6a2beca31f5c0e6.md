
# Part IV: Fedora RHEL Network and Server Setup

- **Hostname** — The name or IP address of the proxy server. (This assumes that the client can reach the proxy over the company's LAN or other IP-based network.)
- **Port numbers** — The number of the HTTP service (3128 by default). That same port number can be used for FTP service as well.

How you go about setting up proxy service on the client has more to do with the browser you are using than the operating system you are using. Follow the procedures outlined in the following sections for setting up Firefox, Microsoft Internet Explorer, Mosaic, or lynx browsers.

# Configuring Firefox to use a proxy

Normally, you would set up Firefox to browse the Web directly over a TCP/IP connection to the Internet (over telephone lines or via a router on your LAN). Follow this procedure to change Firefox to access the Web through your proxy server:

1. Open Firefox.
2. Choose Edit → Preferences. The Preferences window opens.
3. Select the Advanced category and select the Network tab.
4. Click the Settings button. Connection Settings window appears.
5. Click Manual proxy configuration to enable proxy configuration (see Figure 16-2 for an example of the Firefox Connection Settings pages).

![](img/63c86e1d25a0e2be7e9f6de6b6f02530_775_0.png)

Figure 16-2: The Preferences window identifies proxy servers and port numbers in Firefox.

# Chapter 16: Connecting to the Internet 729

6. Type the proxy server's name or IP address in the address boxes for HTTP, FTP, and Gopher services.
7. Type the port number for HTTP services on your proxy server (probably 3128) in the Port boxes for HTTP, FTP, and Gopher services. (You can just fill in the information for the HTTP Proxy and check the Use proxy for all protocols option to have those services filled in automatically.)
8. Click OK.

The next time you request a Web address from Firefox, it will contact the proxy server to obtain the content.

# Configuring other browsers to use a proxy

There are different methods for indicating a proxy server to other browsers available with Linux. To make a Mosaic or lynx browser use a proxy to access the Internet, add an environment variable to the shell where the browser will run. Here's how you would set the environment variables for HTTP and FTP proxy services to a proxy computer named maple using a csh or tcsh shell:

```
setenv http_proxy=http://maple:3128/
setenv ftp_proxy=http://maple:3128/
```

If you are using a csh or bash shell, type the following:

```
export http_proxy=http://maple:3128
export ftp_proxy=http://maple:3128
```

You can add any of these values to your start-up scripts. Or, to make them available on a system-wide basis, you could add them to a system configuration file, such as /etc/profile or /etc/skel/.bash_profile.

For the elinks and links browsers, you can indicate to use a proxy server in the /etc/elinks.conf file. For example, here are the lines you would add to the /etc/elinks.conf file to have elinks and links as a proxy for FTP and HTTP services:

```
protocol.http.proxy.host maple: 3128
protocol.http.proxy.host maple: 3128
```

# Summary

Connecting to the Internet opens a whole world of possibilities for your Fedora or RHEL computing. Using Fedora or RHEL as a public Web server, mail server, or FTP server depends on its capability to connect to the Internet. Likewise, if your computers are already connected in a LAN, adding an Internet connection can provide Internet access to everyone on the LAN in one stroke.

Descriptions of how Internet domains are organized built on the coverage of IP addresses in the previous chapter. Creating dial-up connections to the Internet focused on descriptions of PPP. This chapter also discusses several different techniques for connecting your LAN to the Internet. You can set up your Linux computer as a router or as a Squid proxy server.

To use your Internet connection to transport sensitive data to another location in your company’s private network, you can configure a VPN. This chapter describes how to use IPSec in Fedora and RHEL to create a VPN connection between two locations.

# Chapter 17

# Setting Up Printers and Printing

In This Chapter

- Understanding printing in Linux
- Setting up printers
- Using printing commands
- Managing document printing
- Sharing printers

Sharing printers is a good way to save money and make your printing more efficient. Very few people need to print all the time, but when they do want to print something, they usually need it quickly. Setting up a print server can save money by eliminating the need for a printer at every workstation. Some of savings can be used to buy printers that can output more pages per minute or have higher-quality output.

You can attach printers to your Fedora or RHEL system to make them available to users of that system or to other computers on the network. You can configure your Fedora or RHEL printer as a remote CUPS printer or Samba printer. With Samba, you are emulating a Windows print server.

This chapter describes configuring and using printers in Fedora or RHEL. It focuses on Common UNIX Printing Service (CUPS), which is the recommended service for the current versions of Fedora and RHEL. To configure CUPS printers, this chapter focuses on the Printer Configuration window (system-config-printer command).

When a local printer is configured, print commands (such as `lpr`) are available for carrying out the actual printing. Commands also exist for querying print queues (`lpq`), manipulating print queues (`lpc`), and removing print jobs (`lprrm`). A local printer can also be shared as a print server to other computers on your network.

## Common UNIX Printing Service

CUPS has become the standard for printing from Linux and other UNIX-like operating systems. Instead of being based on older, text-based line printing technology, CUPS was 732 Part IV: Fedora and RHEL Network and Server Setup designed to meet today's needs for standardized printer definitions and sharing on IP-based networks (as most computers are today). Here are some features of CUPS:

- IPP — At its heart, CUPS is based on the Internet Printing Protocol (www.pwg.org/ipp), a standard that was created to simplify how printers can be shared over IP networks. In the IPP model, printer servers and clients who want to print exchange information about the model and features of a printer using the HTTP protocol. A server can also broadcast the availability of a printer, so a printer client can easily find a list of locally available printers.
- Drivers — CUPS also standardized how printer drivers are created. The idea was to have a common format that could be used by printer manufacturers to work across all types of UNIX systems. That way, a manufacturer could create the driver only once for Linux, Mac OS X, and a variety of UNIX derivatives.
- Printer classes — Using printer classes, you can create multiple print servers that point to the same printer or one server entry that points to multiple printers. In the first case, multiple entries could allow each other options (such as pointing to a particular paper tray or printing with certain character sizes or margins). In the second case, you could have a pool of printers that is distributing. This would decrease the occurrence of congested print jobs, caused by a malfunctioning printer or a printer that is dealing with large documents. To integrate into Linux and other UNIX environments, CUPS offers versions of standard commands for printing and managing printers that have been traditionally used in UNIX systems.

The Printer configuration window (system-config-printer command) lets you configure printers in Fedora and RHEL that use the CUPS facility. However, CUPS also offers a Web-based interface for adding and managing printers. Configuration files for CUPS are contained in the /etc/cups directory. In particular, you might be interested in the cupsd.conf file (which identifies permission, authentication, and other information for the printer daemon) and printers.conf (which identifies addresses and options for configured printers).

# Setting Up Printers

Most parallel printers and USB printers can be detected and set up using the Printer configuration window. However, the Printer configuration window also lets you configure Fedora or RHEL so you can use printers that are available on your LAN as a Windows printer (Samba), AppleSocket or HP JetDirect, Internet Printing Protocol (IPP) printer, or UNIX printer (LPD or LRP daemons).
