# NOTE

> Unless compiled with the `--enable-override` option, neither `opiekey` nor `opiepasswd` will successfully execute over the network, even if you use the `-f` flag. This may be inconvenient, but it provides substantial additional security by disallowing secret passphrases to be submitted over the network. Consider this feature carefully before you compile with the `--enable-override` option. And don't expect your users not to know about the `-f` flag—they can read man pages, too!

Recall that both su and ftp are replaced with OPiE versions when OPiE is installed. Thus, those utilities will behave similarly with respect to requiring OTP when invoked.

The biggest problem with using OPiE is that it imposes OTP everywhere, including at the console. This may be desirable, but it also means that, in order to log in at the console, either you will need a printed list of one-time passwords or you will need to have access to another system that can run opiekey. One way to work around this issue is to utilize the /etc/opieaccess file.

**Using /etc/opieaccess** This is a very simple access control list that contains rules using the syntax displayed in Example 6-24. In this file, the keyword permit or deny is followed by one or more spaces and then the network/netmask entry. Both the network and netmask entries must be in dot decimal notation. The same goes for the host entry, which uses a netmask value of 255.255.255.255 to inform OPiE that it is a rule for a host and not for a network.

# Example 6-24  /etc/opieaccess Syntax

```
```
permit host/netmask
permit  host/255.255.255.255
deny  network/netmask
deny  host/255.255.255.255
```
```

The deny keyword indicates that any host coming from the network indicated must respond to an OPiE challenge. The same is true for a single host if the target of deny is a host-only entry.

The permit keyword means that the network/netmask entry to its right will not be required to supply an OPiE OTP; instead the user will be given the option of supplying the OTP password or the Linux password. Consider Example 6-25, which reflects a sample /etc/opieaccess file on topcat. In this case, the users logging in from host 172.17.31.104 (which is topcat itself) will be allowed to supply either an OPiE OTP or a Linux password. The same is true for any user from any host on the subnetwork 172.17.1.0 except for the host 172.17.1.5. All other access will be required to use OPiE OTP.

# Example 6-25  Sample /etc/opieaccess File

```
```
permit  172.17.31.104/255.255.255.255
permit  172.17.1.0/255.255.255.0
deny    172.17.1.5/255.255.255.255
```
```