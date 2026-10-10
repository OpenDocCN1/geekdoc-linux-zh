If you have BIND and BIND-utils installed on your computer, you can configure a caching nameserver by installing the `caching-nameserver` package. This sets up the `/etc/named.conf` configuration file, the `/var/named` directory, and the configuration files in `/var/named` (`localhost.zone`, `named.ca`, and `named.local`).

To start the caching nameserver, you can start the named service manually (see Chapter 11, “Automating Tasks”) or use the `system-config-services` GUI configuration tool. Choose the Services menu option in the Server Settings menu, which is in the System Settings menu, and then select named and click the Start button.

To get your local computer to use the caching nameserver, reconfigure the `/etc/resolv.conf` file to comment out any references to your ISP’s nameservers, and set the only nameserver to be the localhost (127.0.0.1). The `/etc/resolv.conf` for the caching nameserver host is as follows:

```
```text
#/etc/resolv.conf
#nameserver 83.64.1.10
#nameserver 83.64.0.10
nameserver 127.0.0.1
```
```

Other machines on your network should have the IP of the local caching nameserver in their `/etc/resolv.conf` files. Assuming that the IP address for the computer running the caching nameserver is 192.168.1.5, the `/etc/resolv.conf` files on the other machines on your network should be the following:

```
```text
#/etc/resolv.conf
#nameserver 83.64.1.10
#nameserver 83.64.0.10
Nameserver 192.168.1.5
```
```

# Ad Blocking with a Caching Nameserver

Another advantage of setting up a caching nameserver is that you can use it to block ads and objectionable sites by using bogus DNS zones to block specific domains. You can do this by overriding the DNS lookup of the sites you want to block. Configuration is simple. First, determine the sites that you want to block. For example, you might want to block all access to doubleclick.net. Create an entry in `/etc/named.conf` like this:

```
```text
zone “doubleclick.net” { type master; file “fakes”; };
```
```

Then create a new `/var/named/fakes` file. This should contain

```
```text
$TTL 1D
@       IN      SOA     dns.companyname.com. hostmaster.companyname.com. (
                        2004081701 8H 2H 4W 1D)

@       IN      NS      dns.companyname.example.com.
@       IN      A       127.0.0.1
*       IN      A       127.0.0.1
```
```