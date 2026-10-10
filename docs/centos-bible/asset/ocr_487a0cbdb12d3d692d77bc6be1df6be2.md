+   7. Type the port number for HTTP services on your proxy server (probably 3128) in the Port boxes for HTTP, FTP, and Gopher services. You can just fill in the information for the HTTP Proxy and check the "Use this proxy server for all protocols" option to have those other services filled in automatically.

+   8. Click OK.

The next time you request a web address from Firefox, it will contact the proxy server to try to obtain the content.

# Configuring Other Browsers to Use a Proxy

There are different methods for indicating a proxy server to other browsers available with Linux. To have a Mosaic or Lynx browser use a proxy server to access the Internet, add an environment variable to the shell where the browser will run. Here's how you would set the environment variables for HTTP and FTP proxy services to a proxy computer named `maple` using a `csh` or `tcsh` shell:

```
```
setenv http_proxy http://maple:3128/
setenv ftp_proxy http://maple:3128/
```
```

If you are using a `ksh` or `bash` shell, type the following:

```
```
export http_proxy=http://maple:3128
export ftp_proxy=http://maple:3128
```
```

You can add any of these values to your start-up scripts. Or, to make them available on a system-wide basis, you could add them to a system configuration file, such as `/etc/profile` or `/etc/skel/.bash_profile`.

For the `elinks` and `links` browsers, you can indicate to use a proxy server in the `/etc/elinks.conf` file. For example, here are the lines you would add to the `/etc/elinks.conf` file to have `elinks` and `links` use the computer named `maple` act as a proxy for FTP and HTTP services:

```
```
protocol.ftp.proxy.host maple:3128
protocol.http.proxy.host maple:3128
```
```

# Summary

Connecting to the Internet opens a whole world of possibilities for your CentOS system. Using your system as a public Web Server, mail server, or FTP server depends on its capability to connect to the Internet. Likewise, if your computers are already connected in a LAN, adding an Internet connection can provide Internet access to everyone on the LAN in one stroke.