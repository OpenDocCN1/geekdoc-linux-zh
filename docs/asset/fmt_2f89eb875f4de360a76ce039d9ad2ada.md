
# Section 7: password handling of DOS-clients (required)

```
# ==============================
# Section 7: password handling of DOS-clients (required)
#
# When changing your "mars_nwe"-password from a DOS-client, this client
# (think of "LOGIN.EXE", "SYSCON.EXE" or "SETPASS.EXE") can encrypt your
# password before sending it to the "mars_nwe"-server (this improves
# security a little bit).
# In this section you can enforce encryption of user-passwords or allow
# not-encrypted sending of passwords over the net.
#
# On the Linux-side, passwords will only be stored in encrypted format.
#
#
# ---------------------------------------------------------------
# Syntax:
# 7 FLAG
#
# FLAG:
# 0 enforce encryption of _all_ passwords by the DOS-client
# (default)
# 1 as "0", but allow the non-encrypted version of the
# change password-routine.
# 7 allow all non-encrypted stuff but no empty nwe passwords.
# 8 allow all non-encrypted stuff and also allow empty
# nwe-passwords.
# 9 use all non-encrypted calls + "get crypt" key will always fail
# so the login program will use the old unencrypted calls.
# this will "not" work with all clients !! (OS/2 client)
# ---------------------------------------------------------------
7 0
```

再次，这里在 Red Hat 提供的示例（见列表 18.7）与 IPX-HOWTO 之间存在差异。HOWTO 建议此参数的值为 `1`，而示例文件指定为零。在我进行的所有实验中，我将其设置为零，并且它按预期工作。

下一个感兴趣的章节是第 10 节，见列表 18.8。第 8 节和第 9 节目前未使用。在第 10 节和第 11 节中，您指定一个非特权用户和组，DOS 客户端在登录服务器之前会使用它们。

## 列表 18.8 `/etc/nwserv.conf` 文件的第 10 节—非特权用户的用户和组 ID

```
# Section 10: UID and GID with minimal rights
# =================================================================
#
# When loading the netware-drivers in the "autoexec.bat" of your
# DOS-client, you automatically "attach" to a netware-server.
# As a result, a new drive-letter is accessible under DOS, usually
# containing the programs "login.exe" and "slist.exe".
# Because you haven't logged in, nothing else of the netware-server
# will be visible to you. All actions requested from the DOS-client
# will be done with the following UID and GID on the Linux-side in this
# case.
#
# To achieve some level of security, the user/group associated with
# the UID and GID should only have _read_ rights on the files visible,
# _nothing_ else.
#
# .......................................................................
#
# Syntax:
#       10          GID
#       11          UID
#
# GID  numeric number of the group
# UID  numeric number of the user
#
# .......................................................................
#
# Example:
#       10          65534
#       11          65534
#
        10          99
        11          99
```

用户编号 `99` 和组编号 `99` 对应 `nobody` 用户和 `nobody` 组，出于安全考虑，这是最佳设置。此用户账户应仅具有查看 `LOGIN` 目录中文件的权限。

下一节，见列表 18.9，定义了服务器的超级用户登录。此条目是必需的，并将传统上称为 `SUPERVISOR` 的 NetWare 超级用户账户与 Linux 系统上的登录账户关联起来。

## 列表 18.9 `/etc/nwserv.conf` 文件的第 12 节—超级用户登录
