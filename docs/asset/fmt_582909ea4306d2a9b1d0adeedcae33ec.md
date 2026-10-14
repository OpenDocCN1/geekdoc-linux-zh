
```
Hit http://archive.ubuntu.com/ubuntu/quantal-security i386 Packages
Hit http://archive.ubuntu.com/ubuntu/quantal-security/restricted i386 Packages
Hit http://archive.ubuntu.com/ubuntu/quantal/main Sources
Hit http://archive.ubuntu.com/ubuntu/quantal-universe i386 Packages
Hit http://archive.ubuntu.com/ubuntu/quantal-multiverse i386 Packages
Hit http://archive.ubuntu.com/ubuntu/quantal-updates/main Sources
Hit http://archive.ubuntu.com/ubuntu/quantal-updates/restricted Sources
Hit http://archive.ubuntu.com/ubuntu/quantal-updates/universe Sources
Hit http://archive.ubuntu.com/ubuntu/quantal-updates/multiverse Sources
Hit http://archive.ubuntu.com/ubuntu/quantal-main i386 Packages
Hit http://archive.ubuntu.com/ubuntu/quantal-restricted i386 Packages
Hit http://archive.ubuntu.com/ubuntu/quantal-universe i386 Packages
Hit http://archive.ubuntu.com/ubuntu/quantal-multiverse i386 Packages
```

Reading package lists... Done

`matthew@semour:-$`

通过输入以下命令升级软件：

`matthew@semour:-$ apt-get dist-upgrade`

由于你已经检查了更新，Ubuntu 自动知道只下载并安装它需要的软件包。`dist-upgrade` 选项智能地工作，确保任何所需的依赖关系都能得到满足并安装，即使需要重大更改。

## sudo 命令

你也可以使用 `upgrade` 选项，它没有 `dist-upgrade` 智能，但在生产服务器上可能是更好的选择，因为 `upgrade` 不会对软件安装进行重大更改。这允许系统管理员在保持设置不变的情况下，更灵活地保持安全更新。

## sudo 命令

当你在命令行工作时，你会发现 Ubuntu 依赖 `sudo` 命令。该命令用在命令前面，告诉 Ubuntu 你想以超级用户权限运行指定的命令。这听起来很特别，实际上也如此。当你使用 `sudo` 命令时，可以对系统进行广泛更改。然而，运行任何 `sudo` 命令时都要小心；错误的选项或命令可能会导致破坏性的后果。

`sudo` 的用法非常直观。你只需要这样输入：

```
matthew@seymour# sudo command options
```

只需将 `command` 替换为你想要运行的命令以及任何选项。例如，以下命令以超级用户身份在 vi 中打开 `xorg.conf` 文件，并允许你在保存之前进行任何更改：

每当你使用 `sudo` 执行命令时，系统都会提示你输入密码。这是和你登录 Ubuntu 时相同的密码，所以记住它很重要。

然而，有时你可能想使用经典的 root 提示符，而不是在命令行每个需要超级用户权限的命令前都输入 `sudo`。例如，`sudo` 允许你通过 `sudo -i` 命令来实现。同样，系统会提示你输入密码，输入后 Ubuntu 会给你标准的 root 提示符，如下：

```
matthew@seymour:--#
```
