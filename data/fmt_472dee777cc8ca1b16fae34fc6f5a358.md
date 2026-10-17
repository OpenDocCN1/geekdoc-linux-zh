
`offsec_repository` 状态依赖于 `pkgrepo` 状态模块。示例使用该状态模块中的 `managed` 函数来注册软件包存储库。通过 `key_url` 属性，你告知 salt 验证存储库签名所需的（ASCII 装甲）GPG 密钥可以从 salt master 上的 `/srv/salt/offsec-apt-key.asc` 获取。`require_in` 属性确保此状态在 `offsec-defaults` 之前处理，因为后者需要正确配置存储库才能安装软件包。

`offsec-defaults` 状态安装同名的软件包。这表明键的名称对于状态通常是一个重要的值，尽管它始终可以通过 `name` 属性进行覆盖（如前一个状态所示）。对于像这样的简单情况，这既易读又简洁。

最后一个状态（`ssh_key_for_root`）将 `name` 属性中给出的 SSH 密钥添加到 `/root/.ssh/authorized_keys`（目标用户设置在 `user` 属性中）。请注意，我们在此处为了可读性缩短了密钥，但你应该在 `name` 属性中放入完整的密钥。

然后可以将此状态文件应用于给定的 Minion：

```bash
server# salt kali-scratch state.apply offsec
```

```
kali-scratch:
----------
    ID: offsec_repository
  Function: pkgrepo.managed
    Name: deb http://pkgrepo.offsec.com offsec-internal main
  Result: True
  Comment: Configured package repo 'deb http://pkgrepo.offsec.com offsec-internal
           main'
  Started: 06:00:15.767794
 Duration: 4707.35 ms
   Changes:  ------------
             repo:
               deb http://pkgrepo.offsec.com offsec-internal main
----------
    ID: offsec-defaults
  Function: pkg.installed
  Result: True
  Comment: The following packages were installed/updated: offsec-defaults
  Started: 06:00:21.325184
 Duration: 19246.041 ms
   Changes:  ------------
             offsec-defaults:
               ------------
               new:
                 1.0
               old:
----------
    ID: ssh_key_for_root
  Function: ssh_auth.present
```

它还可以通过将其记录在 `/srv/salt/top.sls` 文件中与 minion 永久关联，该文件被 `state.highstate` 命令用于一次性应用所有相关状态：

```bash
server# cat /srv/salt/top.sls
base:
    kali-scratch:
      - offsec
```

```bash
server# salt kali-scratch state.highstate
```

```
kali-scratch:
----------
            ID: offsec_repository
      Function: pkgrepo.managed
          Name: deb http://pkgrepo.offsec.com offsec-internal main
        Result: True
      Comment: Package repo 'deb http://pkgrepo.offsec.com offsec-internal main' already
               configured
         Started: 06:06:20.650053
       Duration: 62.805 ms
       Changes:
----------
            ID: offsec-defaults
      Function: pkg.installed
        Result: True
      Comment: Package offsec-defaults is already installed
         Started: 06:06:21.436193
       Duration: 385.092 ms
       Changes:
----------
            ID: ssh_key_for_root
      Function: ssh_auth.present
          Name: ssh-rsa AAAAB3NzaC1yc2...89C4N rhertzog@kali
        Result: True
      Comment: The authorized host key AAAAB3NzaC1yc2...89C4N is already present for user root
         Started: 06:06:21.821811
       Duration: 1.936 ms
       Changes:
Summary for kali-scratch
---
Succeeded:     3
Failed:        0
---
Total states run:     3
Total run time: 449.833 ms
```
