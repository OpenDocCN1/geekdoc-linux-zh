
## 5.15.4.6. Using the Rich Rule Log Command Example 6

Whitelist a source address to allow all connections from this source.

```
rule family="ipv4" source address="192.168.2.2" accept
```

See the `firewalld.richlanguage(5)` man page for more examples.

## 5.16. CONFIGURING FIREWALL LOCKDOWN

Local applications or services are able to change the firewall configuration if they are running as **root** (for example, `libvirt`). With this feature, the administrator can lock the firewall configuration so that either no applications or only applications that are added to the lockdown whitelist are able to request firewall changes. The lockdown settings default to disabled. If enabled, the user can be sure that there are no unwanted configuration changes made to the firewall by local applications or services.

### 5.16.1. Configuring Lockdown with the Command-Line Client

To query whether lockdown is enabled, use the following command as **root**:

```
~]# firewall-cmd --query-lockdown
```

The command prints **yes** with exit status `0` if lockdown is enabled. It prints **no** with exit status `1` otherwise.

To enable lockdown, enter the following command as **root**:

```
~]# firewall-cmd --lockdown-on
```

To disable lockdown, use the following command as **root**:

```
~]# firewall-cmd --lockdown-off
```

### 5.16.2. Configuring Lockdown Whitelist Options with the Command-Line Client

The lockdown whitelist can contain commands, security contexts, users and user IDs. If a command entry on the whitelist ends with an asterisk `"*"`, then all command lines starting with that command will match. If the `"*"` is not there then the absolute command including arguments must match.

The context is the security (SELinux) context of a running application or service. To get the context of a running application use the following command:

```
~]$ ps -e --context
```

That command returns all running applications. Pipe the output through the `grep` tool to get the application of interest. For example:

```
~]$ ps -e --context | grep example_program
```

To list all command lines that are on the whitelist, enter the following command as **root**:

```
~]# firewall-cmd --list-lockdown-whitelist-commands
```

To add a command *command* to the whitelist, enter the following command as **root**:

```
~]# firewall-cmd --add-lockdown-whitelist-command='/usr/bin/python -Es /usr/bin/command'
```

To remove a command *command* from the whitelist, enter the following command as **root**:

```
~]# firewall-cmd --remove-lockdown-whitelist-command='/usr/bin/python -Es /usr/bin/command'
```

To query whether the command *command* is on the whitelist, enter the following command as **root**:

```
~]# firewall-cmd --query-lockdown-whitelist-command='/usr/bin/python -Es /usr/bin/command'
```

The command prints **yes** with exit status **0** if true. It prints **no** with exit status **1** otherwise.

To list all security contexts that are on the whitelist, enter the following command as **root**:

```
~]# firewall-cmd --list-lockdown-whitelist-contexts
```

To add a context *context* to the whitelist, enter the following command as **root**:

```
~]# firewall-cmd --add-lockdown-whitelist-context=context
```

To remove a context *context* from the whitelist, enter the following command as **root**:

```
~]# firewall-cmd --remove-lockdown-whitelist-context=context
```

To query whether the context *context* is on the whitelist, enter the following command as **root**:

```
~]# firewall-cmd --query-lockdown-whitelist-context=context
```

Prints **yes** with exit status **0**, if true, prints **no** with exit status **1** otherwise.

To list all user IDs that are on the whitelist, enter the following command as **root**:

```
~]# firewall-cmd --list-lockdown-whitelist-uids
```

To add a user ID *uid* to the whitelist, enter the following command as **root**:

```
~]# firewall-cmd --add-lockdown-whitelist-uid=uid
```

To remove a user ID *uid* from the whitelist, enter the following command as **root**:

```
~]# firewall-cmd --remove-lockdown-whitelist-uid=uid
```

To query whether the user ID *uid* is on the whitelist, enter the following command:

```
~]$ firewall-cmd --query-lockdown-whitelist-uid=uid
```

Prints **yes** with exit status **0**, if true, prints **no** with exit status **1** otherwise.

To list all user names that are on the whitelist, enter the following command as **root**:

```
~]# firewall-cmd --list-lockdown-whitelist-users
```

To add a user name *user* to the whitelist, enter the following command as **root**:

```
~]# firewall-cmd --add-lockdown-whitelist-user=user
```

To remove a user name *user* from the whitelist, enter the following command as **root**:

```
~]# firewall-cmd --remove-lockdown-whitelist-user=user
```

To query whether the user name *user* is on the whitelist, enter the following command:

```
~]$ firewall-cmd --query-lockdown-whitelist-user=user
```

Prints **yes** with exit status **0**, if true, prints **no** with exit status **1** otherwise.

### 5.16.3. Configuring Lockdown Whitelist Options with Configuration Files

The default whitelist configuration file contains the **NetworkManager** context and the default context of **libvirt**. The user ID 0 is also on the list.

```xml
<?xml version="1.0" encoding="utf-8"?>
<whitelist>
    <selinux context="system_u:system_r:NetworkManager_t:s0"/>
    <selinux context="system_u:system_r:virt_t:s0-s0:c0.c1023"/>
    <user id="0"/>
</whitelist>
```

Following is an example whitelist configuration file enabling all commands for the **firewall-cmd** utility, for a user called *user* whose user ID is **815**:

```xml
<?xml version="1.0" encoding="utf-8"?>
<whitelist>
    <command name="/usr/bin/python -Es /bin/firewall-cmd*"/>
    <selinux context="system_u:system_r:NetworkManager_t:s0"/>
    <user id="815"/>
    <user name="user"/>
</whitelist>
```

This example shows both **user id** and **user name**, but only one option is required. Python is the interpreter and is prepended to the command line. You can also use a specific command, for example:

```
/usr/bin/python /bin/firewall-cmd --lockdown-on
```

In that example, only the **--lockdown-on** command is allowed.

![](img/c62903c5bdbf5bcc6bc0ae8373bee5f4_181_0.png)

**NOTE**

In Red Hat Enterprise Linux 7, all utilities are placed in the `/usr/bin/` directory and the `/bin/` directory is sym-linked to the `/usr/bin/` directory. In other words, although the path for `firewall-cmd` when run as `root` might resolve to `/bin/firewall-cmd`, `/usr/bin/firewall-cmd` can now be used. All new scripts should use the new location. But be aware that if scripts that run as `root` have been written to use the `/bin/firewall-cmd` path, then that command path must be whitelisted in addition to the `/usr/bin/firewall-cmd` path traditionally used only for non-`root` users.

The `(*)` at the end of the name attribute of a command means that all commands that start with this string will match. If the `(*)` is not there then the absolute command including arguments must match.

## 5.17. CONFIGURING LOGGING FOR DENIED PACKETS

With the `LogDenied` option in the `firewalld`, it is possible to add a simple logging mechanism for denied packets. These are the packets that are rejected or dropped. To change the setting of the logging, edit the `/etc/firewalld/firewalld.conf` file or use the command-line or GUI configuration tool.

If `LogDenied` is enabled, logging rules are added right before the reject and drop rules in the INPUT, FORWARD and OUTPUT chains for the default rules and also the final reject and drop rules in zones. The possible values for this setting are: `all`, `unicast`, `broadcast`, `multicast`, and `off`. The default setting is `off`. With the `unicast`, `broadcast`, and `multicast` setting, the `pkttype` match is used to match the link-layer packet type. With `all`, all packets are logged.

To list the actual `LogDenied` setting with `firewall-cmd`, use the following command as `root`:

```
~]# firewall-cmd --get-log-denied
off
```

To change the `LogDenied` setting, use the following command as `root`:

```
~]# firewall-cmd --set-log-denied=all
success
```

To change the `LogDenied` setting with the `firewalld` GUI configuration tool, start `firewall-config`, click the `Options` menu and select `Change Log Denied`. The `LogDenied` window appears. Select the new `LogDenied` setting from the menu and click `Ok`.

## 5.18. ADDITIONAL RESOURCES

The following sources of information provide additional resources regarding `firewalld`.

### 5.18.1. Installed Documentation

- `firewalld(1)` man page – Describes command options for `firewalld`.
- `firewalld.conf(5)` man page – Contains information to configure `firewalld`.
- `firewall-cmd(1)` man page – Describes command options for the `firewalld` command-line client.
