| Service | Description |
| :--- | :--- |
| files | Checks corresponding `/etc` file for the configuration (for example, `/etc/hosts` for hosts); this service is valid for all files |
| db | Checks corresponding `/var/db` databases for the configuration; valid for all files except `netgroup` |
| compat | Valid only for `passwd`, `group`, and `shadow` files |
| dns | Checks the DNS service; valid only for `hosts` file |
| nis | Checks the NIS service; valid for all files |
| nisplus | NIS version 3 |
| hesiod | Uses Hesiod for lookup |

TABLE 35-9    NSS Configuration Services

files, db, dns, and compat (see Table 35-9). Not all are valid for each configuration file. For example, the dns service is valid only for the `hosts` file, whereas nis is valid for all files. The following example will first check the local `/etc/password` file and then NIS.

```
passwd:    files nisplus
```

An action item specifies the action to take for a specific service. An action item is placed within brackets after a service. A configuration specification can list several services, each with its own action item. In the following example, the entry for the network file has a configuration specification that says to check the NIS service and, if not found, to check the `/etc/protocols` file:

```
protocols: nisplus [NOTFOUND=return] files
```

An action item consists of a status and an action. The status holds a possible result of a service lookup, and the action is the action to take if the status is true. Currently, the possible status values are SUCCESS, NOTFOUND, UNAVAIL, and TRYAGAIN (service temporarily unavailable). The possible actions are return and continue: return stops the lookup process for the configuration file, whereas continue continues on to the next listed service. In the preceding example, if the record is not found in NIS, the lookup process ends.

Shown here is a copy of the `/etc/nsswitch.conf` file, which lists commonly used entries. Comments and commented-out entries begin with a # sign:

```
/etc/nsswitch.conf
#
# /etc/nsswitch.conf
#
# An example Name Service Switch config file.

passwd:             db files nisplus nis
shadow:             db files nisplus nis
group:             db files nisplus nis
hosts:             files nisplus dns
```