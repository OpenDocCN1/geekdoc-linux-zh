proxy server, as well as the port it is using. Proxies usually make use of port 3128. To configure use of a proxy server running on the local sample network described in Chapter 5, you would enter the following in the Proxy configuration settings of your browser. The proxy server is running on **turtle.mytrek.com** (192.168.0.1) and using port 3128.

```
```192.168.0.1 3128```
```

On Firefox, Mozilla, and Netscape, the user on the sample local network would first select the Proxy panel located in Preferences under the Edit menu. Then, in the Manual proxy configuration's View panel, enter the previous information. The user will see entries for FTP, Gopher, HTTP, and Security proxies. For standard Web access, enter the IP address in the FTP, Gopher, and Web boxes. For their port boxes, enter 3128.

For GNOME, select Network Proxy in the Preferences menu or window, and for Konqueror on the KDE Desktop, select the Proxies panel on the Preferences | Web Browsing menu window. Here, you can enter the proxy server address and port numbers. If your local host is using Internet Explorer (such as a Windows system does), you set the proxy entries in the Local Area Network settings accessible from the Internet Options window.

On Linux or Unix systems, local hosts can set the **http_proxy**, **gopher_proxy** and **ftp_proxy** shell variables to configure access by Linux-supported Web browsers such as Lynx. You can place these definitions in your **bash_profile** or /etc/profile file to have them automatically defined whenever you log in.

```
```
http_proxy=192.168.0.1:3128
ftp_proxy=192.168.0.1:3128
gopher_proxy=192.168.0.1:3128
export http_proxy ftp_proxy gopher_proxy
```
```

Alternatively, you can use the proxy's URL.

```
```http_proxy=http://turtle.mytrek.com:3128```
```

For the Elinks browser, you can specify a proxy in its configuration file, /etc/elinks.conf. Set both FTP and Web proxy host options, as in:

```
```
protocol.http.proxy.host  turtle.mytrek.com:3128
protoco1.ftp.proxy.host   turtle.mytrek.com:3128
```
```

Before a client on a local host could use the proxy server, access permission would have to be given to it in the server's **squid.conf** file, described in the later section “Security.” Access can easily be provided to an entire network. For the sample network used here, you would have to place the following entries in the **squid.conf** file. These are explained in detail in the following sections:

```
```
acl mylan src 192.168.0.0/255.255.255.0
http_access allow mylan
```
```

> TIP Web clients that need to access your Squid server as a standard proxy cache will need to know the server's address and the port for Squid's HTTP services, which by default is 3128.