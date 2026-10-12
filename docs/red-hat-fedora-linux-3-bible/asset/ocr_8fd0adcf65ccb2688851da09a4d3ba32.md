```
```
setenv http_proxy http://maple:3128/
setenv gopher_proxy http://maple:3128/
setenv ftp_proxy http://maple:3128/
```
```

If you are using a ksh or bash shell, type the following:

```
```
export http_proxy=http://maple:3128
export gopher_proxy=http://maple:3128
export ftp_proxy=http://maple:3128
```
```

You can add any of these values to your start-up scripts. Or, to make them available on a system-wide basis, you could add them to a system configuration file, such as /etc/profile or /etc/skel/.bash_profile.

For the elinks and links browsers, you can indicate to use a proxy server in the /etc/elinks.conf file. For example, here are the lines you would add to the /etc/elinks.conf file to have elinks and links use the computer named maple act as a proxy for FTPand HTTP services:

```
```
protocol.ftp.proxy_host maple:3128
protocol.http.proxy_host maple:3128
```
```

# ## Summary

Connecting to the Internet opens a whole world of possibilities for your Fedora computer. Using Fedora as a public Web server, mail server, or FTP server depends on Fedora’s capability to connect to the Internet. Likewise, if your computers are already connected in a LAN, adding an Internet connection can provide Internet access to everyone on the LAN in one stroke.

Descriptions of how Internet domains are organized built on the coverage of IP addresses in the previous chapter. Creating dial-up connections to the Internet focused on descriptions of PPP. This chapter also discusses several different techniques for connecting your LAN to the Internet. You can set up your Fedora computer as a router or as a Squid proxy server.

To use your Internet connection to transport sensitive data to another location in your company’s private network, you can configure a VPN. This chapter describes how to use IPsec in Fedora to create a VPN connection between two locations.