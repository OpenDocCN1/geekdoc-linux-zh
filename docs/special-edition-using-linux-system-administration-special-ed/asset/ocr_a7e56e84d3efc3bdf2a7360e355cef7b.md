# EDIT THE FILE `/etc/ypservers`

Once the contents of the ypservers NIS database is saved in text form in the file `/etc/ypservers`, you need to edit the file. The file typically has the following format:

```
foo foo
YP_MASTER_NAME linux
YP_LAST_MODIFIED 942365535
linux linux
```

This file contains entries for two NIS servers (foo and linux) and indicates that linux is the master NIS server for the domain.

To add the new master server to the file, delete the first two lines containing `YP_MASTER_NAME` and `YP_LAST_MODIFIED`, and append a line at the end of the file with the server’s hostname repeated twice and separated by a space:

```
newhostname newhostname
```

# REGENERATE THE `ypservers` DATABASE

Once the new master server’s hostname is in the file `/etc/ypservers`, you need to regenerate the ypservers NIS map from this file. This is done by passing the contents of the text file through the makedbm program that generates an NIS map file.

This requires the following two steps:

+   1. Change your working directory to the directory containing the NIS maps for your domain with the following command:
+      ```
+      # cd /var/yp/<domainname>
+      ```
+   2. Use cat to display the contents of `/etc/ypservers` to the standard output and pipe this through makedbm to create the resulting NIS map:
+      ```
+      # cat /etc/ypservers | /usr/lib/yp/makedbm - ypservers
+      ```

# PUSH THE NEW DATABASE TO THE SLAVE SERVERS

Using the ypush command you can push the ypservers map to all slave servers in the domain:

```
# ypush ypservers
```

# COPYING THE `/etc` CONFIGURATION FILES

Several configuration files in `/etc` on the master NIS server are used to generate NIS maps:

+   - `/etc/passwd`: user database
+   - `/etc/group`: groups database
+   - `/etc/hosts`: host to IP address table
+   - `/etc/networks`: network addresses
+   - `/etc/services`: network port numbers and service names