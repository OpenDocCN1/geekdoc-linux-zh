# Figure 6.346 IPv6 addrconf_sysctl: linux/net/ipv6/addrconf.c.

```
1886 static struct addrconf_sysctl_table
1887 {
1888     struct ctl_table_header *sysctl_header;
1889     ctl_table addrconf_vars[11];
1890     ctl_table addrconf_dev[2];
1891     ctl_table addrconf_conf[2];
1892     ctl_table addrconf_proto[2];
1893     ctl_table addrconf_root_dir[2];
1894 } addrconf_sysctl = {
1895     NULL,
1896     {NET_IPV6_FORWARDING, "forwarding",
1897     &ipv6_devconf.forward, sizeof(int), 0644, NULL,
1898     &addrconf_sysctl_forward;
1899
1900     {NET_IPV6_HOP_LIMIT, "hop_limit",
1901     &ipv6_devconf.hop_limit, sizeof(int), 0644, NULL,
1902     &proc_dointvec;
1903
1904     {NET_IPV6_MTU, "mtu",
1905     &ipv6_devconf.mtu6, sizeof(int), 0644, NULL,
1906     &proc_dointvec;
1907
```

# Figure 6.347 IPv6 addrconf_sysctl:linux/net/ipv6/addrconf.c.

```
1912     {NET_IPV6_ACCEPT_REDIRECTS, "accept_redirects",
1913     &ipv6_devconf.accept_redirects, sizeof(int), 0644, NULL,
1914     &proc_dointvec;
1915
1916     {NET_IPV6_AUTOCONf, "autoconf",
1917     &ipv6_devconf.autoconf, sizeof(int), 0644, NULL,
1918     &proc_dointvec;
1919
1920     {NET_IPV6_DAD_TRANSMITS, "dad_transmits",
1921     &ipv6_devconf.dad_transmits, sizeof(int), 0644, NULL,
1922     &proc_dointvec;
1923
1924     {NET_IPV6_RTR_SOLICITS, "router_solicitations",
1925     &ipv6_devconf.rtr_solicits, sizeof(int), 0644, NULL,
1926     &proc_dointvec;
1927
1928     {NET_IPV6_RTR_SOLICIT_INTERVAL, "router_solicitation_interval",
1929     &ipv6_devconf.rtr_solicit_interval, sizeof(int), 0644, NULL,
1930     &proc_dointvec_jiffies;};
1931
1932     {NET_IPV6_RTR_SOLICIT_DELAY, "router_solicitation_delay",
1933     &ipv6_devconf.rtr_solicit_delay, sizeof(int), 0644, NULL,
```