
好了，现在更安全了。

您应该注意规则的顺序。如果您交换前两个 `<Directory>` 块的位置，其效果将是您的用户无法在他们的主目录中查看、读取或写入任何内容。思路是先阻止全局访问，然后允许某些路径。

> TIP
> 使用我们刚刚解释的方法禁止用户浏览其主目录之外的内容，可以通过一个标签来完成。使用 `DefaultRoot` 标签，您可以将用户监禁在其主目录的边界内。例如，在配置文件中输入 `DefaultRoot ~ users` 将导致 `users` 组中的任何用户的根目录变为该用户的主目录。当该用户登录时，他将无法移出其主目录。应该注意的是，此方法并非 100% 安全——用户有办法从此监狱中逃脱。这就是我们之前解释的方法更安全的原因。

到目前为止，您已使用 `AllowAll` 和 `DenyAll` 标签来告诉 `<Limit>` 该做什么。您也可以使用 `AllowUser`、`AllowGroup`、`DenyUser` 和 `DenyGroup` 来更灵活地操作。每个标签都接受用户、组或它们的列表作为参数。例如，以下允许用户 `john` 和用户 `mary`：

```
<Limit READ>

    AllowUser john, mary

</Limit>
```

相比之下，以下代码允许用户 `john` 但不允许用户 `mary`。`!` 是逻辑非：

```
<Limit READ>

    AllowUser john, !mary

</Limit>
```

## 杂项选项

以下是一些常用的标签，可用于进一步定义 `proftpd` 的工作方式：

- `AllowRetrieveRestart`—此选项设置为 `on`（默认）时，允许客户端恢复中断的文件检索。建议您将此选项设置为 `on`。
- `AllowStoreRestart`—此选项设置为 `on` 时，允许客户端恢复向服务器中断的文件上传。我们不建议您将其设置为 `on`，因为这将允许各种用户损坏现有文件。其默认设置是 `off`。
- `CDPath`—这与 shell 的 `CDPATH` 环境变量完全相同。它接受一个路径作为参数，允许用户通过仅指定其名称直接将工作目录更改为该路径内的任何目录。例如，假设您有一个名为 `/usr/local` 的目录，在其中您有 `/usr/local/files`。将 `CDPath` 设置为 `/usr/local/`，如下所示：

```
CDPath /usr/local/
```

将允许任何用户通过仅键入以下内容来更改其工作目录到 `/usr/local/files`，而不管该用户当前在文件系统中的位置如何：

```
cd files
```

- `DefaultTransferMode`—`ftp` 使用两种传输模式之一——`ASCII` 用于文本文件，二进制用于其他文件。通常，`ftp` 客户端会根据正在传输的文件类型告诉服务器使用哪一种。您可以在必要时告诉 `proftpd` 默认使用哪一种。以下是一个示例：

```
DefaultTransferMode binary
```
