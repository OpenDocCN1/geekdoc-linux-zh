+   • This mode may open connections to the password server and keep them open for extended periods.
+   • Security on the Samba server breaks badly when the remote password server suddenly shuts down.
+   • With this mode there is NO security account in the domain that the password server belongs to for the Samba server.

In server security mode the Samba server reports to the client that it is in user-level security. The client then does a session setup as described earlier. The Samba server takes the *username/password* that the client sends and attempts to log into the *password server* by sending exactly the same *username/password* that it got from the client. If that server is in user-level security and accepts the password, then Samba accepts the client’s connection. This parameter allows the Samba server to use another SMB server as the *password server*.

You should also note that at the start of all this, when the server tells the client what security level it is in, it also tells the client if it supports encryption. If it does, it supplies the client with a random cryptkey. The client will then send all passwords in encrypted form. Samba supports this type of encryption by default.

The parameter *security* = *server* means that Samba reports to clients that it is running in *user mode* but *actually* passes off all authentication requests to another user mode server. This requires an additional parameter *password server* that points to the real authentication server. The real authentication server can be another Samba server, or it can be a Windows NT server, the latter being natively capable of encrypted password support.

> **NOTE**
> 
> When Samba is running in *server security mode*, it is essential that the parameter *password server* is set to the precise NetBIOS machine name of the target authentication server. Samba cannot determine this from NetBIOS name lookups because the choice of the target authentication server is arbitrary and cannot be determined from a domain name. In essence, a Samba server that is in *server security mode* is operating in what used to be known as workgroup mode.

# 3.3.5.1 Example Configuration

*Using MS Windows NT as an Authentication Server*

This method involves the additions of the following parameters in the *smb.conf* file:

```
```
encrypt passwords = Yes
security = server
password server = "NetBIOS_name_of_a_DC"
```
```