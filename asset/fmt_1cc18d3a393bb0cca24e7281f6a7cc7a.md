
这会在你的整个 Web 空间中禁用 `exec` 和包含 SSI 命令；但是，你可以通过定义范围更窄的目录容器来在需要时启用这些命令，例如：

```apache
<Directory />

    Options IncludesNOEXEC

</Directory>

<Directory "/ssi*">

    Options +Includes

    SetOutputFilter INCLUDES

</Directory>
```

此配置片段在全局范围内禁用了 `exec` 命令，但在 `/ssi` 目录中除外。

还要避免使用 `printenv` 命令，该命令会打印出所有现有环境变量及其值。例如，命令：

```bash
<--#printenv -->
```
