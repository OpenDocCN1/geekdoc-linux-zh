
使用 `MASQUERADE_AS` 宏来启用伪装。例如，要对 `foobirds.org` 进行伪装，请在宏配置中放入以下命令：

```
MASQUERADE_AS(`foobirds.org`)
```

`MASQUERADE_AS` 命令提供的名称应该是一个有效的、规范的 DNS 名称（canonical DNS name）。通常，当使用伪装为整个企业创建一个简化的、标准的地址格式时，它是一个域名而不是主机名。

上述 `MASQUERADE_AS` 命令的效果与将 `sendmail1.cf` 中的 `M` 变量设置为 `foobirds.org` 相同。事实上，`MASQUERADE_AS` 仅仅是 `M` 的一个值。列表 9.2 证明了这一事实。

### 列表 9.2 `MASQUERADE_AS` 对 `sendmail.cf` 的影响

```
[root] # diff ../domain/old-foobirds.m4 ../domain/foobirds.m4
8a9
> MASQUERADE_AS(`foobirds.org`)' > dn1
[root] # m4 ../m4/cf.m4 redhat811.mc > masquerade.cf
[root] # diff plain.cf masquerade.cf
12c8c128
< DM

> foobirds.org
```

在列表 9.2 中，第一个 `diff` 命令显示，两个 `DOMAIN` 文件之间的唯一区别是，新文件包含一个 `MASQUERADE_AS` 命令，而 `old-foobirds.m4` 中没有找到该命令。新文件通过 `m4` 处理以构建 Sendmail 配置。`plain.cf` 配置文件是在列表 9.1 中创建的。列表 9.2 创建了名为 `masquerade.cf` 的配置。第二个 `diff` 比较了这两个文件的内容。`plain.cf` 文件在 `M` 中没有存储值，而 `masquerade.cf` 文件在 `M` 中存储了 `foobirds.org`。这是这些配置之间的唯一区别，也是 `MASQUERADE_AS` 命令做的唯一更改。

根据我们在第 7 章进行的测试，我们知道在 `M` 中存储一个值会导致 Sendmail 将标头地址的主机端口重写为 `M` 中找到的值。存在一些限制条件：`M` 中的值仅在发现地址中的主机端口时才会被重写标头地址。通过我们在第 7 章进行的测试我们知道了这一点。列表 9.3 展示了这些效果。

### 列表 9.3 测试 `MASQUERADE_AS` 的默认设置

```
[root] # sendmail -bt -masquerade.cf
ADDRESS (ruleset 3 automatically invoked)
Enter <ruleset>
=$w
wren.foobirds
[172.16.0.1]
localhost
>/tryflags HS
> /try esmtp @wren.foobirds.org
header sender address @wren.foobirds.org for mailer esmtp
canonify input: @wren.foobirds.org
...
final:
 returns: @wren.foobirds.org
Rcode = 0, addr=wren.foobirds.org
> /tryflags ES
> /try esmtp @wren.foobirds.org
header sender address @wren.foobirds.org for mailer esmtp
canonify input: @wren.foobirds.org
...
final:
 returns: @wren.foobirds.org
Rcode = 0, addr=wren.foobirds.org
> ^D
```

列表 9.3 经过了大量的编辑以保持其合理的长度，但显示默认伪装设置的关键元素是：首先，我们显示类 `w` 的内容，证明它包含四个值；这些是将被伪装的四个名称。我们使用 `/tryflags` 命令请求对 `wren.foobirds.org` 标头进行 `esmtp` 处理。地址被重写为 `foobirds.org`，证明了该配置将 `wren.foobirds.org` 伪装为 `foobirds.org`（头部发送者地址）。接下来，我们处理 `hawk.foobirds.org` 作为 `esmtp` 邮件头部。地址被重写为 `foobirds.org`，证明了该配置将 `hawk.foobirds.org` 伪装为 `foobirds.org`（头部发送者地址）。

### 伪装选项

`w` 中主机的默认伪装设置通常足够了。通常，伪装的目的是为远程用户提供正确的回复。本地系统不会接受发送到 `M` 中主机的邮件。

如果伪装不足以满足需求，还有两个功能可以将伪装扩展到其他类型的地址。这些功能是：

- `FEATURE(masquerade-envelope)` 此功能导致 Sendmail 伪装信封地址（envelope addresses）。如果设置了此功能，列表 9.2 中的第三次测试将导致 `wen.foobirds.org` 在信封中伪装为 `foobirds.org`。如果伪装是为了满足安全策略，则此功能非常有用。

- `FEATURE(allmasquerade)` 此功能导致 Sendmail 伪装接收者地址。通常，这不是一个好主意。伪装是针对外发邮件的源地址的。更改入站邮件的地址没有意义，因为本地系统的用户已经知道该真实名称。

当使用默认设置配合 `MASQUERADE_AS(foobirds.org)` 时，将从 `foobirds.org` 发出。但如果同时也使用了 `FEATURE(limited_masquerade)`，邮件将以来自 `bridal-gowns.com` 的名义发送，除非你显式地将 `bridal-gowns.com` 添加到类 `M` 中。

使用 `MASQUERADE_DOMAIN` 为类 `M` 添加单个值。例如，要将 `hawk.foobirds.org` 添加到类 `M`，可以在宏配置文件中添加 `m4` 宏：

```
MASQUERADE_DOMAIN(`hawk.foobirds.org`)
```

当仅需要向类 `M` 添加少数几个值，且这些值不经常发生变化时，`MASQUERADE_DOMAIN` 最为有用。当你有多个（多于几个）想要伪装的域名名时，使用 `MASQUERADE_DOMAIN_FILE` 从文件中加载类 `M`。假设你想要从一个名为 `/etc/mail/masquerade-domain-names` 的文件中加载类 `M`。你可以在配置文件中添加以下 `m4` 宏：

```
MASQUERADE_DOMAIN_FILE(`/etc/mail/masquerade-domain-names`)
```

正如 `MASQUERADE_DOMAIN` 的名称所示，存储在类 `M` 中的值并不必须是主机名；它们可以是全域名名。默认情况下，输入地址的主机名部分必须与类或类 `M` 中的值完全匹配，才能重写为伪装值。因此，如果类 `M` 包含 `terms.foobirds.org`，则输入地址 `kerstan.terms.foobirds.org` 被重写，除非地址 `kerstan.sooty.terms.foobirds.org` 不被重写。这意味着，如果在类或 `M` 中找到了域名，请使用 `FEATURE(masquerade_entire_domain)` 来更改此默认行为，使得类或类 `M` 中域名的每个组件都进行伪装。如果指定了 `masquerade_entire_domain` 且类 `M` 包含 `terms.foobirds.org`，则输入地址 `kerstan.terms.foobirds.org` 被重写，同样地，地址 `kerstan.sooty.terms.foobirds.org` 也是如此。列表 9.4 说明了这些选项对伪装的影响。

### 列表 9.4 测试特殊伪装选项

```
[root]# diff ../old/foobirds.m4 ../foobirds.m4
8a9,12
 MASQUERADE_AS(`foobirds.org`)`dn1
> MASQUERADE_DOMAIN(`foobirds.org`)`dn1
> FEATURE(`limited_masquerade`)`dn1
> FEATURE(`masquerade_entire_domain`)`dn1
[root]# m4 ../m4/m4 redhat811.mc > masquerade.cf
[root]# sendmail -bt -masquerade.cf
```

![](img/9639113aa446fb8976cb3d377f7aafdd_276_0.png)

地址测试模式（规则集 3 不自动调用）
