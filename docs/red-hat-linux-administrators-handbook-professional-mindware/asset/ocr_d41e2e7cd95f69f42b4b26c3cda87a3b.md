The deny offset for new connections is ten minutes, by default, but you can change that with the `-l` option. Also note that you can supply a more customized warning message than the default `System shutdown at %s` by using one or more of the magic cookies shown in Table 10-3.

# Table 10-3 Magic Cookies for ftpshut Warning Message

| Magic Cookie | Replacement Text |
| :--- | :--- |
| `%s` | The time the system is going to shut down |
| `%r` | The time new connections will be denied |
| `%d` | The time current connections will be disconnected |

In addition to these cookies, you can use all the cookies previously shown in Table 10-2. To create such a message, run the `ftpshut` command as follows:

```
ftpshut -d NN -l MM HHMM "Shutdown at %s. Be done by %d."
```

Don't forget to replace *MM*, *HHMM*, and so on with appropriate values. When you are ready to restart the FTP service, you have to remove the `/etc/shmssg` file.

# *virtual*

**Syntax:** `virtual address root[\ banner\ logfile path`

**Default:** none

Use this keyword if you have multiple IP addresses for your Linux system and want to offer virtual FTP services. See the section “Creating virtual FTP sites,” later in the chapter, for details.

# **/etc/ftpconversions**

The `ftpconversions` file stores the FTP server's conversion database. The default configuration for this file is sufficient for almost all installations. If you need more information, see the man page for `ftpconversions`.

# **/etc/ftpgroups**

The file `/etc/ftpgroups` is important only if you allow the nonstandard SITTE commands. The Red Hat-shipped `wu-ftp` package comes with the