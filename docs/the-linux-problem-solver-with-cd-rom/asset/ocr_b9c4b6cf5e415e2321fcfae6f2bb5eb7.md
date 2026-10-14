username * password

This forces pppd to accept any remote host and IP address. To tell pppd what user name to use, put

```
name username
```

in your ISP's options file (that is, a file in /etc/ppp/peers), or in /etc/ppp/options if you don't plan on using more than one ISP.

# Multiple ISPs

If you have more than one ISP with the same user name, you can distinguish between them in /etc/ppp/pap-secrets by changing the asterisk (*) to a name, then forcing the remote name to name in that ISP's options file (in /etc/ppp/peers) with

```
remotename name
```

Doing so allows you to add more lines to /etc/ppp/pap-secrets for additional ISPs.

> NOTE When adding ISPs, make the appropriate changes to the files in /etc/ppp/peers.

# PROBLEM 9

Symptom: pppd successfully begins negotiation, but authentication times out or fails (even though the server accepted your password).

Problem: Using the require-pap option.

Fix: When using PAP as a normal dial-up user, don't put require-pap in your options files, or your pppd will ask the dial-up server to prove its identity. Even if your dial-up tries to prove its identity, you most likely won't have an entry in your pap-secrets file to back it up.

> NOTE If you configured Red Hat 6 for PPP and PAP with linuxconf, you may notice that it never puts an asterisk in the /etc/ppp/pap-secrets file. linuxconf forces everything into the /etc/sysconfig/network-scripts/ifcfg-ppp* files by setting the variables DEVICE to the interface and PAPNAME to the user (they get passed to pppd as the options remotename and name).

# CHAP

CHAP (Challenge Handshake Authentication Protocol) is similar to PAP, but requires that both sides give user names and passwords. It is usually used for connecting to Windows NT servers.