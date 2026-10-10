fast and handy when no graphical environment is available, such as when used in scripts.

# 10.3.3.3 Proxy servers

# 10.3.3.3.1 What is a proxy server?

Companies and organizations often want their users to use a proxy server. Especially in environments with lots of users, a proxy server can enable faster downloads of web pages. The proxy server stores web pages. When a user asks for a web page that has already been requested previously, the proxy server will give that page to the user directly, so that s/he does not need to get it from the Internet, which would take longer. Of course, measures can be taken so that the proxy server does a quick check and always serves the most recent version of a page. In some environments, usage of the proxy server is compulsory, in other environments you may have the choice whether or not to use it.

# 10.3.3.3.2 Proxy configuration

If you have the proxy server name and port, it should be rather obvious to feed that information into your browser. However, many (command line) applications depend on the variables **http_proxy** and **ftp_proxy** for correct functioning. For your convenience, you might want to add a line like the following to your ~/.bashrc:

```
export http_proxy=http://username:password@proxy_server_name:port_number
```

For instance:

```
export http_proxy=http://willy:Appelsj3ntj3@proxy:80
```

If you do not need to give a username and password, simply leave out everything before the "@" sign, this sign included.

# 10.3.4 File Transfer Protocol

# 10.3.4.1 FTP servers

On a Linux system, an FTP server is typically run from **xinetd**, using the WU-ftp'd server, although the FTP server may be configured as a stand-alone server on systems with heavy FTP traffic. See the exercises.

Other FTP servers include among others vsftpd, Ncftpd and Proftpd.

Most Linux distributions contain the anonftp package, which sets up an anonymous FTP server tree and accompanying configuration files.