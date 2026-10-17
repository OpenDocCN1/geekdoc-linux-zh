
成功完成安装后，产品已准备好配置并启动。

## 9.4 配置 NetVault

在本节中，我们将描述如何配置 IBM 3583。其他 LTO 模型使用类似的配置方法。请参阅《NetVault 管理员指南》获取常规操作信息。

Linux 和 Windows 2000 之间的 NetVault 配置差异非常小。这些差异将在必要处进行突出显示。

最初需要执行 NetVault 配置器以验证基础 NetVault 配置。

在 Windows 2000 中，选择“开始 → 程序 → NetVault 6”来启动 NetVault 配置器。

在 Linux 中，NetVault 配置器从 Linux 命令行启动，并需要 X 显示。

命令是：

```
/usr/NetVault6/bin/nvconfigurator
```

你将看到图 9-11 所示的面板。

![](img/a48407b38d72fd58ea3627423836388a_378_0.png)

图 9-11 NetVault 配置器

我们不需要对配置器中的任何字段进行更改；但是我们从 BakBone 网站下载了最新的补丁：

```
http://www.bakbone.com/support/patches_and_updates/
```
