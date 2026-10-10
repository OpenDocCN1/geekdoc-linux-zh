# ### **pap-secrets and chap-secrets**

The `/etc/ppp/chap-secrets` and `/etc/ppp/pap-secrets` files contain the CHAP and PAP authentication information, respectively. The files follow the basic format of `username hostname password` where `username` is your ISP login name, `hostname` is the name of the host that this entry will also authenticate, and `password` is (of course) your Internet password. You can replace the hostname entry with a wildcard (`*`), which tells `pppd` that this entry can authenticate to any host. Using a wildcard is a good idea for configuring your Internet account, because if you dial in to your ISP, you are already assured that the host you are contacting is who it claims to be. A sample entry for either of these files might look like this:

```
```
foo * bar
```
```

Here, `foo` is the username, `*` means that this entry is good for any host, and `bar` is the password.

You can use other options in the `chap-secrets` and `pap-secrets` files, but they are generally used only if you are providing dial-in PPP service. If you are interested, further information on how to use these files can be found in the "Authentication" section of the `man pppd` page.

> **CAUTION**
> The `/etc/ppp/chap-secrets` and `/etc/ppp/pap-secrets` files should be readable only by root. Change the permissions accordingly; otherwise, anyone who has shell access to your system can get your Internet password from these files.

# ### Dial-On-Demand and Persistent Connections

As the name suggests, *dial-on-demand* means that `pppd` automatically dials out whenever it detects outgoing traffic that needs to be sent. A *persistent connection*, on the other hand, is always "up" and redials the connection immediately if `pppd` detects a disconnect. The following subsections describe how to enable both kinds of connections in kernel PPP.

# #### Dial-On-Demand

Dial-on-demand causes `pppd` to establish a dial-up connection any time it detects outgoing network traffic when the connection is not already up. The relevant statements in `/etc/ppp/` options are as follows:

+   *   `demand`—This statement turns on dial-on-demand.

+   *   `idle` *n*—Here, *n* is a number representing seconds. This option causes `pppd` to automatically disconnect after *n* seconds of being *idle*, meaning that no traffic has been sent or received over the PPP link during that time.