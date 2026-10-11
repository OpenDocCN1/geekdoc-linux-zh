All Kerberos systems need the correct software. If Kerberos is not installed on your system, you need to locate and download three packages before you can begin the configuration:

+   - `krb5-libs-1.2.1-8`: the libraries
+   - `krb5-workstation-1.2.1-8`: the workstation binaries
+   - `krb5-server-1.2.1-8`: the server binaries

These packages are readily available in RPM format from your favorite repository. Note that you must install `krb5-workstation-1.2.1-8.i386.rpm` before `krb5-server-1.2.1-8.i386.rpm` because it's one of its dependencies. Execute the following commands in this order to install these three packages:

```
```
[ramon]$ sudo rpm -i krb5-libs-1.2.1-8
[ramon]$ sudo rpm -i krb5-workstation-1.2.1-8.i386.rpm
[ramon]$ sudo rpm -i krb5-server-1.2.1-8.i386.rpm
```
```

Begin the Kerberos configuration by creating a primary KDC. First, check out the `/etc/krb5.conf` file. This is the general Kerberos configuration file, which is divided into several sections, or stanzas. Each of these section starts with a heading, followed by a number of variable assignments:

```
```
[stanza heading]
    variable1 = value
    variable2 = value
... 
```
```

The sample `/etc/krb5.conf` file supplied with the server package is a good starting point for your configuration. Pay special attention to the `[logging]` and the `[realms]` sections. The `[logging]` section instructs the KDC and the Kerberos administration server to send log events to a specific file or facility. The variables defined in the `[logging]` section are as follows:

+   - `admin_server` specifies a target file or device for the administrative server to perform its logging.
+   - `kdc` specifies a target file or device to which the KDC server should log its events.
+   - `default` specifies how to perform logging in the absence of an entry for `admin_server` or `kdc`.

The values to be used for these variables can be as follows:

+   - `FILE=filename` to specify a regular Linux file.
+   - `STDERR` to specify the standard error log.
+   - `CONSOLE` to specify the Linux console.