# mod_auth_anon

The `mod_auth_anon` module enables anonymous access to authenticated areas. If you are familiar with anonymous FTP servers, this is very similar to such a setup. All users can use a user ID called "anonymous" and their e-mail addresses as the password to get access. The e-mail address entered is stored in log files and can be used to perform user tracking or to create a mailing list of prospective clients.

You have to enable this module by using the `-enable-auth-anon` option with the `configure` script in the source distribution, and by compiling and installing Apache.

# Anonymous

By using the `Anonymous` directive you can specify one or more usernames that can be used to access the area. It is a good idea to keep the username "anonymous" in your chosen list, because it is widely associated with anonymous access. If the username you choose has a space character in it, make sure that the username is surrounded by quotation marks.

**Syntax:** `Anonymous user user ...`

**Context:** Directory, per-directory access control file (`.htaccess`)

**Override:** `AuthConfig`

For example, the following directive allows users to enter Unregistered User or anonymous as the username to enter an anonymous area.

```
Anonymous "Unregistered User" anonymous
```

![](bbox=[0.122, 0.588, 0.201, 0.656])

> The username strings are not case sensitive.

# Anonymous_Authoritative

When set to `on`, the anonymous authentication becomes the authoritative authentication scheme for a directory. In other words, if you have multiple authentication requirements for a directory and it also has this directive set, then the other methods will be ignored.

**Syntax:** `Anonymous_Authoritative On | Off`

**Default setting:** `Anonymous_Authoritative Off`

**Context:** Directory, per-directory access control file (`.htaccess`)

**Override:** `AuthConfig`