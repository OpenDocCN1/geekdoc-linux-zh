Syntax: AuthGroupFile filename

Context: Directory, per-directory access control file

Override: AuthConfig

You can create this file using any text editor. The format of this file is as follows:

```
groupname: username username username ...
```

For example, the following command creates a group called startrek, which has four users: kirk, spock, picard, and data:

```
startrek: kirk spock picard data
```

The Caution icon in the AuthUserFile section also applies to this directive.

# AuthAuthoritative

If you are using more than one authentication scheme for the same directory, you can set this directive to Off so that when a user name/password pair fails with the first scheme, it is passed on to the next (lower) level.

Syntax: AuthAuthoritative On | Off

Default setting: AuthAuthoritative On

Context: Directory, per-directory access control file

Override: AuthConfig

For example, if you are using mod_auth_mysql and the standard mod_auth module to provide authentication services, and a user name/password pair fails for one of them, the next module is used to authenticate the user, if possible. When a user name/password pair fails all modules, the server reissues a 401 status header and sends the WWW-Authenticate response header for re-authentication. However, if a particular module successfully authenticates a user name/password pair, the lower-level modules never receive the user name/password pair.

I recommended that you leave the default because you should not design a trickle-down authentication scheme where a user may fail one and pass another.