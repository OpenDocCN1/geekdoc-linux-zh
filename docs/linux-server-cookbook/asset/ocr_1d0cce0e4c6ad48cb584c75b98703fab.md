![](bbox=[0.13, 0.07, 0.88, 0.7])

*Figure 8.2: Firewalld structure. Source: firewalld*

The command `firewall-cmd` communicates with the service `firewalld` to operate with rules and zones. The service will use the backend defined, by default `nft`, to configure the rules indicated.

The default configuration file for `firewalld` is located on `/etc/firewalld/firewalld.conf`. The following code contains an example of the default configuration values: