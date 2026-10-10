![](bbox=[0.15, 0.11, 0.24, 0.16])

OpenSSH 4.0 and later support hashing of hostnames in the known hosts file. When this feature is enabled, the hostname is *hashed* (that is, encrypted using a one-way encryption algorithm) and stored in hashed form. The idea is that you'll still be able to authenticate SSH servers to which you connect, because a hash of the type hostname will match a hash of the stored hostname; but if an intruder steals your known hosts file, the intruder will be unable to determine the identities of the computers to which you've been connecting.

# Controlling SSH Access

You can limit who may access an SSH server in various ways. The most obvious and basic method is via password authentication. The usual SSH authentication method is to employ a username and password, much as Telnet does. (The ssh client program sends the username automatically or as part of the command line, so you won't see a username prompt when logging in via ssh.)

Beyond password authentication, SSH supports several other types of limitations:

**TCP Wrappers** If you run SSH from a super server, or if the server was compiled with TCP Wrappers support, you can use the `/etc/hosts.allow` and `/etc/hosts.deny` files to limit access by IP address. Note that if you launch SSH via a SysV startup script, this approach works only if the server was compiled to support it. This support may or may not be present in your distribution's standard SSH package.

**Firewalls** As with all servers, you can restrict access by using a firewall. SSH uses TCP port 22. Technically, this isn't an SSH feature, but it's certainly useful for protecting an SSH server.

**/etc/noLogin** If this file is present, SSH honors it. As described earlier, this file's presence means that only root may log in. Ordinarily, the file's contents are displayed as an error message; however, OpenSSH doesn't do this.

# Copying Files via SSH

Most users employ the ssh client program, which provides remote login access—type **ssh othersystem** to log into othersystem using the same username you're using on the client system; or add a username, as in **ssh user@othersystem**, to log in using another username.

SSH includes a file-copying command, too: *scp*. This command works much like the cp command for copying files locally; however, you must specify the target computer, and optionally the username, just before the target filename. For instance, to copy the file masterpiece.c to the lisa account on leonardo.example.com, you would type

```
$ scp masterpiece.c lisa@leonardo.example.com:
```

The colon (`:`) that terminates this command is extremely important; if you omit it, you'll find that scp works like cp, and you'll end up with a file called `lisa@leonardo`