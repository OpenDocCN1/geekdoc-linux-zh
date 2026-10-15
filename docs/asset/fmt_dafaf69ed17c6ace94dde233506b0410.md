
由于我们仍然从 23.5.2 节设置了 `_CAA_UI_FMT` 环境变量，我们将启动 `powerUP` 资源但仅使用 `grep(1)` 过滤 `_CAA_CLIENT_LOCALE` 输出。

```
# caa_start powerUP | grep _CAA_CLIENT_LOCALE
_CAA_CLIENT_LOCALE = "C C C C C C"
```

有关区域设置的更多信息，请参阅 `locales(5)`、`locale(1)` 和 `setlocale(3)` 参考页面。

## 23.6 重新审视资源属性

我们对资源属性这个话题进行了一些思考，考虑了本章前面呈现的表格（参见第 23.4.4 节），并且几个有趣的问题涌入了我们集体的脑海（可怕吧？）。现在我们确信我们的出版商正摇着头，因为本章的页数在我们这些谦卑作者的疯狂科学家般的思维下不受控制地增长，但我们被迫以奇怪和随机的方式思考——对不起亲爱的出版商，对不起。到底是什么问题？请继续阅读。

在下面的示例中，依赖资源是 `memberUP`，支持的资源是 `nicUP`（网络资源）和 `powerUP`（应用资源）。

### 23.6.1 依赖关系——可选还是必需？

- 如果一个资源依赖于另一个资源，会发生什么如果它所依赖的资源消失或迁移？

要回答这个问题，让我们考虑两种场景：

- 1. `powerUP` 是 `memberUP` 的 `OPTIONAL_RESOURCE`。

```
# caa_stat -t -v memberUP powerUP
```

| Name | Type | R/RA | F/FT | Target | State | Host |
|---|---|---|---|---|---|---|
| memberUP | application | 0/1 | 0/0 | OFFLINE | OFFLINE | |
| powerUP | application | 0/1 | 0/0 | ONLINE | ONLINE | molari |

更新 `memberUP` 的配置文件，使 `powerUP` 成为 `OPTIONAL_RESOURCE`。

```
# caa_profile -update memberUP -l powerUP
```

使用更新后的 `memberUP` 配置文件更新 CAA 注册表并启动 `memberUP`。

```
# caa_register -u memberUP && caa_start memberUP
Attempting to start "memberUP" on member "molari"
Start of "memberUP" on member "molari" succeeded.
```

好的，两个资源都在 `molari` 上运行。让我们停止 `powerUP`。

```
# caa_stop powerUP
Attempting to stop "powerUP" on member "molari"
Stop of "powerUP" on member "molari" succeeded.
```

这对 `memberUP` 有不利影响吗？

```
# cca_status -v -w memberUP,powerUP
Name       Type         R/RA   F/FT   Target   State    Host
memberUP   application  0/1    0/0    ONLINE   ONLINE   molari
powerUP    application  0/1    0/0    OFFLINE  OFFLINE
```

应该吗？不，`powerUP` 只是“可选”，因此 `memberUP` 不会停止（甚至不会迁移）。如果 `powerUP` 是“必需”的 however...

- 2.

`powerUP` 是 `memberUP` 的 `REQUIRED RESOURCE`。

我们在这里需要做的第一件事是修改 `memberUP` 的配置文件，停止 `memberUP`，并更新注册表。

```
# cca_profile -update memberUP -l " " -R powerUP; cca_stop memberUP

Attempting to stop memberUP on member 'molari'
Stop of 'memberUP' on member 'molari' succeeded.
```

```
# cca_register -u memberUP ; cca_start memberUP

Attempting to start 'powerUP' on member 'molari'
Start of 'powerUP' on member 'molari' succeeded.
Attempting to start 'memberUP' on member 'molari'
Start of 'memberUP' on member 'molari' succeeded.
```

请注意 `powerUP` 也启动了。这是因为 `memberUP` 现在要求 `powerUP` 在同一成员上运行。让我们看看如果我们尝试迁移或停止 `powerUP` 会发生什么。

```
# cca_relocate powerUP

sheridan : Resource memberUP (application) is running on molari

Resource powerUP has placement error.
```

```
# cca_stop powerUP

Resources depending on powerUP are running
Resource powerUP has placement error.
```

没有成功。我们能否强制 `powerUP` 迁移或停止？`caa_relocate`（或 `caa_start`）命令的“-f”选项允许 CAA 停止和/或启动应用程序资源所依赖的那些资源，以使任务成功。例如，由于我们想将 `memberUP` 迁移到 `molari`，但 `memberUP` 需要 `powerUP`（目前在 `sheridan` 上），同时停止 `powerUP` 以及 `memberUP` 并将它们都启动在 `molari` 上。

```
# caa_relocate powerUP -f
Attempting to stop 'memberUP' on member 'molari'
Stop of 'memberUP' on member 'molari' succeeded.
Attempting to stop 'powerUP' on member 'molari'
Stop of 'powerUP' on member 'molari' succeeded.
Attempting to start 'powerUP' on member 'sheridan'
Start of 'powerUP' on member 'sheridan' succeeded.
Attempting to start 'memberUP' on member 'sheridan'
Start of 'memberUP' on member 'sheridan' succeeded.
```

```
# caa_stat -t -v memberUP powerUP
Name            Type        R/RA  F/FT  Target    State   Host
---------------------------------------------------------------
memberUP        application 0/1   0/0   ONLINE    ONLINE  sheridan
powerUP         application 0/1   0/0   ONLINE    ONLINE  sheridan
```

```
# caa_stop powerUP -f
Attempting to stop 'memberUP' on member 'sheridan'
Stop of 'memberUP' on member 'sheridan' succeeded.
Attempting to stop 'powerUP' on member 'sheridan'
Stop of 'powerUP' on member 'sheridan' succeeded.
```

```
# caa_stat -t -v memberUP powerUP
Name            Type        R/RA  F/FT  Target    State   Host
---------------------------------------------------------------
memberUP        application 0/1   0/0   OFFLINE   OFFLINE
powerUP         application 0/1   0/0   OFFLINE   OFFLINE
```
