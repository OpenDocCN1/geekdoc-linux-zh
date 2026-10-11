![](bbox=[0.06, 0.1, 0.2, 0.2])

# NOTE

> From the client's point of view **security = server** is the same as **security = user**. It only affects how the server deals with the authentication, it does not in any way affect what the client sees.

Note that the name of the resource being requested is *not* sent to the server until after the server has successfully authenticated the client. This is why guest shares don't work in user level security without allowing the server to automatically map unknown users into the *guest account*. See the *map to guest* parameter for details on doing this.

See also the section the section called “8220:NOTE ABOUT USERNAME/PASSWORD VALIDATION”.

See also the *password server* parameter and the *encrypted passwords* parameter.

```
SECURITY = ADS
```

In this mode, Samba will act as a domain member in an ADS realm. To operate in this mode, the machine running Samba will need to have Kerberos installed and configured and Samba will need to be joined to the ADS realm using the net utility.

Note that this mode does NOT make Samba operate as a Active Directory Domain Controller.

Read the chapter about Domain Membership in the HOWTO for details.

# **server schannel (G)**  Default: *server schannel = autoyes*

Example: *server schannel = yes*

This controls whether the server offers or even demands the use of the netlogon schannel. *server schannel = no* does not offer the schannel, *server schannel = auto* offers the schannel but does not enforce it, and *server schannel = yes* denies access if the client is not able to speak netlogon schannel. This is only the case for Windows NT4 before SP4.

Please note that with this set to *no* you will have to apply the WindowsXP *WinXP.Sgn0rSeal.reg* registry patch found in the docs/registry subdirectory of the Samba distribution tarball.

# **server signing (G)**  Default: *server signing = Disabled*

This controls whether the server offers or requires the client it talks to to use SMB signing. Possible values are *auto, mandatory* and *disabled*.