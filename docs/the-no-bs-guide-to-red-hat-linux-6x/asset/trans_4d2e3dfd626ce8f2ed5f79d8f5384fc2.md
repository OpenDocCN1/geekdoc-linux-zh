

## 冲突的文件？

如果你安装的软件包包含一个属于之前已安装软件包的文件，RPM 将会退出并打印类似以下的错误信息：

```
rpm -ivh panda-2.0-1.i386.rpm
panda    /usr/bin/fluff conflicts with file from spiff-1.0-1
error: panda-2.0-1.i386.rpm cannot be installed
```

如果你确定用 panda 软件包中的副本替换现有的 /usr/bin/fluff 文件是可以的，你可以通过在 RPM 命令行中添加 --replacefiles 标志来告诉 RPM 忽略该错误，如此示例所示：

```
rpm -ivh --replacefiles panda-2.0-1.i386.rpm
panda    #############################################
```

## 未解决的依赖关系？

如果你尝试安装一个需要其他软件包才能正常运行的软件包，RPM 将会退出并打印类似以下的错误信息：

```
rpm -ivh hotrod-1.0-1.i386.rpm
failed dependencies:
    gasoline is needed by hotrod-1.0-1
```

这种情况下，RPM 表示 hotrod 软件包要求先安装 gasoline 软件包。如果你认为 RPM 只是想破坏你的乐趣，你可以添加 --nodeps 标志，如下一个示例所示。RPM 将跳过依赖检查并继续安装软件包，但 hotrod 软件包在没有 gasoline 的情况下可能无法正常运行。

```
rpm -ivh --nodeps panda-2.0-1.i386.rpm
panda    #############################################
```

## 卸载软件包

如果磁盘空间不足，使用 RPM 卸载一个或多个软件包。卸载甚至比安装更容易，因为你只需要知道软件包名称，而不需要知道原始软件包文件的名称。以下是如何移除 dogfood 软件包的方法：

```
rpm -e dogfood
```

RPM 会告诉你如果移除该软件包是否会导致其他已安装软件包出现问题。如果会，你可能会看到类似这样的信息：

```
removing these packages would break dependencies:
dogfood is needed by fido-1.0-1
```

如果你确定自己知道在做什么，可以添加 --nodeps 标志，RPM 将跳过依赖检查并继续卸载软件包。

## 升级和刷新软件包

升级软件包与安装类似，但 RPM 会在安装新版本之前自动卸载软件包的现有版本。如果找不到旧版本的软件包，升级选项仍会安装它。 （这与刷新选项不同，后者只有在找到旧版本的软件包时才会安装。）请注意 RPM 标志区分大小写，因此升级时请确保使用大写字母“U”，如下例所示：

```
rpm -Uvh panda-2.0-1.i386.rpm
panda
########################################
```

由于 RPM 对带配置文件软件包执行智能升级，你可能会看到类似这样的信息：

```
saving /etc/panda.conf as /etc/panda.conf.rpmsave
```

RPM 表示它保存了你的原始配置文件副本并安装了新文件。你应该使用 diff 或目视检查来查找两个文件之间的任何差异，以确保你的自定义设置已应用到新版本。

## 嘿，那是降级！

如果 RPM 认为你正尝试升级到版本号更旧的软件包，你会看到类似以下的错误信息：

```
rpm -Uvh panda-2.0-1.i386.rpm
panda    package panda-3.0-1 (which is newer) is already installed
error: panda-2.0-1.i386.rpm cannot be installed
```

如果你希望 RPM 忽略此情况，可以添加 --oldpackage 标志，如此处示例所示：

```
rpm -Uvh --oldpackage panda-2.0-1.i386.rpm
panda    ########################################
```

## 与 Linux 保持新鲜

刷新软件包与升级相同，但 RPM 只有在已安装旧版本软件包时才会执行升级。请注意 RPM 标志区分大小写，因此刷新时请确保使用大写字母 "F"，如下例所示：

```
rpm -Fvh pinesol-3.2-1.i386.rpm
panda    ########################################
```

RPM 的刷新选项在你刚下载了一堆软件包，并且只想升级系统上已安装的那些软件包时特别方便。使用如下命令告诉 RPM 在当前目录中查找所有软件包文件并仅刷新之前已安装的软件包：

```
rpm -Fvh *.rpm
```

## 查询软件包

RPM 具有强大的查询功能，允许你查找系统上已安装的软件包、与软件包关联的文件，或拥有特定文件的是哪个软件包。使用 -q 标志告诉 RPM 显示已安装软件包的软件包名称、版本号和发行版号，如此示例所示：

```
rpm -q panda
panda-2.0-1
```
