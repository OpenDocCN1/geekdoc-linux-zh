The `resolv.conf` file lists IP addresses of name servers. The name server that appears first in the file is queried first. It is important to ensure all name servers listed in the `resolv.conf` file are functional. A non-functioning name server entry followed by a functioning name server entry will cause name lookups to work; however, it will introduce long delays in name lookups.

Check the contents of the `resolv.conf` file and make sure all information in it is up to date and accurate.

# ## OUTDATED `root.hints` FILE

The `root.hints` file contains the domain names and IP addresses of the root servers for each domain. Changes to the `root.hints` file are not automatically propagated to your name server. You must update this file manually. Check for updated root servers information at `rs.internic.net`. You can get the latest root server information from `rs.internic.net` by running the following command.

```
```sh
# dig @rs.internic.net . ns > root.hints.new
```
```

The output of the `dig` command is saved to the file `root.hints.new`. Compare the contents of this file with your current `root.hints` file and if it differs use the new `root.hints` file. It is possible to set up a cron job to automatically retrieve information about the root servers once a month, install the updated information, restart named, and notify the administrator of the update via email. A ready script that performs this function is listed in the Linux DNS HOWTO file, which is available on-line in the `/usr/doc/HOWTO` directory.