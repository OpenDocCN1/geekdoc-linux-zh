

## LISTING 5.19 使用 UID

```
erikkx:42120:10::/export/home/users/erikk:/bin/sh
42 = Department Intl. MIS
120 = Employee ID within the department
```

由于许多 *NIX 变体限制了变量 $MAXUID（在 Solaris 上理论上的 $MAXUID 为 2147483647），因此在实施此类方案时应谨慎。UID 高达 60000 通常是安全的。小于 100（Solaris）和小于 500（Linux）的 UID 分别用于特定账户，不应使用。

像 .rhosts 或 /etc/hosts.equiv 这样的文件的使用，尽管可能很方便，但应避免，或者至少只有在进行广泛的风险评估后才允许使用。这些文件可用于在不同系统上对用户进行身份验证，只需用户登录一次即可。如果其中一个系统被攻破，而所有其他系统都配置为使用上述文件相互信任，那么整个系统网络也会被攻破。在使用这些文件之前应三思而行。如果不使用这些文件（而且不应该使用），那么可能有必要采取预防措施，确保这些文件将来不会被激活（无论是意外还是其他原因）。对于 root 的 $HOME 中的文件 .netrc 也是如此。清单 5.20 显示了如何确保上述文件不能被使用或创建，除非是超级用户。

## LISTING 5.20 禁用 .rhosts、hosts.equiv 和 .netrc

```
root@unixhost> cd /
root@unixhost> touch .rhosts .netrc /etc/hosts.equiv
root@unixhost> chmod 0 .rhosts .netrc /etc/hosts.equiv
root@unixhost> ls -l .rhosts
--------- 1 root other 0 Sep 23 11:54 .rhosts
root@unixhost> ls -l .netrc
--------- 1 root other 0 Sep 23 11:54 .netrc
root@unixhost> ls -l /etc/hosts.equiv
--------- 1 root other 0 Sep 23 11:54 /etc/hosts.equiv
```

由于文件没有任何设置权限，只有 root 能够更改这些文件。文件 .netrc 在 Solaris 系统上位于 /，即 root 的 $HOME。具有 root 独立 $HOME 的系统应相应使用该命令。例如 GNU/Linux 使用 /root。如果系统允许用户登录，则应在他们的主目录中也创建指示的文件，以确保文件

```
root@unixhost# ls -al admintrans
total 3
drwxrwx--- 2 root admintrans 512 Sep 20 10:10 .
drwxr-xr-x 11 root other 512 Sep 20 10:07 ..
-rw-rw-r-- 1 silvied admintrans 89 Sep 20 10:14 monthlytasks.txt
```

清单 5.21 创建了一个供 admintrans 组成员共享的目录。用户 silvied、marionb 和 markusk 在该目录中具有读写权限。每个用户都能够读取、更改和删除由另一用户创建的文件；命令 chmod g+w admintrans 赋予了该组所有成员的权限。其他用户的全部权限已通过 chmod o-r,o-x admintrans 被撤销；只有 admintrans 组的成员才能使用该目录并列出其中的文件。

是否可以防止意外删除由另一用户创建的文件？每个 *NIX 系统上已经存在一种使用此类保护的目录，即 /tmp 目录。清单 5.22 显示了权限。

## LISTING 5.22 /tmp 目录

```
root@unixhost# ls -ld /tmp
drwxrwxrwt 6 root sys 381 Sep 20 11:13 /tmp
```

所谓的粘滞位用于防止一个用户删除由另一用户创建的文件。设置的粘滞位在权限中以字母 t 表示。如果用户在目录中具有写权限，则该用户能够删除文件，即使该用户对文件没有写权限。如果在目录上设置了粘滞位，则只有所有者和 root 能够删除文件。设置粘滞位如清单 5.23 所示。

## LISTING 5.23 设置粘滞位

```
root@unixhost# chmod +t admintrans
root@unixhost# ls -l
total 10
drwxrwx-T 2 root admintrans 512 Sep 20 13:31 admintrans
drwxr-xr-x 5 chrisk admintrans 512 Aug 23 15:33 chrisk
...
```

这次出现大写字母 T 的原因是在某些 *NIX 变体中没有为其他用户设置权限。命令 chmod +t <directoryname> 可以工作。

