
```
Comment=Battle.net

Exec= gamemoderun wine "/home/username/.wine/drive_c/Program Files (x86)/Battle.net/Battle.net.exe" --disable-software-rasterizer

Icon=/home/username/.wine/drive_c/Program Files (x86)/Battle.net/Battle.net.png

Terminal=false

Type=Application

Categories=Utility;Game;
```

要保存进度，请点击“保存”。或者，您可以点击“文件”，然后点击“保存”，或者点击 `≡` 图标选择“另存为”，最后点击“保存”。保存后关闭编辑器。

如果仅使用 `wine-staging` 而不是其他版本，只有通过命令行启动，`Battle.net` 才会不会出现 `wine` 调试错误，这是我在 `2024/03/27` 在 `Debian 12` 和 `Linux Mint 21.3` 上遇到的情况。

另外提醒，`Battle.net` 和《魔兽》在基于 `Linux` 的操作系统（如 `Linux Mint 21.3` 和 `Debian 12`）上不受官方支持。

# LINUX MINT 21.3 命令参考

用于文件和目录管理的基础系统命令

### 列出目录内容

命令：`sudo ls directory`

描述：列出指定目录的内容。

### 切换目录

命令：`cd directory`

描述：将当前工作目录更改为指定的目录。

### 返回上一级目录

命令：`cd .. ..`

描述：将当前工作目录更改为父目录，在目录层次结构中向上移动一级。

### 列出所有非隐藏文件和文件夹

命令：`dir`

描述：列出当前工作目录下所有非隐藏的文件和文件夹。

### 列出包括隐藏在内的所有文件和

命令：`ls -a`

描述：列出当前目录下所有的文件和文件夹，包括隐藏文件。

### 创建目录

命令：`sudo mkdir directory`

描述：在当前工作目录下创建一个目录。

### 删除文件

命令：`sudo rm filename`

描述：从文件系统中删除指定的文件。

### 递归删除文件和文件夹

命令：`sudo rm -r directory`

描述：删除指定的目录及其内容，包括所有文件和子目录。

### 复制文件到目的地

命令：`sudo cp filename destination`

描述：将指定的文件复制到指定的目的地。

### 复制文件夹到目的地

命令：`sudo cp -R folder destination`

描述：将指定的文件夹及其内容复制到指定的目的地。

### 移动文件或文件夹到目的地

命令：`sudo mv filename destination`

描述：将指定的文件或文件夹移动到指定的目的地。

### 重命名文件或文件夹

命令：`sudo mv filename newfilename`

描述：将指定的文件或文件夹重命名为新名称。

### 显示文件内容

命令：`sudo cat filename`

描述：在终端显示指定文件的内容。

### 列出当前目录内容

命令：`ls ..`

描述：列出当前工作目录父目录的内容。

# 精通 APT：高级包管理技术

## 更新软件包列表

命令：`sudo apt update`

描述：通过从 `/etc/apt/sources.list.d` 文件夹下的 `sources.list` 或 `.list` 文件列出的软件源中检索最新信息，更新本地软件包数据库。

## 升级已安装的软件包

命令：`sudo apt upgrade`

描述：将所有已安装应用程序升级到仓库中的最新版本，同时处理所需的依赖关系。

## 彻底升级已安装的软件包

命令：`sudo apt full-upgrade`

描述：将系统上的所有软件包完全升级到最新可用版本。必要时可能会删除某些软件包。

### 软件包搜索

命令：`sudo apt search package`

描述：使用此命令搜索匹配指定关键词的软件包，将命令中的 `package` 替换。

### 显示软件包信息

命令：`sudo apt show package`

描述：提供关于特定软件包的详细信息。

### 安装软件包

命令：`sudo apt install package`

描述：从软件源安装软件包，包括任何所需的依赖项。

### 移除软件包

命令：`sudo apt remove package`

描述：从系统中移除软件包，但保留与其相关的任何配置文件。

### 彻底清除软件包

命令：`sudo apt purge package`

描述：从系统中移除软件包，包括其配置文件，在系统中不留任何痕迹。

### 自动移除软件包

命令：`sudo apt autoremove`

描述：从系统中移除任何未使用的软件包及其依赖项，帮助保持系统清洁。

## 列出已安装的软件包

命令：`sudo apt list`

描述：显示系统当前安装的所有软件包列表。

## 添加软件源

命令：`sudo add-apt-repository repository`

描述：向 `/etc/apt/sources.list.d` 文件夹添加新的软件存储库。

## 移除软件源

命令：`sudo add-apt-repository -r repository`

描述：从 `/etc/apt/sources.list.d` 文件夹中移除之前添加的软件源。

## 编辑源文件

命令：`sudo apt edit-sources`

描述：用默认文本编辑器打开 `sources.list` 文件，手动编辑软件源。

## 修复损坏的依赖关系

命令：`sudo apt install -f`

描述：通过安装缺失或冲突的软件包，尝试解决并修复任何损坏的软件包依赖关系。

## 获取软件包源码

命令：`sudo apt source package`

描述：从仓库下载软件包的源代码，这对于开发或调试有用。

## 升级系统

命令：`sudo do-release-upgrade`

描述：启动发行升级过程，将操作系统移动到新的发布版本。

## 清理软件包

命令：`sudo apt clean`

描述：清除本地软件包缓存，重点移除不再需要的 `.deb` 文件，以释放磁盘空间。

## 自动清理软件包

命令：`sudo apt autoclean`

描述：自动清理本地软件包缓存，移除不再需要的 `.deb` 文件，无需用户确认。

## 锁定 Apt 包

命令：`sudo apt mark-hold package`

描述：将软件包设置为锁定状态，防止在运行 `sudo apt upgrade` 时更新它。

## 解锁 Apt 包

命令：`sudo apt mark-unhold package`

描述：取消软件包的锁定，允许在运行 `sudo apt upgrade` 时对其更新。

## 显示已锁定的软件包

命令：`sudo apt-mark showhold`

描述：显示系统当前所有锁定或固定的软件包列表。

## 软件包验证

命令：`sudo apt-key verify`

描述：验证软件包源密钥的完整性和真实性，以确保下载软件包的安全。

# 精通 Flatpak：安装、管理及其他

## Flatpak 安装

命令：`flatpak install package`

描述：从远程仓库向系统安装 Flatpak。

## 列出已安装的 Flatpak

命令：`flatpak list`

描述：显示系统当前安装的所有 Flatpak 应用程序。

## 更新 Flatpak

命令：`flatpak update`

描述：将所有安装的 Flatpak 升级到最新版本，以确保其最新。

## 运行 Flatpak

命令：`flatpak run package`

描述：运行系统中安装的 Flatpak 应用程序。

## 卸载 Flatpak

命令：`flatpak uninstall package`

描述：从系统中卸载指定的 Flatpak 软件包。

## Flatpak 远程源列表

命令：`flatpak remote-list`

描述：列出已系统的 Flatpak 远程源名称。

## 添加 Flatpak 远程源

命令：`flatpak remote-add --if-not-exists name url`

描述：向系统添加新的 Flatpak 远程源，确保其不存在。

## 移除 Flatpak 远程源

命令：`flatpak remote-delete name`

描述：从配置中移除指定的 Flatpak 源。

# Snap 操作：安装、管理和探索 Snap 应用全面指南

## 安装 Snap

- 命令：`sudo snap install <snap>`
- 描述：从 `Snap Craft` 数据库安装 `snap` 应用。

## 列出已安装的 Snap

- 命令：`sudo snap list`
- 描述：列出系统上安装的 `snap`。

## 更新 Snap

- 命令：`sudo snap refresh`
- 描述：将所有 `snap` 升级到最新的可用版本。

## 运行 Snap

- 命令：`snap run <snap>`
- 描述：运行已安装的 `snap`。

## 移除 Snap

- 命令：`sudo snap remove <snap>`
- 描述：从系统中移除已安装的 `snap`。

## 搜索 Snap

- 命令：`sudo snap find <search_term>`
- 描述：在 `Snapcraft` 数据库中搜索匹配搜索术的 `snap`。

## 查看 Snap 信息

- 命令：`sudo snap info <snap>`
- 描述：提供已安装 `snap` 的详细信息，包括安装版本、发布者、许可协议和描述。

## 查看 Snap 连接

- 命令：`sudo snap connections <snap>`
- 描述：显示已安装 `snap` 创建的连接。

# 掌握文件所有权修改

### 文件所有权修改

- 命令：`sudo chown user filename`
- 描述：将文件或文件夹的所有者更改指定的用户。

### 递归修改所有权

- 命令：`sudo chown -R user filename`
- 描述：递归地将文件或文件夹及其内容的所有者更改指定的用户。

### 指定组组所有权修改

- 命令：`sudo chown user:group filename`
- 描述：同时更改文件或文件夹关联的所有者和组。

### 静默所有权修改

- 命令：`sudo chown -f user filename`
- 描述：修改所有权，如果操作未成功则抑制错误消息。

### 详细所有权修改

- 命令：`sudo chown -v user filename`
- 描述：更改所有权的同时提供有关该过程的详细信息。

### 交互式所有权修改

- 命令：`sudo chown -i user filename`
- 描述：在更改文件或文件夹所有权时请求确认。

### 保留时间戳的所有权修改

- 命令：`sudo chown --preserve-timestamps user filename`
- 描述：修改文件所有权的同时保留与文件相关的时间戳。

# 掌握文件权限：管理访问和安全设置全面指南

### 更改文件权限

- 命令：`sudo chmod permissions filename`
- 描述：修改文件或文件夹的权限以控制访问和安全设置。

### 递归更改权限

- 命令：`sudo chmod -R permissions filename`
- 描述：递归修改文件或文件夹及其内容的权限，确保访问控制的一致性。

### 使用数字更改文件权限

- 命令：`sudo chmod numbers filename`
- 描述：使用数字代码（例如 `755`）调整文件或文件夹的权限，以指定不同用户的访问权限。

### 递归更改数字权限

- 命令：`sudo chmod -R numbers filename`
- 描述：使用数字代码递归更新文件或文件夹及其子项的权限，实现精确的访问控制。

### 带详情更改权限

- 命令：`sudo chmod -v permissions filename`
- 描述：更改文件或文件夹所有权的同时提供有关所做权限变化的详细信息。

### 带确认更改权限

- 命令：`sudo chmod -i permissions filename`
- 描述：更改文件或文件夹所有权的同时，对每次单独的权限修改请求确认。

### 使用引用更改权限

- 命令：`sudo chmod --reference=reference-file filename`
- 描述：将文件或文件夹的所有权设置为与指定参考文件的权限匹配，确保访问控制设置的一致性。

# 探索 dpkg：包管理全面指南

### 安装 .deb 包

- 命令：`sudo dpkg -i file.deb`
- 描述：在您的系统上安装指定的 `.deb` 文件。

### 移除已安装的 .deb 包

- 命令：`sudo dpkg -r package_name`
- 描述：卸载已安装的 `.deb` 包并保留其配置文件。

### 移除包含文件的 .deb 包

- 命令：`sudo dpkg -P package_name`
- 描述：完全移除已安装的 `.deb` 包，包括其配置文件。

### 列出已安装包

- 命令：`sudo dpkg -l`
- 描述：列出主机上安装的所有包，以及版本和描述信息。

### 列出包安装的文件

- 命令：`sudo dpkg -L package_name`
- 描述：提供由指定包安装的文件完整列表。

### 检查包依赖关系

- 命令：`sudo dpkg -I package_name.deb`
- 描述：验证并列出 `.deb` 包所需的依赖项。

### 重配置已安装包

- 命令：`sudo dpkg-reconfigure package_name`
- 描述：允许您修改已安装包的配置设置。

### 修复损坏的安装

- 命令：`sudo dpkg --configure -a`
- 描述：通过重新配置未正确安装或配置的包来修复损坏的安装。

# 使用 wget 高效获取文件

### 下载文件

- 命令：`wget url`
- 描述：从指定的 `URL` 下载文件。

### 更改输出文件名

- 命令：`wget -o filename url`
- 描述：修改要下载的文件名。

### 后台下载文件

- 命令：`wget -b url`
- 描述：在下载文件的同时允许不中断地使用命令行。
