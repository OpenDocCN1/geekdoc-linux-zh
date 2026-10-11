
Entries in the smbpasswd file follow this general format:

```
User:UID:LAN-Manager-password:NT-password:account-flags:update-time
```

Each of these fields has the following meaning:

- **User**: *User* is the textual username supplied by the client. This field must match a username in the local `/etc/passwd` file.
- **UID**: *UID* is the numeric user ID. This field must also match an /etc/passwd entry.
- **LAN-Manager-password**: *LAN-Manager-password* is the encrypted representation of the old-style (Windows 9x) password. The actual entry is computed by DES-encrypting a well-known character sequence using the repeated password (in all capitals) as the key.
- **NT-password**: *NT-password* is the encrypted representation of the new-style (Windows NT and 2000) password. This field results from the MD4 hashing of the password in Unicode format.
- **account-flags**: The *account-flags* field is a combination of the following four types of flags:
    - U: This flag indicates a standard user account.
    - D: This flag indicates a disabled account (no logins allowed).
    - N: This flag indicates an account with no password.
    - W: This flag indicates a workstation account, which is used to configure Samba as an NT PDC.
- **update-time**: The *update-time* field is the seconds since the epoch (1 January 1970) when the entry was last updated.

## Access Control

Whenever the Samba server receives an SMB request from a client, the server tells the client which authentication setting it should conform to. Samba supports four fundamental modes of authentication, reflected as the four options to the following smb.conf directive:

```
security = [share|user|server|domain]
```

Let’s take a closer look at each of these four access-control choices.

**share mode**

By setting up one or more passwords for general access to a file, directory, or printer, you can allow all your users access by providing the same password(s). This is generally not recommended, except for allowing access to guest shares, as well as giving general access to print servers.

Even though SMB clients are not required to provide a username for share mode resources, Samba still needs to operate within the Linux paradigm, which requires user ownership for all its resources. So Samba tries to come up with a good default username to use on the client’s behalf. Here are the options that Samba uses as username defaults (in decreasing order of precedence):

- If `smb.conf` includes the configuration lines `guest only = yes` and `guest account = guest,` then the username `guest` is always chosen.
- If the client includes a user with the request anyway, the username supplied is chosen.
- If the client has previously connected to the Samba server, the username that was supplied at that time is chosen.
- If none of the above, then the name of the requested service is chosen.
- If the name of the requested service is not available, the NetBIOS name of the requesting client is chosen.
- As a last resort, the user descriptions present in the `smb.conf` file under the `username= user1, user2,`... directive are chosen.

It’s important to note that if `smb.conf` includes the configuration lines `guest only = yes` and `guest account = guest,` then the username `guest` is always chosen. However, if `guest only = no,` and the password supplied by the client does not match one of the users included in the `username=` directive, access to the share is denied.

While all this seems overly elaborate, the point is simple: Samba must find a Linux username that can be authenticated with the password supplied by the requesting client. The easiest way to ensure this is to assign the same usernames for Windows clients and for interactive logins to the Linux server (`/etc/passwd` or `/etc/shadow`). This makes your users and shares easier to manage across both platforms.

For example, consider the following `smb.conf` configuration. The `[Sales]` stanza defines a resource to be shared, in this case, the `/homes/marketing` directory. This resource is writable and can be browsed using the standard Microsoft Network Neighborhood browsing facility. Note that the directive `security = share` is included in the `[global]` stanza, but you have qualified it with the `guest only = no` and `username = ramon, stacia` directives in the `[Sales]` stanza. This combination of directives allows `share` mode access to the `Sales` share, but only if the password supplied by the client matches the password for either `ramon` or `stacia`, or it matches the password for a user that has previously connected to the Samba server.

```
[global]
security = share
[Sales]
Comment = Sales Share
Path = /homes/marketing
writable = yes
browsable = no
guest_only = no
username = ramon, stacia
```

**user mode**

user mode goes a step beyond share mode by forcing each user to provide a unique username and password combination before granting access to a share. This is clearly recommended over share mode because it allows the administrator to grant or deny access to a share on a per-user basis, and eliminates the complex login used by share mode to assign a default user. user mode is the default authentication mode as of Samba 2.0.

> **NOTE** If the guest only = yes directive is present in smb.conf, the Linux username will be changed to the one specified by the guest account = directive, but only after the supplied password has been verified to belong to the supplied username.

For example, consider the following smb.conf configuration. The security = user directive is included in the [global] stanza, but it is qualified by the valid users = ramon, stacia directive in the [Marketing] stanza (where the sharing of the /homes/marketing directory is defined). This combination of directives allows only users ramon and stacia access to the Marketing share, only after they have supplied a valid username and password combination.

```
[global]
    security = user

[Marketing]
    Comment = Marketing Share
    Path = /homes/marketing
    writable = yes
    browsable = no
    valid users = ramon, stacia
```

**server mode**

When the server mode type of access control is specified, the supplied username and password combination is not checked locally, but instead, is sent to a remote SMB server for verification. The remote server then returns the outcome of the authentication request to the local server. If the remote server cannot authenticate the client, then the local server reverts to user mode access control. The remote server can be a Windows NT machine or another Samba server configured to run in user mode. The name of the remote server must be specified with the `password server =` directive in the `smb.conf` file.

The server mode of authentication is useful when you're operating several Samba servers but only want to have a single authentication point for the majority of your user population. You still have to have the users present in the local `/etc/passwd` file, but their accounts can (and should) be disabled.

As an example, consider the following `smb.conf` configuration. This server consults with SMB server `LINUX_SAMBA_1` for username/password authentication. If `LINUX_SAMBA_1` is unavailable, it next consults with SMB server `LINUX_SAMBA_2`. Note however, that if `LINUX_SAMBA_1` returns an authentication denial, the client is denied access before even consulting the next server on the list.

```
[global]
    security = server
    password server = LINUX_SAMBA_1 LINUX_SAMBA_2
```

**domain mode**

Domain mode is a special case of server mode, where the remote SMB server is an NT domain controller with which the local Samba server has previously established a trust relationship using the command

```
smbpasswd -j NT-Domain -r NT-Domain-Controller
```

In this command, `NT-Domain` is the name of the domain you wish to be part of and `NT-Domain-Controller` is the NetBIOS name of the primary domain controller (PDC) for the given domain. By establishing a trust relationship between the local Samba server and the remote Windows NT domain controller, you are allowing the local Samba server to validate the username/password supplied by a requesting client by passing it to a Windows NT domain controller. This is the same way a Windows NT server that is a member of a given domain passes user authentication requests on to a domain controller for approval. This is a useful access control option for integrating a few Samba servers into an existing NT domain network.

To use domain mode access control, simply include the appropriate directive in the `smb.conf` file. In the following example, the NT domain controllers `ENG_SAMBA_1` and `ENG_SAMBA_2` are used (in that order) to authenticate clients' requests:

```
[global]
    security = domain
    workgroup = ENGINEERING
    domain logins = yes
    password server = ENG_SAMBA_1 ENG_SAMBA_2
```
