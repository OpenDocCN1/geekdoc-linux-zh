runsocks works by adding the location of the SOCKS5 dynamic library to the front of the standard Linux $LD_LIBRARY_PATH, and effectively SOCKS-ifies any standard Linux network clients by replacing references to the commonly used Berkeley Sockets systems calls with their SOCKS5 equivalents.

Notice that the runsocks script is only effective for clients that have been compiled with support for dynamic loading of shared libraries. Applications that have been built to include static libraries cannot be executed by runsocks. Listing 10.4 shows how to use runsocks with the standard Linux ftp client to contact a remote FTP server (public.example.com) through a Proxy server (proxy.example.com). Note that there are three environment variables that need to be set prior to runsocks execution: $SOCKS5_SERVER, $SOCKS5_USER, and $SOCKS5_PASSWD. These variables specify which proxy server to use and the username and password to use for authenticating to the proxy server. These variables can also be defined in the libsocks5.conf file, which is explained in detail in the next section.

# Listing 10.4 Using the runsocks script

```
```
[ramon]$ export SOCKS5_SERVER=proxy.example.com
[ramon]$ export SOCKS5_USER=ramon
[ramon]$ export SOCKS5_PASSWD=mypassword
[ramon]$ runsocks ftp public.example.com
220 public FTP server (Version wu-2.4.2-VR(17))
Mon Apr 19 09:21:53 EDT 1999) ready.
Name (public.example.com,ramon): 
331 Password required for ramon.
Password:
230 User ramon logged in.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp>
```
```

# SOCKS5 Shared Library Configuration

In order to control the execution of the SOCKS5 library and the operation of the SOCKS5-ified clients, you must first create a configuration file, typically named /etc/ libsocks5.conf. The contents of this file are analogous to the proxy-type directives in /etc/socks5.conf, discussed earlier in this chapter. The primary purpose of this file is to define which target hosts should be reached via the proxy and which target hosts should be addressed directly. Consider the following lines from a libsocks5.conf file:

```
```
socks5 - - - 192.168.32.1
no proxy - - 192.168.32. - 
```
```