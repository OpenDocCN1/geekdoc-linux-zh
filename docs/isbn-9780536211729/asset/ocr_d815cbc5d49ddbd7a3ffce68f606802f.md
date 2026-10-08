# 7.5 Enabling Common TCP Services

```
-d $IPADDR --dport 443 \\n-m state --state NEW -j ACCEPT
```

```
$IPT -A INPUT -i INTERNET -p tcp \\n--sport $UNPRIVORTS \\n-d $IPADDR --dport 443 -j ACCEPT
```

```
$IPT -A OUTPUT -o INTERNET -p tcp ! --syn \\n-s $IPADDR --dport 443 \\n--dport $UNPRIVORTS -j ACCEPT
```

# WEB PROXY ACCESS (TCP Ports 8008, 8080)

Publicly accessible web server proxies are most common at ISPs. As a customer, you configure your browser to use a remote proxy service. Web proxies are accessed through one of two privileged ports for this purpose, ports 8008 or 8080, as defined by the ISP. In return, you get faster page access when the pages are easily cached at your ISP's server and the relative anonymity of proxied access to remote sites. Your connections are not direct, but instead are done on your behalf by your ISP's proxy. Table 7.10 lists the complete client/server connection protocol for the web proxy service.

| Description | Protocol | Remote Address | Remote Port | In/Out | Local Address | Local Port | TCP Flag |
|---|---|---|---|---|---|---|-|
| Local client request | TCP | WEB PROXY SERVER | WEB PROXY PORT | Out | IPADDR | 1024:65535 | |
| Remote server response | TCP | WEB PROXY SERVER | WEB PROXY PORT | In | IPADDR | 1024:65535 | ACK |

Table 7.10 Web Proxy Protocol

If you use a web proxy service offered by your ISP, the specific server address and port number will be defined by your ISP. The client rules are as follows:

```
WEB_PROXY_SERVER="my.proxy" # ISP Web proxy server, if any
WEB_PROXY_PORT="my.proxy.port" # ISP Web proxy port, if any
# typically 8008 or 8080
```

```
if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A OUTPUT -o INTERNET -p tcp \\n-s $IPADDR --sport $UNPRIVORTS \\n-d $WEB_PROXY_SERVER --dport $WEB_PROXY_PORT \\n-m state --state NEW -j ACCEPT
```

fi