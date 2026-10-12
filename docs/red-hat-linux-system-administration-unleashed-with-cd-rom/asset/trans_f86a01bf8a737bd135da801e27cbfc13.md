
## 列表 18.7 /etc/nwserv.conf 文件的第 7 节—DOS 客户端密码处理

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

再次，这里在 Red Hat 提供的示例（见列表 18.7）与 IPX-HOWTO 之间存在差异。HOWTO 建议此参数的值为 1，而示例文件指定为零。在我进行的所有实验中，我将其设置为零，并且它按预期工作。

下一个感兴趣的章节是第 10 节，见列表 18.8。第 8 节和第 9 节目前未使用。在第 10 节和第 11 节中，您指定一个非特权用户和组，DOS 客户端在登录服务器之前会使用它们。

## 列表 18.8 /etc/nwserv.conf 文件的第 10 节—非特权用户的用户和组 ID

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

用户编号 99 和组编号 99 对应 nobody 用户和 nobody 组，出于安全考虑，这是最佳设置。此用户账户应仅具有查看 LOGIN 目录中文件的权限。

下一节，见列表 18.9，定义了服务器的超级用户登录。此条目是必需的，并将传统上称为 SUPERVISOR 的 NetWare 超级用户账户与 Linux 系统上的登录账户关联起来。

## 列表 18.9 /etc/nwserv.conf 文件的第 12 节—超级用户登录

```
# ==============================================================
# Section 12: supervisor-login (required)
#
# The "supervisor" of a nw-server is much like "root" on the Linux-side.
#
# Specify a Linux-user that should be mapped to the supervisor of this
# mars_nwe.server.
# To improve security, don't use "root" for this purpose but create a
# seperate administrative account (under Linux) called "nw-adm" or similar.
#
# The nw-user defined in this section will have the mars_nwe internal UID
# "1" (remember even under Linux "root" must have the special UID "0"), so
# it is not possible to define a supervisor in section 13 (the users
# defined there will get random UIDs).
# You can define a user with name "SUPERVISOR" in section 13, but he
# won't really be the "local god" on the "mars_nwe" server.
# And of course you can define a supervisor with name "GOD" or "ROOT"
# in this section, which would only break the traditional naming-scheme
# of the netware-world.
#
#
# ---------------------------------------------------------------
# Syntax:
# 12      NW_LOGIN      LINUX_LOGIN      [PASSWORD]
#
# NW_LOGIN:      the login-name for the "mars_nwe" server (traditionally,
#                this is "SUPERVISOR")
# LINUX_LOGIN:   the account on the Linux-side associated with the NW_LOGIN
# PASSWORD:      the password for the NW_LOGIN. It must be clear-text but
#                will be encrypted and permanent stored in the
#                bindery-files, so it (the password or the whole section, at
#                your option) can be deleted after the first start of
#                "nwserv".
#
#
# Make sure this file is not world-readable as long
# as the password stands here.
#
#
# If you leave this field blank when starting "mars_nwe" the
# first time, the supervisor-login will be completely
# disabled. In other words: there is no way to supply the
# supervisor with no password ("null-password").
# ---------------------------------------------------------------
```

## 列表 18.9 继续

```
#
# Example:
# 12      SUPERVISOR    nw-adm    top-secret

12 SUPERVISOR adm *
```

关于第 12 节的设置有两个注意事项：您可以将 NetWare SUPERVISOR 账户映射到 Linux root 账户；但是，如果这样做，您必须在首次启动 nwserv 守护进程之前以明文形式暴露 root 密码。因此，不建议这样做。另一个注意事项是，Red Hat 附带的配置文件中的条目没有用处。您应在首次启动 mars_nwe 时定义一个密码，然后删除 nwserv.conf 文件中的条目或将其更改为星号，如图所示。

配置文件的第 13 节用于将 NetWare 用户账户与 Linux 系统上的账户映射。此文件部分见列表 18.10，且为可选。此部分的语法与第 12 节相同。

## 列表 18.10 /etc/nwserv.conf 文件的第 13 节—用户登录

```
# ===================================================
# Section 13: user-logins (optional)
#
# You can provide mappings from the regular login-names of your Linux-Box
# to "mars_nwe"-logins here.
# Every "mars_nwe"-user _must_ have a login-name on the Linux side (even
# if he can't log in into the account associated with the login-name,
# because you locked it with a "*") in order to 'own' files.
# If you specify a Linux-login that doesn't exist (one could think of a
# typo), the user will only have the minimal rights defined in
# sections 10/11.
#
# See section 12 for a description of the syntax.
#
# Unlike in section 12, you can define users with no password.
#
# Example:
# 13      MARTIN        martin
```

在第 13 节中，您可以允许将 NetWare 用户名映射到 Linux 名称，并且强烈建议这样做。这是因为我接下来要描述的自动映射选项无法使用 Linux 密码，如果启用自动映射，您将为所有用户使用一个通用密码。

如果您选择使用 NetWare 用户名到 Linux 用户名的自动映射，您需要使用配置文件中的第 15 节，见列表 18.11。

## 列表 18.11 /etc/nwserv.conf 文件的第 15 节—NetWare 用户到 Linux 用户的自动映射

```
# ===========================================================================
# Section 15: automatic mapping of logins (decision required)
#
# If you have a large number of accounts on your Linux-machine, you may
# want to map all Linux-logins automatically to "mars_nwe"-logins.
#
# At this stage this section is only a quick hack to make life a bit
# easier for the administrator.
#
# WARNING: as there is no algorithm to convert the encrypted
# "Linux-passwords" into the encrypted format used by the DOS-clients (and
# therefore "mars_nwe"), you have to supply a common password for all
# automatically mapped users. This is a big security concern and you
# should never make this common password public (and, of course you
# should choose a sufficient 'secure' (read: difficult) password).
# Type the common password to grant access to the users login and the
# command "setpass" instead of telling the password to the user.
#
# Only those Linux-logins will be handled automatically that don't have a
# "x" or "*" as their encrypted password.
#
#
# ===========================================================================
# Syntax:
# 15 FLAG DEFAULT_PASSWORD
#
# FLAG:
#
# 0 DON'T map the Linux-logins automatically to
# "mars_nwe"-logins (default)
#
# 1 YES, DO the automatic mapping and provide every login
# created this way with the common password given with
# "DEFAULT_PASSWORD"
#
# 99 re-read the logins from /etc/passwd and overwrite even the
```
