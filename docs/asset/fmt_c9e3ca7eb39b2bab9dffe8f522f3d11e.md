
要从 Fedora 源码目录安装源码包，请执行以下操作：

1. 参考附录 A 获取获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 `packagename` 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 `/usr/src/rpmsbuild/SOURCES` 目录。Spec 文件被复制到 `rpmbuild/SPECS`。在 Fedora 10 之前，默认路径是 `/usr/src/redhat/SOURCES` 和 `/usr/src/redhat/SPECS`。
4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```
5. 如下所示解压源码（注意你可能需要安装 `rpm-build` 包）：

```
# rpmbuild -bp packagename*.spec
```
6. 包的源码被安装到 `rpmbuild/BUILD/package`，其中 `package` 是软件包的。
7. 你现在可以对 `rpmbuild/BUILD/package` 中的文件进行更改，其中 `package` 是软件包的名字。查看 `README`、`Makefile` 以及其他文件。`rebuild` 选项用于构建。

## 安装 tar.gz 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：
1. 参考附录 A获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 `packagename` 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 `/usr/src/rpmsbuild/SOURCES` 目录。Spec 文件被复制到 `rpmbuild/SPECS`。在 Fedora 10 之前，默认路径是 `/usr/src/redhat/SOURCES` 和 `/usr/src/redhat/SPECS`。
4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```
5. 如下所示解压源码（注意你可能需要安装 `rpm-build` 包）：

```
# rpmbuild -bp packagename*.spec
```
6. 包的源码被安装到 `rpmbuild/BUILD/package`，其中 `package` 是软件包的。
7. 你现在可以对 `rpmbuild/BUILD/package` 中的文件进行更改，其中 `package` 是软件包的名字。查看 `README`、`Makefile` 以及其他文件。`rebuild` 选项用于构建。

## 安装 tar.bz2 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：
1. 参考附录 A获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 `packagename` 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 `/usr/src/rpmsbuild/SOURCES` 目录。Spec 文件被复制到 `rpmbuild/SPECS`。在 Fedora 10 之前，默认路径是 `/usr/src/redhat/SOURCES` 和 `/usr/src/redhat/SPECS`。
4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```
5. 如下所示解压源码（注意你可能需要安装 `rpm-build` 包）：

```
# rpmbuild -bp packagename*.spec
```
6. 包的源码被安装到 `rpmbuild/BUILD/package`，其中 `package` 是软件包的。
7. 你现在可以对 `rpmbuild/BUILD/package` 中的文件进行更改。

## 安装 .tgz 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：
1. 参考附录 A获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 `packagename` 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 `/usr/src/rpmsbuild/SOURCES` 目录。Spec 文件被复制到 `rpmbuild/SPECS`。在 Fedora 10 之前，默认路径是 `/usr/src/redhat/SOURCES` 和 `/usr/src/redhat/SPECS`。
4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```
5. 如下所示解压源码（注意你可能需要安装 `rpm-build` 包）：

```
# rpmbuild -bp packagename*.spec
```
6. 包的源码被安装到 `rpmbuild/BUILD/package`，其中 `package` 是软件包的。
7. 你现在可以对 `rpmbuild/BUILD/package` 中的文件进行更改。

## 安装 .gz 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：
1. 参考附录 A获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 `packagename` 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 `/usr/src/rpmsbuild/SOURCES` 目录。Spec 文件被复制到 `rpmbuild/SPECS`。在 Fedora 10 之前，默认路径是 `/usr/src/redhat/SOURCES` 和 `/usr/src/redhat/SPECS`。
4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```
5. 如下所示解压源码（注意你可能需要安装 `rpm-build` 包）：

```
# rpmbuild -bp packagename*.spec
```
6. 包的源码被安装到 `rpmbuild/BUILD/package`，其中 `package` 是软件包的。
7. 你现在可以对 `rpmbuild/BUILD/package` 中的文件进行更改。

## 安装 .tar 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：
1. 参考附录 A获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 `packagename` 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 `/usr/src/rpmsbuild/SOURCES` 目录。Spec 文件被复制到 `rpmbuild/SPECS`。在 Fedora 10 之前，默认路径是 `/usr/src/redhat/SOURCES` 和 `/usr/src/redhat/SPECS`。
4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```
5. 如下所示解压源码（注意你可能需要安装 `rpm-build` 包）：

```
# rpmbuild -bp packagename*.spec
```
6. 包的源码被安装到 `rpmbuild/BUILD/package`，其中 `package` 是软件包的。
7. 你现在可以对 `rpmbuild/BUILD/package` 中的文件进行更改。

## 安装 .tar.bz2 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：
1. 参考附录 A获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 `packagename` 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 `/usr/src/rpmsbuild/SOURCES` 目录。Spec 文件被复制到 `rpmbuild/SPECS`。在 Fedora 10 之前，默认路径是 `/usr/src/redhat/SOURCES` 和 `/usr/src/redhat/SPECS`。
4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```
5. 如下所示解压源码（注意你可能需要安装 `rpm-build` 包）：

```
# rpmbuild -bp packagename*.spec
```
6. 包的源码被安装到 `rpmbuild/BUILD/package`，其中 `package` 是软件包的。
