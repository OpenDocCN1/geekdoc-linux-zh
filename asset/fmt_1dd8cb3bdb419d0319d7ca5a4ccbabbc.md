
为用户密码设置有效期限制。

## Linux 系统信息

```bash
pwck
```
检查 `/etc/passwd` 文件的格式正确性以及用户是否存在。

```bash
grpck
```
检查 `/etc/group` 文件的格式正确性以及组是否存在。

```bash
newgroup group_name
```
注册新组，以更改新创建文件的默认组。

## 4.8. 文件权限 (+ = 添加权限和 - = 移除权限)

```bash
ls -lh
```
显示权限。

```bash
ls /tmp | pr -T -W$COLUMNS
```
将终端分为 5 列。

```bash
chmod ugo+rwx directory1
```
为目录 `file1` 的所有者 `u`、组 `g` 和其他 `o` 设置读 `r`、写 `w` 和执行 `x` 权限。

```bash
chmod go-rwx directory1
```
移除目录 `file1` 组 `g` 和其他 `o` 的读 `r`、写 `w` 和执行 `x` 权限。

```bash
chown user1 file1
```
更改文件所有者。

```bash
chown -R user1 directory1
```
更改目录及其包含的所有文件和目录的所有者。

```bash
chgrp group1 file1
```
更改组。

```bash
chown user1 file1
```
更改所有权。

```bash
find / -perm -u+s
```
查看所有配置了 SUID 系统的文件。

```bash
chmod u+s /bin/file1
```
在二进制文件中设置 SUID。运行此文件的用户将获得与所有者相同的权限。

```bash
chmod -u+s /bin/file1
```
禁用二进制文件中的 SUID。

```bash
chmod g+s /home/public
```
在目录上设置 SGID 位 - 类似于 SUID，但针对目录。

```bash
chmod -g-s /home/public
```
关闭目录上的 SGID 位。

```bash
chmod o+t /home/public
```
在目录上设置 STICKY（粘滞位）。仅允许合法所有者删除文件。

```bash
chmod -o-t /home/public
```
关闭目录上的 STICKY 位。

## 1.9. 特殊文件属性 (+ = 添加和 - = 移除权限)

```bash
chattr +a file1
```
允许通过追加模式打开文件进行记录。

```bash
chattr +c file1
```
允许文件自动压缩/解压缩。

```bash
chattr +d file1
```
确保程序在备份期间忽略删除文件的操作。

```bash
chattr +i file1
```
使文件不可更改，因此无法被删除、修改、重命名或链接。

```bash
chattr +s file1
```
允许安全地删除文件。

```bash
chattr +S file1
```
确保文件被修改时，更改将按照指定的同步模式写入。

```bash
chattr +u file1
```
允许文件被压缩。

```bash
lsattr file1
```
显示特殊属性。

## 10. 压缩文件

```bash
chattr -u file1
```
解压缩文件或允许其解压缩。

```bash
lsattr file1
```
显示特殊属性。

```bash
chattr +c file1
```
允许文件被压缩。

```bash
chattr -c file1
```
解压缩文件。

```bash
chattr +d file1
```
允许文件被压缩。

```bash
gzip -9z file1
```
压缩文件。

```bash
rpm -q -a
```
显示所有压缩包。

```bash
rpm -q - grep
```
all of with the file.

文件的所有内容。

```bash
rpm -q -i
```
关于压缩包的信息。

```bash
rpm -q -l
```
显示压缩包提供的文件列表。

```bash
rpm -q -f
```
检查哪个压缩包属于给定的文件。

```bash
rpm -q -p file.rpm -l
```
显示尚未安装的 rpm 包所提供的文件列表。

```
rpm2cpio package.rpm | cpio -extract-make-directories *bin*
```
从 rpm 包中提取可执行文件。

```
rpm -ivh /usr/src/redhat/RPMS/arch/package.rpm
```
安装从 rpm 源码构建的包。

```
rpmbuild -rebuild package_name.src.rpm
```
从源码 rpm 重新构建 rpm 包。

## 4.12. YUM 更新更新包（Red Hat, Fedora 及其衍生版）

`yum install package_name`
下载并安装一个 rpm 包。

`yum localinstall package_name.rpm`
它将安装一个 RPM 包，并尝试使用您的存储库为您解析所有的依赖关系。

`yum update package_name.rpm`
更新系统上安装的所有 rpm 包。

`yum update package_name`
升级/更新 rpm 包。

`yum remove package_name`
移除一个 rpm 包。

`yum list`
列出系统上安装的所有包。

`yum search package_name`
在 rpm 仓库中查找软件包。

`yum clean packages`
清除 rpm 缓存，删除已下载的包。

`yum clean headers`
删除系统用于解析依赖关系的所有包头文件。

`yum clean all`
移除缓存文件和包头文件。

## I.13. DEB 包（Debian, Ubuntu 及其衍生版）

`dpkg -i package.deb`
安装/更新一个 deb 包。

`dpkg -r package_name`
移除系统包中的 deb 包。

```
dpkg -l
```
显示系统上安装的所有 deb 包。

```
dpkg -l | grep httpd
```
显示所有名称为“httpd”的 deb 包。

```
dpkg -s package_name
```
关于您系统上安装的特定软件包的信息。

```
dpkg -L package_name
```
显示系统上安装的软件包所提供的文件列表。

```
dpkg -contents package.deb
```
显示尚未安装的软件包所提供的文件列表。

```
dpkg -S /bin/ping
```
检查给定文件属于哪个软件包。

## 4.14. APT 包更新器（Debian, Ubuntu 及其衍生版）

```
apt-get install package_name
```
安装/更新一个 deb 包。

```
apt-cdrom install package_name
```
从 cd-rom 安装/更新一个 deb 包。

```
apt-get update
```
更新软件包列表。

```
apt-get upgrade
```
更新所有已安装的包。

```
apt-get remove package_name
```
从系统中卸载 deb 包。

```
apt-get purge program_name
```
卸载一个系统程序。

```
apt-get check
```
检查依赖解析是否正确。

```
apt-get clean
```
清除已下载包的缓存。

```
apt-cache search searched-package
```
返回与 'packages' 系列相对应的软件包列表。

## I.15. 查看文件内容

```
cat file1
```
从第一行开始显示文件内容。

```
tac file1
```
从最后一行开始显示文件内容。

```
more file1
```
跨页显示文件内容。

`less file1`
与 `more` 命令类似，但允许您保存文件并向后移动。

`head -2 file1`
显示文件的前两行。

`tail -2 file1`
显示文件的最后两行。

`tail -f /var/log/messages`
实时显示向文件中添加的内容。

## 4.16. 文本处理

`cat file1 .. | command <> file1_in.txt_or_file1_out.txt`
