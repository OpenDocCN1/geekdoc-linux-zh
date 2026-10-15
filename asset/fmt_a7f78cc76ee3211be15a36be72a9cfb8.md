
如第 257 页表 11.7 所述，`StrictHostKeyChecking` 的默认值为 `ask`。示例 11-6 展示了确保客户端首次连接到服务器时的对话框。通过回答“`Are you sure you want to continue connecting (yes/no)`”（您确定要继续连接吗（是/否）？）这个问题，客户端（`underdog`）将导致服务器（`pluto`）的公共主机密钥（位于服务器 `pluto` 的 `/etc/ssh/ssh_host_key` 中）被添加到用户（`mary`）的 `$HOME/.ssh/known_hosts` 文件中。如果将 `StrictHostKeyChecking` 设置为 `no`，则公共主机密钥会自动添加（无需提示）。

## 示例 11-6 首次连接的默认行为

```text
[mary@underdog]# ssh pluto
Host key not found from the list of known hosts.
Are you sure you want to continue connecting (yes/no)? yes
Host 'pluto' added to the list of known hosts.
Last login: Tue Jun 29 19:02:42 1999 from underdog
[mary@pluto]$
```

示例 11-7 中显示的条目是在用户的 `$HOME/.ssh/known_hosts` 文件中找到的条目。此文件的语法是主机名（`pluto`），后跟模数的位数（`1024`），然后是指数（`37`），最后是模数本身（那个跨五行换行的很长数字）。该条目代表一行，或一条记录。

## 示例 11-7 $HOME/.ssh/known_hosts 中 pluto 的条目

```text
pluto 1024 37 139857661633970133381559171353939443804008080590757470781931602
022871170094795293291221715550255203037833736537193262559154533114496229328
637585395026090985398431650030267428626207532711814567600329166509482267712
63643216843142397128397352098050110711040730851803084717186416878255559722
327548734329098524150772854588750069
```

如示例 11-8 所示，同一条记录在服务器的 `/etc/ssh/ssh_host_key.pub` 文件中看起来略有不同。此文件的语法是模数的位数（`1024`），然后是指数（`37`），接着是模数本身（那个跨五行换行的长数字），最后是 `user@hostname`（`root@pluto`，这是一个注释字段）。请注意，对于服务器的公共主机密钥，用户始终为 `root`。

## 示例 11-8 pluto 上 pluto 的 /etc/ssh/ssh_host_key.pub 条目

```text
1024 37 13985766163397013338155917135393944380400808059075747078193160222871
170911955529229121715551502030703783373653719326255915453311449622966855
59526099995938451650602626742862620753271181456760029166504982866712
68431429735209850110711040730851803084717186416878255597223272548
327548734329098524150772854588750069 root@pluto
```

从这两个示例中，应该可以看出，将公共主机密钥整合到其他主机的一种方式是将条目从服务器文件手动复制到客户端的 `/etc/ssh/ssh_known_hosts` 文件中。相反，您也可以将其添加到特定用户的 `$HOME/.ssh/known_hosts` 文件中，但这样只有该用户才能访问该密钥。系统范围文件 `/etc/ssh/ssh_known_hosts` 的用途是包含所有经常连接的服务器，而用户的 `$HOME/.ssh/known_hosts` 文件应包含用户经常连接但其他用户通常不连接的服务器。

如果用户回答示例 11-6 中显示的问题“`are you sure you want to continue connecting (yes/no)?`”（您确定要继续连接吗（是/否）？）为 `no`，则连接将简单地终止。类似地，如果在 `$HOME/.ssh/config` 中的调用用户或客户端系统的 `/etc/ssh/ssh_config` 中，`StrictHostKeyChecking` 被设置为 `yes`，则连接也将失败。在后一种情况下，您将得到如下错误消息：

```text
No host key is known for pluto and you have requested strict checking.
```

此设置将提高安全性，因为密钥的自动更新可能因欺骗或中间人攻击而被破坏。不幸的是，在大型环境中，这可能意味着过多的人工工作量，而在这些环境中，冒此类攻击的风险可能是必要的。然而，由于这是初始身份验证步骤，通过其他强制身份验证步骤（如 `RSA` 身份验证，在第 293 页的 *RSA Authentication Configuration* 中讨论）可以大大减轻这种风险。

**应对主机密钥变更。** 基于主机的 `RSA` 身份验证的另一个方面是，可能定期需要更改服务器的主机密钥。这可能是密钥泄露的结果，也可能是因为您的站点策略规定定期更改。无论原因如何，当服务器公共主机密钥与存储在 `/etc/ssh/ssh_known_hosts` 或 `$HOME/.ssh/known_hosts` 文件中的密钥不同时，就会出现类似示例 11-9 中所示的警告。请注意，代理转发（在第 301 页的 *Managing RSA Authentication with ssh-agent and ssh-add* 中讨论）和 `X Window System` 转发（在第 301 页的 *Managing RSA Authentication with ssh-agent and ssh-add* 和第 304 页的 *ssh Examples* 中讨论）已被禁用。再次出现“`are you sure you want to continue connecting (yes/no)?`”（您确定要继续连接吗（是/否）？）这个问题，是因为 `StrictHostKeyChecking` 被设置为 `ask`。回答这个问题为 `yes` 不会更新 `Mary` 的 `$HOME/.ssh/known_hosts` 文件中的密钥，并且该消息会在每次后续连接中重复出现，直到消除差异为止。`Mary` 可以手动完成此操作，或者通过从她的 `$HOME/.ssh/known_hosts` 文件中删除相应的条目，这将导致示例 11-6（第 285 页）中显示的对话框在她下次调用 `ssh` 连接到 `underdog` 时再次出现。

3. 所有密钥都使用 `ssh-keygen` 实用程序进行更改。具体来说，更改主机密钥在第 297 页的 *Using ssh-keygen for root*（为 `root` 使用 `ssh-keygen`）中进行了讨论。

## 示例 11-9 因主机密钥变更而出现的警告消息
