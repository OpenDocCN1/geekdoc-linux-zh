
# 模块 4：安装软件

3. 是的，只要应用程序所依赖的与 KDE 相关的库已安装在系统上即可。但你不必*正在运行* KDE 就能使用 KDE 应用程序。同样地，只要安装了必要的库，GNOME 应用程序也可以在 KDE 下运行。

4. 在 Red Hat Linux 8.0 中用于启动图形界面的命令是 **startx**。

5. 对于每个用户，你可以修改 `~/.xinitrc` 以包含 **gnome-session** 或 **startkde** 中的任意一个。对于整个系统，请修改 `/usr/X11R6/defaults/startkde` 使其指向期望的图形界面。

6. 在 Red Hat Linux 桌面上，系统监视器（D）和终端模拟器（G）默认均不包含在内。

7. 在面板的空白处右键单击，然后选择“添加到面板”选项。可用的选项非常多！

8. GNOME 项目的主要网站是 `http://www.gnome.org`。

9. 用于获取 GNOME 主题的资源包括 `http://art.gnome.org`、`http://themes.freshmeat.net` 和 `http://www.themedepot.org`。

10. KDE 的主要网站是 `http://www.kde.org`。

11. KDE 主题可在 `www.kde-look.org`、`http://themes.freshmeat.net` 和 `http://www.themedepot.org` 上获取。

12. 在面板的空白处右键单击并选择“添加”选项。

13. Red Hat Linux 8.0 新增了 Bluecurve 主题及其各种元素：图标、背景等。

14. 对于每个用户，可以使用 `~/fonts` 作为新字体库。若要让字体在整个系统范围内可用，请改用 `/usr/share/fonts` 目录。

15. 运行 **fc-cache** 脚本并指定字体目录，以将新字体添加到系统中。

# 模块 4：安装软件

1. 要安装包，请使用 `rpm -i rpmfile`。要升级包，请使用 `rpm -U rpmfile`。要删除包，请使用 `rpm -e rpmfile`。

2. 要确定哪个包拥有 `/bin/gzip`，请使用 `rpm -qf /bin/gzip`。

3. 你可以查看 `rpm -qf /bin/gzip` 返回的包名（即 **gzip**）并运行 `rpm -e gzip`。不过，**gzip** 工具非常有用，因此不要在你关心的系统上尝试这样做。

4. 如果你确定要在 RPM 工具给出原因的情况下仍强制安装一个顽固的包，请使用 `rpm -i --force` 命令。

5. 使用 `rpm -i --test` 命令在不实际执行安装的情况下测试包的安装。

6. 正确答案是 C。`rpm -qlp bc` 命令无效，因为 `-p` 选项用于查看包文件而非已安装的包，且 `bc` 不是有效的 RPM 文件名。`rpm -ql` bc-1.0.10.i386.rpm 命令指定了一个包文件，因此需要一个 `-p` 选项，并且它不会检查已安装的包。`rpm -qa | grep "mysql"` 命令将列出所有包名中包含 "mysql" 的已安装包，但它不会列出这些包中包含的文件。

7. **redhat-config-packages** 工具是一个在两种桌面环境下都能工作的包管理器。

8. 从 Red Hat 菜单中选择“系统设置”，然后选择“软件包”，即可在不诉诸命令行的情况下运行该工具。

9. 这话说得可能太直白了，但 http://www.redhat.com 是开始的一个地方。你还可以查看 http://www.rpmfind.net、http://freshrpms.net、http://www.linuxapps.com、http://www.freshmeat.net 以及其他网站。

10. tar 包是一个单文件压缩存档，包含一个或多个（通常更多）文件和目录。**tar** 命令用于创建存档，该存档可以使用多种不同的压缩工具进行压缩。

11. Tar 包通常使用以下扩展名之一：**​.tar.gz** 或 **.tgz** 用于 gzip 压缩的 tar 存档，或 **.tar.bz2** 用于 bzip2 压缩的 tar 存档。

12. **configure** 脚本通常将 --help 参数识别为对可用选项帮助的请求，因此请使用 **./configure --help**。你也可以使用文本编辑器甚至 **more .configure** 来查看 **.configure** 文件的内容。

13. 除非你更改其权限，否则只有 root 用户可以操作 **/usr/local/src** 中的文件，这意味着你必须以 **root** 身份复制、配置和构建软件，这既不必要也不总是明智的。

14. 正确答案是 **D**。首先运行 configure 脚本，然后制作软件，安装它，最后清理。

15. 使用 **echo $PATH** 命令查看当前路径中包含哪些目录。

16. 使用 **rm -rf** 命令删除目录及其所有子目录和所有内容。它就像目录的核武器，所以要小心！

# 模块 5：管理用户

1. GID 是组 ID，是分配给每个用户组的唯一标识符。

2. UID 是用户 ID，是分配给每个用户账户的唯一数字标识符。

3. 可以在（且应当）在 Red Hat Linux 8.0 系统上安装 MD5 加密方案。

4. `/etc/shadow` 文件包含系统中的 MD5 加密密码。

5. 在配置正确的系统上，只有 root 用户可以查看 `/etc/shadow` 文件的内容。

6. 我建议向密码字段添加星号（\*）字符以禁用登录。此外，我建议添加简短的文本描述来说明密码被禁用的原因。

7. 默认用户配置文件的默认位置是 `/etc/skel`。可以更改此目录的内容，或者设置 `adduser` 命令使用另一个目录作为默认配置文件目录。

8. 使用 `groupadd -r` 命令请求下一个可用的系统组 ID。

9. 使用 `userdel -r` 命令删除账户，并从用户的主目录中移除所有由该用户拥有的文件。

10. 只有 B 是正确的；从 X 环境使用 `redhat-config-users` 命令以图形化方式管理用户和组账户。其他程序名称是我杜撰的。

11. 某些可执行文件具有权限设置，表明它们在运行时以拥有者的权限运行。如果该拥有者是 root 用户，则该文件被称为 SetUID root。

12. `sudo` 命令具有更多配置和限制选项，包括对谁可以使用它的更细粒度的控制，并且比 SetUID root 更不容易被滥用。

13. 应使用 `visudo` 命令编辑 `/etc/sudoers` 文件。虽然 `/etc/sudoers` 是一个文本文件，但 `visudo` 编辑器提供了应加以利用的安全功能。

14. 如果目录列表中某个文件的所有者用户或组显示为数字，这意味着拥有该文件的用户或组已被删除。该数字是已故用户或组的 UID 或 GID。

15. `/etc/pam.d` 目录存储每个使用 PAM 的程序的配置文件。

16. auth 模块要求用户提供密码，并传达用户和组权限。account 模块不验证用户；它根据其他因素限制或允许访问。session 模块表明登录前或登录后需要执行的操作。password 模块允许用户更改其密码。

17. requisite 模块必须成功验证用户，否则过程将立即终止并失败。required 模块必须成功验证用户，否则过程将失败。如果一个 sufficient 模块成功验证了用户，且没有其他必须处理的 required 或 sufficient 标志，则该过程成功。optional 模块即使验证用户失败也不会导致整个过程失败。

# 模块 6：命令行

1. 使用 `jobs` 命令查看会话中已启动的进程的名称和进程号。

2. 运行带有要转入前台的进程号的 `fg` 命令。

3. 匹配项为：
    - A. `command < file`
    - B. `command`
    - C. `command > file`
    - D. `command 1 | command 2`
    - E. `command 1; command 2`
    - F. `command &`

4. 由于程序文档位于手册部分 1（默认部分），你可以使用 **man passwd** 或 **man 1 passwd**。

5. 由于配置文件文档位于部分 5，请使用 **man 5 passwd** 命令。

6. 这些构成了目录列表的内容：
    - A. 普通文件是 **usage.out**。
    - B. 目录是 **routerconfig**。
    - C. 符号链接是 **a.txt**。
    - D. 块设备是 **sdb9**。
    - E. 字符设备是 **zqft2**。
    - F. 命名管道是 **flicker**。
    - G. 用户 **rwhite** 拥有 **routerconfig** 目录。
    - H. 组 **rwhite** 拥有 **usage.out** 文件。
    - I. **usage.out** 文件仅对用户 **root** 可读。
    - J. **routerconfig** 目录可以由 admin 组读取或写入。

7. 使用命令 **chown rwhite README** 和 **chgrp rwhite README**。如果你阅读 **chown** 的手册页，你会发现你也可以使用 **chown** 命令在一步中执行这两个操作：**chown rwhite.rwhite README**。

8. 使用以下值的 **chmod** 命令：**chmod 664 README**。

9. 可以使用 **find** 命令：**find /usr -name README**。

10. 以 **root** 身份使用 **tar** 命令：**tar /root/etc.tar.gz etc/**。

11. 要识别输入 **top** 时运行的可执行文件，请使用 **which top**。

12. 这样查找本地磁盘的空闲空间：**df -l**。

13. 使用带有你希望终止的进程号的 **kill -9** 命令。通常情况下，它绝对不会停止，直到进程死亡。

14. 运行 **who** 命令查看谁已登录，或运行 **w** 命令查看谁已登录以及他们正在做什么的更多信息。

15. 使用 CTRL-H 组合键在 **emacs** 中获取帮助。

16. 使用 **:help** 命令在 **vi** 中获取帮助。
