
SSH 公钥指纹: `SHA256:soayP+ToVqBs9MrDc/tfF7kn0xHCS1Cf7861SKWO` `antonio@sierra.linuxaholics.local` (`ssh-rsa`)

账户禁用: `False`

密码: `True`

组成员: `ipusers`

可用 Kerberos: `True`

我们还有将 SELinux 用户映射到 FreeIPA 用户的可能性。首先，我们使用 `semanage` 列出可用的 SELinux 用户。

```
[root@quebec ~]# semanage user --list
```

| SELinux User | MLS/ Prefix | MCS Level | MCS Range | SELinux Roles |
| :--- | :--- | :--- | :--- | :--- |
| guest_u root | user | s0 | s0 | guest_r staff_r sysadm_r system_r unconfined_r |
| staff_u | user | s0 | s0-s0:c0.1023 | staff_r sysadm_r system_r unconfined_r |
| sysadm_u system_u | user | s0 | s0-s0:c0.1023 | sysadm_r system_r unconfined_r |
| unconfined_u user_u | user | s0 | s0-s0:c0.1023 | unconfined_r |

我们使用 `ipa selinuxmap-add` 命令添加 SELinux 用户映射。

```
[root@sierra ~]# ipa selinuxusermap-add sample_SELinux_user
--selinuxuser=user_u:s0
ipa: ERROR: SELinux user sysadm_u:s0 not found (in config)
```

在这种情况下我们收到了错误，因为所有的 SELinux 用户都已包含在内。我们可以通过 `ipa config-show` 命令查看。

```
[root@sierra ~]# ipa config-show | grep SELinux
SEinux user order: guest_u:s0,staff_u:s0,sysadm_u:s0,unconfined_u:s0
Default SELinux user: unconfined_u:s0
```

我们看到 `unconfined_u` 是 FreeIPA 使用的 SELinux 用户。事实上，我们以用户 `jose` 登录 `sierra.linuxaholics.local` 并运行 `id` 命令，这就是我们看到的 SELinux 上下文。

```
-sh-4.2$ id
uid=974400003(jose) gid=974400003(jose) groups=974400003(jose) context=unconfined_u:unconfined_t:s0:c0.1023
```

我们可以通过 `ipa config-mod` 修改 FreeIPA 配置以包含更多的 SELinux 用户，但由于我们只对概念证明，我们将使用已定义的 SELinux 用户创建映射。

# 第 25 章 FreeIPA 实体管理

我们还将适用于 SELinux 映射的用户也添加到其中。

```
[root@sierra ~]# ipa selinuxusmap-add-user sample_SELinux_user_user
--users=jose
Rule name: sample_SELinux_user_map
SELinux User: user_u:s0
Enabled: TRUE
Users: jose
```

添加了 1 个成员

我们重启 `sssd` 服务，并登录 `sierra.linuxaholics.local`。

```
-sh-4.2$ id
uid=974400003(jose) gid=974400003(jose) groups=974400003(jose)
context=user_u:r:user_t:s0
```

我们看到 SELinux 上下文已根据映射的内容发生了了相应的更改。

```
[root@quebec ~]# su - jose
Last login: mie feb 20 12:58:25 CET 2019 on pts/0
s: warning: cannot change directory to /home/jose: No such file or
directory
-sh-4.2$ id
uid=597800004(jose) gid=597800004(jose) groups=597800004(jose) context=unconfined:u:unconfined_r:unconfined_t:s0:c0.c1023
```

`NIS` 是类 Unix 系统最早的集中管理解决方案之一。然而，现在它在很大程度上被 FreeIPA 等系统取代了。为了方便起见，FreeIPA 包含了几个有助于从 NIS 迁移到 FreeIPA 的功能。

首先，我们必须使用 FreeIPA 组来集成 NIS 实体。此外，我们应该启用安装时包含的 NIS 监听器和兼容插件。

```
[root@quebec ~]# ipa-nis-manage start
[root@quebec ~]# ipa-compat-manage status
```

最后，我们应该启动端口映射服务并重启目录服务器。

```
[root@quebec ~]# systemctl start rpcbind
[root@quebec ~]# systemctl start dirsrv
```

## 基于主机的访问控制 (HBAC)

FreeIPA 可以允许或拒绝任何用户访问任何主机。这被称为基于主机的访问控制 (`HBAC`)。默认情况下，定义了一个 HBAC 规则允许所有用户访问任何主机。

```
[root@quebec ~]# ipa hbacrule-find
```

匹配到 1 条 HBAC 规则

Rule name: `allow_all`

User category: `all`

Host category: `all`

Service category: `all`

Description: 允许所有用户从任何主机访问任何主机

Enabled: `TRUE`

返回 1 个条目

然而，如果我们想根据 HBAC 限制访问，可以创建我们自定义的 HBAC。

```
[root@quebec ~]# ipa hbacrule-add "Customized rule" -desc="Restricting access"
```

已添加 HBAC 规则 `"Customized rule"`

Rule name: `Customized rule`

Description: `Restricting access`

Enabled: `TRUE`

### 第 25 章 FreeIPA 实体管理

创建规则后，我们向其添加了一些主机和用户。

```
[root@quebec ~# ipa hbacrule-add-host "Customized rule" --hosts="romeo.linuxaholics.local"
Rule name: Customized rule
Description: Restricting access
Enabled: TRUE
Hosts: romeo.linuxaholics.local
```

添加了 1 个成员

```
[root@quebec ~#] ipa hbacrule-add-user "Customized rule" --users=jose
Rule name: Customized rule
Description: Restricting access
Enabled: TRUE
Users: jose
Hosts: romeo.linuxaholics.local
```

添加了 1 个成员

此外，我们必须指定受 HBAC 规则影响的一个（或多个）服务。

```
[root@quebec ~#] ipa hbacrule-add-service "Customized rule" --hbacsvcs=sshd
Rule name: Customized rule
Description: Restricting access
Enabled: TRUE
Users: jose
Hosts: romeo.linuxaholics.local
Services: sshd
```

添加了 1 个成员

现在，该规则允许用户 `jose` 访问主机 `romeo.linuxaholics.local` `sshd` 服务。要检查这一点，我们可以使用 FreeIPA 提供的测试工具。
