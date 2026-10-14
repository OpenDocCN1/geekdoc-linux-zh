If everything works fine, you might want to have the rest of your applications use the proxy server. Some applications such as GNU wget use a proxy if certain system variables are declared. Other applications use the same behavior. The variables are http_proxy and ftp_proxy. To set them up, enter the following declarations in /etc/profile:

```
export http_proxy=http://localhost:3128
export ftp_proxy=http://localhost:3128
```

Now all applications that use these variables will use the proxy server.

# Access Control in Squid

The configuration that you just made is simple but good enough for home use. You told squid to allow all clients that are connecting from localhost. Localhost is your machine, which means that if another machine on the network attempts to use your proxy server, squid will not allow it to do so. Squid uses Access Control Lists (ACL) to define the entities that have access to its services. ACLs are an important concept to understand if you are to properly configure squid.

Actually, you have already used ACLs without knowing it—when you modified /etc/squid.conf to include the line http_access allow localhost. How do you suppose squid understood what localhost is? From a previous ACL. If you look at the section prior to the tag you modified, you will see the following line:

```
acl localhost src 127.0.0.1/255.255.255.255
```

An ACL statement starts with the tag acl, followed by the name of the access list you are defining. In this case, it's localhost. The src tag defines the sources of the access list, which are 127.0.0.1/255.255.255.255 in the case of localhost. So, this statement is saying "Define localhost as a machine that comes from 127.0.0.1/255.255.255.255."

Another important ACL is the all ACL. This is defined as the following:

```
acl all src 0.0.0.0/0.0.0.0
```

As you can tell by now, this ACL defines all to be any machine that matches the IP 0.0.0.0 with netmask 0.0.0.0, which is any machine. So, when you say http_access deny all, you are telling squid to deny all machines.

Squid uses ACL statements to know what to do with connecting clients. ACL statements are in the following form:

```
acl_name acl_type string
```

You can define many different ACLs that behave differently. The following are the most common source definition types:

+   - src—These ACLs are used to define client sources by using IPs. For example, you can define an ACL statement for one IP/Netmask like this:

```
acl someone src 192.168.168.17/255.255.255.255
```