
按照指定在 `serverb` 上准备一个 `kickstart` 文件，并将其放在 `http://serverb.lab.example.com/ks-config/kickstart.cfg` 供访问。使用你准备的 `kickstart` 文件在 `servera` 上执行 `kickstart` 安装。

### 准备 kickstart 文件

- 在 `serverb` 上，将 `/root/anaconda-ks.cfg` 复制到 `/home/student/kickstart.cfg`，以便学生可以编辑。

- 使用 `ssh` 命令以用户 `student` 登录 `serverb`。

```
[student@workstation ~]$ ssh student@serverb

...output omitted...

[student@serverb ~]$
```

- 将 `serverb` 上的 `/root/anaconda-ks.cfg` 复制到名为 `/home/student/kickstart.cfg` 的文件，以便学生可以编辑。使用 `sudo cat /root/anaconda-ks.cfg > /kickstart.cfg` 将 `/root/anaconda-ks.cfg` 的内容复制到 `/home/student/kickstart.cfg`。如果 `sudo` 提示输入用户密码，请使用 `student` 作为密码。

```
[student@serverb ~]$ sudo cat /root/anaconda-ks.cfg > ~/kickstart.cfg

[sudo] password for student: student
```

### 修改 `/home/student/kickstart.cfg`

2. 对 `/home/student/kickstart.cfg` 进行以下更改。

- 注释掉 `reboot` 命令。
- 注释掉 BaseOS 仓库的 `repo` 命令。修改 AppStream 仓库的 `repo` 命令，使其指向 `http://classroom.example.com/content/rhel8.0/x86_64/dvd/AppStream/`。仓库名称应设置为 `appstream`。
- 修改 `url` 命令，使用 `http://classroom.example.com/content/rhel8.0/x86_64/dvd/` 作为安装源。
- 注释掉 `network` 命令。
- 修改 `rootpw` 命令使其使用明文 `cleartext`，并将 `root` 密码设置为 `redhat`。
- 删除使用 `auth` 命令的行，并添加 `authselect select sssd` 行，将 `sssd` 设置为身份和认证源。
- 简化 `services` 命令，使得仅禁用 `kdump` 和 `rhsmcertd` 服务。保留 `sssd`、`rngd` 和 `chromedriver` 开启状态。
- 添加 `autopart` 命令。`part` 和 `reqpart` 命令已经被注释掉。
- 简化 `%post` 部分，使其运行一个脚本，将 `kickstarted on DATE` 追加到 `/etc/issue` 文件的末尾。`DATE` 是变量名，应由脚本使用无额外选项的命令生成。
- 简化 `%package` 部分如下：包含 `@core`、`chrony`、`dracut-nocrescue`、`firewall`、`grub2`、`kernel`、`rsync`、`tar` 和 `http` 包。确保没有安装 `plymouth` 包。

3. 验证 `kickstart.cfg` 的语法。

4. 将 `/home/student/kickstart.cfg` 文件发布 `http://serverb.example.com/ks-config/kickstart.cfg`。

5. 回到 `workstation` 系统检查你的工作。

## 评估

在 `workstation` 上运行 `installing-review grade` 脚本对本次练习进行评分。重启 `servera` 执行 `kickstart` 安装。

```
[student@workstation ~]$ installing-review grade
```

如果 `serverb` 网页共享的 `kickstart.cfg` 出现任何错误，请直接修改 `/var/www/html/ks-config/kickstart.cfg`，或通过修改 `~/kickstart.cfg` 并将其复制到 `/var/www/html/ks-config/` 来修复。

重启 `servera` 执行 `kickstart` 安装。在 GRUB 菜单中，选择 "Kickstart Red Hat Linux 8" 并按回车。

## 完成

在 `workstation` 上运行 `installing-review finish` 脚本完成本次练习。该脚本将移除练习期间在 `serverb` 上配置的 Web 服务器。

```
[student@workstation ~]$ installing-review finish
```
