ownership for all its resources. So Samba tries to come up with a good default username to use on the client’s behalf. Here are the options that Samba uses as username defaults (in decreasing order of precedence):

+   - If `smb.conf` includes the configuration lines `guest only = yes` and `guest account = guest,` then the username `guest` is always chosen.
+   - If the client includes a user with the request anyway, the username supplied is chosen.
+   - If the client has previously connected to the Samba server, the username that was supplied at that time is chosen.
+   - If none of the above, then the name of the requested service is chosen.
+   - If the name of the requested service is not available, the NetBIOS name of the requesting client is chosen.
+   - As a last resort, the user descriptions present in the `smb.conf` file under the `username= user1, user2,`... directive are chosen.

It’s important to note that if `smb.conf` includes the configuration lines `guest only = yes` and `guest account = guest,` then the username `guest` is always chosen. However, if `guest only = no,` and the password supplied by the client does not match one of the users included in the `username=` directive, access to the share is denied.

While all this seems overly elaborate, the point is simple: Samba must find a Linux username that can be authenticated with the password supplied by the requesting client. The easiest way to ensure this is to assign the same usernames for Windows clients and for interactive logins to the Linux server (`/etc/passwd` or `/etc/shadow`). This makes your users and shares easier to manage across both platforms.

For example, consider the following `smb.conf` configuration. The `[Sales]` stanza defines a resource to be shared, in this case, the `/homes/marketing` directory. This resource is writable and can be browsed using the standard Microsoft Network Neighborhood browsing facility. Note that the directive `security = share` is included in the `[global]` stanza, but you have qualified it with the `guest only = no` and `username = ramon, stacia` directives in the `[Sales]` stanza. This combination of directives allows `share` mode access to the `Sales` share, but only if the password supplied by the client matches the password for either `ramon` or `stacia`, or it matches the password for a user that has previously connected to the Samba server.

```
```
[global]
security = share
[Sales]
Comment = Sales Share
```
```