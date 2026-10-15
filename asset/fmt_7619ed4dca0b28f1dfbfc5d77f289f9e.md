
## Section #5: Special Device Flags

This section indicates how Mars should handle routing. Set this section to `0x0` unless you're testing your configuration.

## Recommended Section #6: Version Spoofing

Use this section to lie to the clients and tell them that you are running a certain version of NetWare. Use existing NetWare version numbers or some clients will not believe you! A list of the correct values is found in the configuration file that comes with SuSE Linux. The following configuration tells the clients that you are running NetWare version 3.11:

```
6 1 0x0
```

## Required Section #7: Password Handling

This section describes the password encryption method that Mars should use. The default and recommended value is `0`.

## Required Section #12: Supervisor Login

The format of this section is as follows:

```
12 NW_LOGIN LINUX_LOGIN [PASSWORD]
```

In this format, `NW_LOGIN` is the NetWare server login name and `LINUX_LOGIN` is the Linux NetWare administrator's username. `[PASSWORD]` is the password you want to set to the NetWare server.

This section is used only once. Use this section to set up your root NetWare account and start the server. After the server has started, remove the password of this section.

## Recommended Section #13: User Logins

For users to have files, you must designate those users as normal SuSE Linux users. If you don't want those users to use their accounts, but do want them to use the Mars server, you can do so by making an account for each of them as described in Chapter 4, “Managing Users and Groups,” and then disabling the account. The syntax for users is as follows:

```
13  NW_LOGIN  [LINUX_LOGIN]  [PASSWORD]  [FLAGS]
```

The only flag currently available is `0x1`, which disables the user's ability to change his password. Here is an example of using this section:

```
13  JOE  joe  0x1  #joe has no password...
```

## Recommended Section #21: Print Queues

This section should contain all the printers you want to make available to the clients. For more information regarding printing on SuSE Linux, refer to Chapter 11. The format for this section is as follows:

```
21  QUEUE_NAME  [QUEUE_DIR]  [PRINT_COMMAND]
```

In the previous line, `QUEUE_NAME` is the name the clients will see as the printer name, `QUEUE_DIR` is the printer spooling directory, and `PRINT_COMMAND` is the command that should be used with this printer. Use the minus sign (`-`) to replace a default spooling directory. The following is an example of sharing a printer:

```
21  HPDJ610C  .  lpr
```

The other sections of the file are intended for tweaking. You can modify their values to better suit your network or improve performance. In most cases, the default values specified in the file will provide the best results.

## Troubleshooting NetWare Networks

### `ipx_configure` doesn't seem to work. What's the problem?

You probably have Microsoft Windows 95/98 running IPX on the network. You should use the `ipx_interface` command instead of `ipx_configure` in this case. For example, use the following:

```
ipx_interface add -p <device> <frame>
```
