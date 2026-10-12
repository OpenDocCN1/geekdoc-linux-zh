band (and preferably quantum safe). The PPK's should be very strong in randomness and not be based on dictionary words. The PPK ID and PPK data itself are stored in `ipsec.secrets`, for example:

```
@west @east : PPKS "user1" "thestringismeant tobearandomstr"
```

The **PPKS** refers to static PPKs. There is an experimental function to use one-time-pad based Dynamic PPKs. Upon each connection, a new part of a onetime pad is used as the PPK. When used, that part of the dynamic PPK inside the file is overwritten with zeroes to prevent re-use. If there is no more one time pad material left, the connection fails. See the `ipsec.secrets(5)` man page for more information.

> **WARNING**
> 
> The implementation of dynamic PPKs is provided as a Technology Preview and this functionality should be used with caution. See the **Red Hat Enterprise Linux 7.5 Release Notes** for more information.

# ### 4.6.10. Additional Resources

The following sources of information provide additional resources regarding Libreswan and the `ipsec` daemon.

# #### 4.6.10.1. Installed Documentation

+   * `ipsec(8)` man page – Describes command options for `ipsec`.
+   * `ipsec.conf(5)` man page – Contains information on configuring `ipsec`.
+   * `ipsec.secrets(5)` man page – Describes the format of the `ipsec.secrets` file.
+   * `ipsec_auto(8)` man page – Describes the use of the `auto` command line client for manipulating Libreswan IPsec connections established using automatic exchanges of keys.
+   * `ipsec_rsasigkey(8)` man page – Describes the tool used to generate RSA signature keys.
+   * `/usr/share/doc/libreswan-version/`

# #### 4.6.10.2. Online Documentation

+   * https://libreswan.org
+       The website of the upstream project.
+   * https://libreswan.org/wiki
+       The Libreswan Project Wiki.
+   * https://libreswan.org/man/
+       All Libreswan man pages.