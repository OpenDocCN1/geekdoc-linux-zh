
两种接口都可以作为 `ipsec0`。第二个还支持通过 PPP 接口进行 IPSEC。如果不使用默认设置=`defaultroute`，则指定的接口将是网关与其它 IPSEC 网关通信的唯一通道。

`klipsdebug=none`
此选项指定 KLIPS（内核 IP SEC）的调试输出。默认值为 `none`，意味着没有调试输出；而值 `all` 表示全量输出。

`plutebug=none`
此选项指定 Pluto 密钥的调试输出。默认值 `none` 表示没有调试输出；而值 `all` 表示全量输出。

`plutoload=%search`
此选项指定在 Pluto 启动时自动加载到内存中的连接（通过名称）。默认是 `none`，值 `%search` 加载所有带有 `auto=add` 或 `auto=start` 的连接。

`plutostart=%search`
此选项指定在 Pluto 启动时自动协商的连接（通过名称）。默认是 `none`，值 `%search` 启动所有带有 `auto=start` 的连接。

`conn deep-mail`
此选项指定用于使用 IPSEC 创建的连接规范的名称。一种良好的命名约定是根据连接的终点来命名，以避免错误。例如，`deep.openarch.com` 和 `mail.openarch.com` 服务器之间的链路可以命名为 "`deep-mail`"，或者蒙特利尔与巴黎网关之间的链路。

请注意，"`deep-mail`" 或你选择的任何名称在两个网关的 "`ipsec.conf`" 文件中必须相同。换句话说，你在第二个网关的 "`/etc/ipsec.conf`" 文件中唯一需要更改的是修改 "`interfaces=`" 这一行，以匹配第二个网关用于 IPSEC 连接的接口（如果它与第一个网关不同）。例如，如果使用 `eth0` 接口进行 IPSEC 通信，则你不需要更改第二个网关上的 "`interfaces=`" 行。在

© Copyright 1999-2000 Gerard Mourani and Open Network Architecture ®

关于本书的意见和建议应邮邮件至 `gmourani@videotron.ca`

另一种情况下，如果第一个网关使用 `eth0` 而第二个使用 `eth1`，你必须更改第二个网关上的 "`interfaces=`" 行以匹配接口 `eth1`。

`left=208.164.186.1`
此选项指定网关外部接口的 IP 地址，该接口用于与另一个网关通信。

`leftsubnet=192.168.1.0/24`
此选项指定网关后私有子网的 IP 网络或地址。

`leftnexthop=205.151.222.250`
此选项指定相应方向上的第一个路由器或 ISP 路由器的 IP 地址。

`right=208.164.186.2`
这与 "`left=`" 的解释相同，但针对右端。

`rightsubnet=192.168.1.0/24`
这与 "`leftsubnet=`" 相同，但针对右端。

`rightnexthop=205.151.222.251`
这与 "`leftnexthop=`" 相同，但针对右端。

`keytries=0`
此选项指定进行重密钥（keying）协商的尝试次数（整数）。建议值为 `0`（无限次）。

`auth=ah`
此选项指定是单独使用 AH（认证头）还是作为 ESP（封装载荷）的一部分进行身份验证。后者更优，可以防止中间人攻击。

`auto=start`
此选项指定是否自动启动。注意："`ipsec.conf`" 中的配置不匹配会导致 FreeS/WAN 失败并记录各种错误信息。

# 配置 `/etc/ipsec.secrets` 文件

"`ipsec.secrets`" 存储密钥。在该文件中可以配置两种不同类型的密钥：共享密钥和 RSA 私钥。你必须检查此文件的权限并阻止他人访问。

## 步骤 1
"`ipsec.secrets`" 默认了一个示例密钥，你应该通过创建自己的密钥来更改它。通过自动密钥，可能会获得一个 256 位的共享密钥，它在密钥交换期间使用以确保不会发生中间人攻击。要创建一个新密钥，使用以下命令：

```
ipsec rankey 256 > temp
```

使用 `rankey` 工具创建一个名为 "`temp`" 的新密钥。如果没有没有足够的熵，`rankey` 工具可能会暂停几秒。

© Copyright 1999-2000 Gerard Mourani and Open Network Architecture ®

关于本书的意见和建议应邮邮件至 `gmourani@videotron.ca`

**注意：** 不要忘记删除你创建的临时文件。

## 步骤 2
现在已经在 "`temp`" 文件中创建了共享密钥，我们将其放入 `/etc/ipsec.secrets` 文件，你会在编辑器中看到如下内容。每行包含两个网关的 IP 地址加上密钥。它看起来应该是：

```
# 此文件持有当前的身份验证机制。由 ipsec_pluto(8) 管理。每个密钥对应一对主机。共享密钥是任意字符串，应该足够长且难以猜测。注意，即使没有空格，所有密钥也必须包含在引号内。

10.0.0.1 11.0.0.1 "jXv1kVVUTRtnTujSm444jauU1mku2nW3nnvuW2jRulmikU1Ru5NNRT"
```

编辑 `ipsec.secrets` (`/etc/ipsec.secrets`) 并更改默认密钥：

```
10.0.0.1 11.0.0.1 "jXv1kVVUTRtnTujSm444jauU1mku2nW3nnvuW2jRulmikU1Ru5NNRT"
```

读取：
```
208.164.186.1 208.164.186.2

"09748c3_2e9919f_d23056b_dc64b57_dc07b01_74bf34_19c0a1a80490ed"
```

其中 `208.164.186.1 208.164.186.2` 是两个网关的 IP 地址，而 `"09748c3_2e9919f_d23056b_dc64b57_dc07b01_74bf34_19c0a1a80490ed"`（注意需要引号）我们用命令 `ipsec rankey 256 >` 生成的共享密钥位于 "`temp`" 文件。

## 步骤 3
"`ipsec.conf`" 和 "`ipsec.secrets`" 必须复制到第二个网关机器，以确保两端相同。唯一的例外来自 "`ipsec.conf`" 文件，如果第二个网关的接口设置与第一个网关不同，则该文件中由配置设置标记的部分必须包含第二个网关正确的接口设置。包含 RSA 私钥的 "`ipsec.secrets`" 文件在两个网关上应具有相同的共享密钥。

注意：文件 "`/etc/ipsec.secrets`" 应该具有权限 `rw-------` (`600`) 并由超级用户 "`root`" 所有。文件 "`/etc/ipsec.conf`" 安装权限为 `rw-r-r--` (`644`) 并必须由 "`root`" 所有。

# 配置 RSA 私钥

回想使用 FreeSwan 有两种密钥：共享密钥和 RSA 私钥。共享密钥是我们在 "`ipsec.conf`" 和 "`ipsec.secrets`" 文件示例中配置的内容。有些人可能倾向于使用 RSA 私钥通过其他主机的 Pluto 进行验证。如果你处于这种情况，你将按照以下步骤对你的 "`ipsec.conf`" 和 "`ipsec.secrets`" 文件进行一些修改：

© Copyright 1999-2000 Gerard Mourani and Open Network Architecture ®

```
leftsubnet=192.168.1.0/24

leftnthop=205.151.222.250

right=208.168.2

rightsubnet=192.168.1.0/24

rightnthop=205.151.222.251

keytrips=0

auth=none

authbyrsasig

leftrasigkey=<Public key deep>

rightrasigkey=<Public key mail-

auto=start
```

`authby=rsasig`
此参数指定两个网关如何相互验证身份。默认值是用于共享密钥的 `secret`。由于我们决定使用 RSA 数字签名，因此必须对 RSA 使用 `rsasig`。

`leftrasigkey=<Public key deep>`
此参数指定左侧参与用于 RSA 签名认证的公钥。在我们的示例中，它是 `208.164.186.1`，代表 `mailopen.com`。我们必须在这一行放入 `deep` 的 RSA 密钥。

`rightrasigkey=<Public key mail>`
此参数指定右侧参与用于 RSA 签名的公钥。在我们的示例中，它是 `208.164.186.2`，代表 `mailopen.com`。我们必须在这一行放入 `mail` 的 RSA 密钥。

你可以在上述步骤 1 中创建的 RSA 密钥文件中获取 `deep` 的密钥，并从名为 "`mail-keys`" 的 RSA 密钥文件中获取 `mail` 的密钥。这些文件的内容如下：

```
RSA key for gateway deep (deep-keys):

[root@deep] # cd /
```
