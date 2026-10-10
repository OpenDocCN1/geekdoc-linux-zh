# # Setting Up a File Server

server — The security option that, from the client’s point of view, is the same as **user** security. In that the client still has to provide a valid username/password combination to use the Samba server at all. The difference is on the **server** side. With **server** security, the username/password is sent to another SMB server for validation. If this fails, Samba will try to validate the client using **user** security.

domain — This security option also, from the client’s point of view, looks the same as **user** security. This setting is used only if the Samba server has been added to a Windows NT domain (using the net join command). When a client tries to connect to the Samba server in this mode, its username and password are sent to a Windows NT Primary or Backup Domain controller. This is accomplished the same way that a Windows NT server would perform validation. Valid Linux user accounts must still be set up.

ads — This security option causes Samba to act as a domain member in an ADS realm. Kerberos must be installed on the Samba machine to use this option. Samba must also join the ADS realm (see the net utility).

+   - **auth methods** — Sets the authentication method used by the Samba server (smbd). Leave the default in most cases. Authentication methods you can choose include anonymous access (guest), relay authentication through winbind (winbind|nbdm), pre-winning NT authentication (ntdomain), local lookups based on netbios or domain name (sam), or remote DC authentication of trusted users (trustdomain).

+   - **encrypt passwords** — Controls whether encrypted passwords can be negotiated with the client. This is on (yes) by default. For domain security, this value must be yes. Later versions of Windows NT (4.0 SP3 or later) and Windows 98 and Windows 2000 expect encrypted passwords to be on.

+   - **client channel** — Chooses if the client is to require the use of netlogin channel (yes), offer channel but not enforce it (auto), or not even offer channel (no).

+   - **server channel** — Chooses if the server requires clients to use netlogin channel (yes), offer channel but not enforce it (auto), or not even offer channel (no). If you set this to no, you must apply the Windows XP WinXP_Sign0rSeal.reg patch available from the Samba project.

+   - **passdb backend** — Chooses the method of storing the backend database used to store passwords. By default, a TDB-based method is used (tdbsam) with a file named passdb.tdb. Other options include smbspassd (Samba password storage style) and ldapsam (LDAP-based storage style).

> > **NOTE** Using smbspassd backend is deprecated, but it is currently still included for backward compatibility.

+   - **guest account** — Specifies the username for the guest account. When a service is specified as “Guest OK,” the username entered here will be used to access that service. The account is usually the nobody username.