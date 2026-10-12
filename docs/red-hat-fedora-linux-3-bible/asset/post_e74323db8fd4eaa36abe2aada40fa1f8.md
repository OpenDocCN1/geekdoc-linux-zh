
Web browser. The beauty of using proxy servers is in what your client computers don’t need to know, such as the following:

- Addresses of DNS servers
- Telephone numbers of ISPs
- Chat scripts to connect to the ISP

There are probably other things that clients don’t need to know, but you get the idea. After the proxy server has a connection to the Internet and has allowed a client computer on the LAN access to that service, all the client needs to know is the following:

- **Host name** — The name or IP address of the proxy server. (This assumes that the client can reach the proxy over the company’s LAN or other IP-based network.)
- **Port numbers** — The port number of the HTTP service (3128 by default). That same port number can be used for FTP and Gopher services as well.

How you go about setting up proxy service on the client has more to do with the browser you are using than with the operating system you are using. Follow the procedures outlined in the following sections for setting up Mozilla, Microsoft Internet Explorer, Mosaic, or lynx browsers.

## Configuring Mozilla to use a proxy

Normally, you would set up Mozilla to browse the Web over a TCP/IP connection to the Internet (over telephone lines or via a router on your LAN). Follow this procedure to change Mozilla to access the Web through your proxy server:

1. Open Mozilla.
2. Choose Edit $\rightarrow$ Preferences. The Preferences window appears.
3. Next to the Advanced category, click the plus sign and select Proxies.
4. Click Manual proxy configuration to open the Proxies window (see Figure 16-2).

![](img/b22364e57409c2481ba806e4e6b9309c_690_0.png)

5. Type the proxy server’s name or IP address in the address boxes for HTTP, FTP, and Gopher services.
6. Type the port number for HTTP services on your proxy server (probably 3128) in the Port boxes for HTTP, FTP, and Gopher services. (You can just fill in the information for the HTTP Proxy and click the “Use these settings for SSL, FTP and Gopher” button to have those other services filled in automatically.)
7. Click OK.

The next time you request a Web address from Mozilla, it will contact the proxy server to try to obtain the content.

## Configuring Internet Explorer to use a proxy

If you have Microsoft Windows clients on your network, you can configure them to use your Linux proxy server as well. To configure Internet Explorer to use your Linux proxy server to get to the Web, you need to change a few Internet options. Follow this procedure:

1. Open the Internet Explorer window.
2. Choose View (or Tools) $\rightarrow$ Internet Options. The Internet Options window appears.
3. Click the Connections tab.
4. Assuming you have a LAN already configured, click Local Area Network and then click LAN Settings. The Local Area Network Settings window should appear, as shown in Figure 16-3.

![](img/b22364e57409c2481ba806e4e6b9309c_691_0.png)

5. Click the Use a proxy server box so a checkmark appears.
6. Type the address of the proxy server and the port number for HTTP services (probably 3128).

> TIP: Microsoft Internet Explorer assumes that the same ports are used for HTTP, Gopher, and FTP services. If this is not true, click Advanced and change the port numbers for each service accordingly.

7. Click OK (in the Local Area Network Settings window) and OK again (in the Internet Options window).

The next time you try to access the Web from Internet Explorer, it will try to do so through the proxy server you defined.

## Configuring other browsers to use a proxy

There are different methods for indicating a proxy server to other browsers available with Linux. To have a Mosaic or lynx browser use a proxy server to access the Internet, add an environment variable to the shell where the browser will run. Here’s how you would set the environment variables for HTTP, Gopher, and FTP proxy services to a proxy computer named maple using a csh or tcsh shell:

```
setenv http_proxy http://maple:3128/
setenv gopher_proxy http://maple:3128/
setenv ftp_proxy http://maple:3128/
```

If you are using a ksh or bash shell, type the following:

```
export http_proxy=http://maple:3128
export gopher_proxy=http://maple:3128
export ftp_proxy=http://maple:3128
```

You can add any of these values to your start-up scripts. Or, to make them available on a system-wide basis, you could add them to a system configuration file, such as /etc/profile or /etc/skel/.bash_profile.

For the elinks and links browsers, you can indicate to use a proxy server in the /etc/elinks.conf file. For example, here are the lines you would add to the /etc/elinks.conf file to have elinks and links use the computer named maple act as a proxy for FTP and HTTP services:

```
protocol.ftp.proxy_host maple:3128
protocol.http.proxy_host maple:3128
```

## Summary

Connecting to the Internet opens a whole world of possibilities for your Fedora computer. Using Fedora as a public Web server, mail server, or FTP server depends on Fedora’s capability to connect to the Internet. Likewise, if your computers are already connected in a LAN, adding an Internet connection can provide Internet access to everyone on the LAN in one stroke.

Descriptions of how Internet domains are organized built on the coverage of IP addresses in the previous chapter. Creating dial-up connections to the Internet focused on descriptions of PPP. This chapter also discusses several different techniques for connecting your LAN to the Internet. You can set up your Fedora computer as a router or as a Squid proxy server.

To use your Internet connection to transport sensitive data to another location in your company’s private network, you can configure a VPN. This chapter describes how to use IPsec in Fedora to create a VPN connection between two locations.

![](img/b22364e57409c2481ba806e4e6b9309c_693_0.png)

# Chapter 17

# Setting Up a Print Server

## In This Chapter

- Understanding printing in Linux
- Setting up printers
- Using printing commands
- Managing document printing
- Sharing printers

Sharing printers is a good way to save money and make your printing more efficient. Very few people need to print all the time, but when they do want to print something, they usually need it quickly. Setting up a print server can save money by eliminating the need for a printer at every workstation. Some of those savings can be used to buy printers that can output more pages per minute or have higher-quality output.

You can attach printers to your Fedora Linux system to make them available to users of that system or to other computers on the network. You can configure your Fedora Linux printer as a remote CUPS printer or Samba printer. With Samba, you are emulating a Windows print server.

This chapter describes configuring and using printers in Fedora Linux. It focuses on Common UNIX Printing Service (CUPS), which is the recommended print service for the current version of Fedora Linux. To configure CUPS printers, this chapter focuses on the Fedora Printer Configuration window (system-config-printer command).

Once a local printer is configured, print commands (such as lpr) are available for carrying out the actual printing. Commands also exist for querying print queues (lpq), manipulating print queues (lpc), and removing print queues (lprm). A local printer can also be shared as a print server to users on other computers on your network.

## Common UNIX Printing Service

CUPS has become the standard for printing from Linux and other UNIX-like operating systems. Instead of being based on older, text-based line printing technology, CUPS was designed to meet today's needs for standardized printer definitions and sharing on IP-based networks (as most computer networks are today). Here are some features of CUPS:

- IPP — At its heart, CUPS is based on the Internet Printing Protocol (`www.pwg.org/ipp`), a standard that was created to simplify how printers can be shared over IP networks. In the IPP model, printer servers and clients who want to print can exchange information about the model and features of a printer using HTTP (that is, Web content) protocol. A server can also broadcast the availability of a printer, so a printing client can easily find a list of locally available printers.
- Drivers — CUPS also standardized how printer drivers are created. The idea was to have a common format that could be used by printer manufacturers that could work across all different types of UNIX systems. That way, a manufacturer only had to create the driver once to work for Linux, Mac OS X, and a variety of UNIX derivatives.
- Printer classes — Using printer classes, you can create multiple print server entries that point to the same printer or one print server entry that points to multiple printers. In the first case, multiple entries could each allow different options (such as pointing to a particular paper tray or printing with certain character sizes or margins). In the second case, you could have a pool of printers so that printing is distributed. This would decrease the occurrence of congested print jobs, caused by a malfunctioning printer or a printer that is dealing with very large documents.
- UNIX print commands — To integrate into Linux and other UNIX environments, CUPS offers versions of standard commands for printing and managing printers that have been traditionally offered with UNIX systems.

The Printer configuration window (`system-config-printer` command) lets you configure printers that use the CUPS facility. However, CUPS also offers a Web-based interface for adding and managing printers. Configuration files for CUPS are contained in the `/etc/cups` directory. In particular, you might be interested in the `cupsd.conf` file (which identifies permission, authentication, and other information for the printer daemon) and `printers.conf` (which identifies addresses and options for configured printers).

## Setting Up Printers

To install a printer from your desktop, use the Printer configuration window (`system-config-printer` command). This tool enables you to add printers, delete printers, and edit printer properties. It also lets you send test pages to those printers to make sure they are working properly.

The key here is that you are configuring printers that are managed by your print daemon (`cupsd` for the CUPS service). After a printer is configured, users on your local system can use it. After that, you can refer to the “Configuring Print Servers” section to learn how to make the server available to users from other computers on your network.
