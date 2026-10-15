
总结提取文件和转换格式的工具。`rpm2cp` 可以 RPM 文件转换为 cpio 存档，允许非 RPM 系统的用户访问 RPM 中的文件。`alien` 实用可以在 Debian 包、RPM、Stampede 包和 tar 包之间进行任意方向的转换。这使得为一个系统设计的包变得可用。

## 复习题

- 1. 以下哪项*不是*源码包相比二进制包的优势？
    - A. 单个源码包可以在多个 CPU 架构上使用。
    - B. 通过重新编译源码包，你有时可以解决库不兼容的问题。
    - C. 你可以修改源码包中的代码，而不改变程序的行为。
    - D. 源码包的安装速度比二进制包快。
    - E. 你可能可以在 Linux 上为非 Linux 的 Unix 程序重新编译源代码。

- 2. 关于在同一台计算机上同时使用 RPM 和 Debian 包管理系统，以下哪项是正确的？
    - A. 这通常是不可接受的，因为这两个系统不共享已安装文件的数据库信息。
    - B. 这是不可能的，因为它们的已安装文件数据库相互冲突。
    - C. 如果你在每种格式中各安装一次重要库，就不会产生任何问题。
    - D. 这在 Red Hat 和 Debian 系统上是常见做法。
    - E. 同时使用这两个系统需要安装 `alien` 程序。

- 3. 关于为特定发行版构建的二进制 RPM 包，以下哪些陈述是正确的？
    - A. 许可证要求禁止在任何其他发行版上使用该包。
    - B. 只有当你将 `--convert-distrib` 参数设置为 `rpm` 时，才能在另一个基于 RPM 的发行版中使用它们。
    - C. 只有在你重新编译该包的源 RPM 后，才能在另一个基于 RPM 的发行版中使用它们。
    - D. 它们可以为运行在其他类型 CPU 上的 RPM 发行版重新编译。
    - E. 它们通常可以在相同 CPU 架构的另一个基于 RPM 的发行版上使用，但无法保证。

- 4. 管理员在基于 RPM 的 Linux 发行版上输入了以下命令：

    ```bash
    rpm -ivh megaprog.rpm
    ```

    该命令的效果是什么？
    - A. 如果计算机上已安装 `megaprog` 包，则会将其卸载。
    - B. 如果 `megaprog.rpm` 包存在且有效，且计算机上尚未安装该包，则会安装它。
    - C. `megaprog.rpm` 源码 RPM 包被编译为该计算机的二进制 RPM。
    - D. 没有任何操作；`megaprog.rpm` 不是一个有效的 RPM 文件名，因此 `rpm` 将拒绝操作此文件。
    - E. `megaprog.rpm` 包将替换计算机上已安装的该包任何早期版本。

- 5. 以下哪个命令会将 `myfonts.rpm` 文件的内容提取到当前目录？
    - A. `rpm2cpio myfonts.rpm | cpio -i --make-directories`
    - B. `rpm2cpio myfonts.rpm > make-directories`
    - C. `rpm -e myfonts.rpm`
    - D. `alien --extract myfonts.rpm`
    - E. `rpmbuild --rebuild myfonts.rpm`

- 6. 要使用 `dpkg` 删除名为 `theprogram` 的包（包括其配置文件），你应该执行以下哪个命令？
    - A. `dpkg -e theprogram`
    - B. `dpkg -p theprogram`
    - C. `dpkg -r theprogram`
    - D. `dpkg -r theprogram-1.2.3-deb`
    - E. `dpkg -P theprogram`

- 7. 以下哪项描述了 `apt-get` 和 `dpkg` 之间的区别？
    - A. `apt-get` 提供 Debian 包管理的 GUI 界面；`dpkg` 没有。
    - B. `apt-get` 除了安装 Debian 包还可以安装 tar 包（tarballs）；`dpkg` 没有。
    - C. `apt-get` 可以自动从站点检索并更新程序；`dpkg` 没有。
    - D. `apt-get` 仅提供于 Debian 发行版，但 `dpkg` 来自 Debian 及其衍生版。
    - E. `apt-get` 仅适用于基于 Debian 的发行版，但 `dpkg` 可以处理 RPM 和 Debian 包。

- 8. 在 Debian 系统上获取所有已安装包列表应该输入什么命令？
    - A. `apt-get showall`
    - B. `apt-cache showpkg`
    - C. `dpkg -r allpkgs`
    - D. `dpkg -i`
    - E. `dpkg --getselections`

- 9. 以 root 身份在 Debian 系统上输入 `apt-get update`。该命令的效果应该是？
    - A. 无效果；`update` 是 `apt-get` 的无效选项。
    - B. `APT` 工具交付你对 Internet 存储库所做的更新，允许你与他人共享更改。
    - C. `APT` 工具下载所有可用的升级并安装到你的系统中。
    - D. `APT` 工具检索有关可用软件包的信息，以便你通过 `apt-get` 安装它们。
    - E. `APT` 工具更新自身，确保你使用的是最新版本的 `APT`。

- 10. 在 Fedora 系统上，输入以下哪个命令更新 `unzip` 程序（选择所有适用项）。
    - A. `yum update unzip`
    - B. `yum upgrade unzip`
    - C. `yum -u unzip`
    - D. `yum -U unzip`
    - E. `yum check-update unzip`

- 11. 如何配置使用 Yum 访问附加存储库的系统？
    - A. 编辑 `/etc/apt/sources.list` 文件以包含存储库的 URL，详见存储库网站。
    - B. 从存储库下载包并用 RPM 安装，或将其放在 `/etc/yum.repos.d` 中。
    - C. 使用 `yum` 的 `add-repository` 子命令或 `yumext` 中的 `Add Repository` 选项传递存储库的 URL。
    - D. 编辑 `/etc/yum.conf` 文件，找到 `[repos]` 部分，在现有存储库之后添加 URL。
    - E. 编辑 `/etc/yum.conf` 文件，找到 `REPOSITORIES=` 行，将新存储库添加到该冒号分隔的列表中。

- 12. 将目录添加到所有用户的库路径的首选方法是什么？
    - A. 在全局 shell 脚本中修改 `LD_LIBRARY_PATH` 环境变量。
    - B. 将目录添加到 `/etc/ld.so.conf` 文件，然后输入 `ldconfig`。
    - C. 输入 `ldconfig /new/dir`，其中 `/new/dir` 是你想添加的目录。
    - D. 从该目录创建一个符号链接。
    - E. 输入 `ldconfig /new/dir`，其中 `/new/dir` 是你想的目录。

- 13. 你更喜欢 GTK 组件，所以想替换它们。你会做什么？
    - A. 输入 `ldconfig --substitute=qt`。
    - B. 使用 `--substitute=qt` 选项。
    - C. 使用 `--replace=qt` 选项。
    - D. 使用 `--rebuild=qt` 选项。
    - E. 使用 `--update=qt` 选项。

- 14. 用户在 `bash` 提示符输入 `kill -9`。可能的意图是什么？
    - A. 使用 TCP 断开网络连接。
    - B. 显示被杀死进程的数量。
    - C. 使系统重新加载配置。
    - D. 终止异常或挂起的进程。
    - E. 增加运行进程的优先级。

- 15. 你可能使用哪些程序来学习系统平均负载？（选择两项。）
    - A. `ld`
    - B. `load`
    - C. `top`
    - D. `uptime`
    - E. `1a`

- 16. 以下哪个命令创建进程显示，通过它们的名称显示父子关系？
    - A. `ps --forest`
    - B. `ps aux`
    - C. `ps -e`
    - D. `ps --tree`
    - E. 以上所有

- 17. 你使用 `top` 检查各种进程消耗的 CPU 时间。你发现一个进程 `dfcomp` 正在消耗系统 90% 以上的 CPU 时间。你可以得出什么结论？
    - A. 结论很少；`dfcomp` 可能在合法地消耗大量 CPU 时间，也可能是未经授权的故障程序。
    - B. 没有任何程序应该消耗 90% 的可用 CPU 时间；`dfcomp` 显然发生了故障并应该被终止。
    - C. 这是正常的；`dfcomp` 是内核的主调度进程，它消耗任何未使用的 CPU 时间。
    - D. 如果你的 CPU 性能低于 2.5GHz EM64T Pentium，则这种行为是正常的，但在新的系统中，没有程序应该消耗 90% 的 CPU 时间。
    - E. 如果你的 CPU 有至少四个核心，则这种行为是正常的，但在核心较少的系统中，没有程序应该消耗 90% 的 CPU 时间。

- 18. 你在命令提示符输入 `jobs`，得到一个没有输出的新命令提示符。你可以得出什么结论？
    - A. 你的进程的总 CPU 时间微乎其微（低于 0.1）。
    - B. 除了你使用的 shell 外，没有进程在运行。
