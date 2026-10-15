
## 复制文件到开发站点

这将把生产服务器中的所有文件和目录复制到开发站点的文档根目录。只需确保将路径信息更改为适合你系统的内容即可。

对于多计算机 Web 周期环境，你可以为生产服务器创建 `tar` 归档，并通过 `FTP` 将其复制到开发站点。

### 设置文件权限

设置文件权限，以便 `Apache` 能够读取所有文件并执行 `CGI` 脚本。如果你有需要 `Apache` 具有写权限的目录（用于写入数据的 `CGI` 脚本），你也应该设置这些权限。完成后，启动或重启 `Apache` 以服务于开发站点。

### 验证一致性

现在，确保开发站点（通过 Web 浏览器）与生产站点完全相同。进行一些手动比较和抽查。确保脚本也能正常工作。

如果你的任何 `CGI` 脚本为你的生产服务器生成了硬编码的 URL，它们也会为你的开发站点这样做。你可以忽略这些 URL，或者修复它们使其使用 `SERVER_NAME` 环境变量的和 `SERVER_PORT` 端口地址。

## 测试 Web 周期

当一切如预期般工作时，你就成功创建了一个 Web 周期环境。现在你可以让开发人员将新内容和脚本放入开发站点并进行测试。每当新内容开发完成时，你首先应该在开发区域进行测试。测试应关注以下问题：

- 它是否实现了其目的？换句话说，新内容提供的功能是否满足你的规范？
- 新内容是否有任何副作用？例如，如果新内容实际上是一个新的 `CGI` 脚本，你应该使用 `Apache` 的脚本调试支持来监控脚本的工作方式。

## 将新站点移至生产服务器

在你满意测试结果后，避免通过停止对新内容的进一步开发而无需执行另一组功能测试。当生产站点更新时，制作你生产站点的副本并将其放置在你的预发布站点上。以下是这样做的建议：

- 确保预发布站点与生产站点完全相同。在执行手动检查以确保一切看起来和感觉相同之后，你可以将新内容和脚本移动到预发布站点并进行集成。
- 一次移动一个项目，以便你可以分阶段发现和解决问题。例如，如果你向开发系统添加了三个新的 `CGI` 脚本，请一次移动一个脚本到预发布区域。执行功能测试和站点集成测试。如果脚本通过测试，请将下一个新脚本移动到预发布区域。在你移动所有新内容之后，你可以执行站点级集成测试。仔细监控你的预发布站点日志。你是否注意到错误日志中有任何异常？如果没有，那么你就准备好对生产站点进行更新了。然而，你必须非常小心。例如，如果你在 `production` 服务器上有创建生产区域数据文件的 `CGI` 脚本，你不想用预发布区域中的数据文件覆盖这些文件。
- 更新生产站点的最佳时间是当你预计生产服务器最闲的时候。此时，你可以从生产服务器获取数据文件并将其应用于站点预发布版本的相应目录。这样可以将你的预发布站点与生产站点同步。此时，你必须快速将预发布站点转储到生产区域。这可能非常棘手，因为生产站点是实时的，你永远不知道何时会有访客访问页面或使用需要读取或写入数据文件的 `CGI` 脚本。

为了最小化切换时间（至少在单服务器设置中），你可以创建一个执行以下操作的 `shell` 脚本：

1. 将所有实时数据文件复制到预发布站点的相应区域。
2. 将你的顶层生产目录（如图 11-2 中的 `public` 目录）重命名为类似 `public.old` 的名称。
3. 将你的顶层预发布目录（如图 11-2 中的 `staging` 目录）重命名为你之前称为顶层生产目录的名称——例如，`public`。
4. 将旧的生产目录（如 `public.old`）重命名为你之前称为预发布顶层目录的名称——例如，`staging`。

这样，预发布站点只需几步即可成为生产站点，而不需要进行大量的文件复制操作。对应于图 11-2 所示环境的此类脚本示例见列表 11-1。

## 列表 11-1：`stage2production.sh` 脚本

```sh
#!/bin/sh

# Purpose: a simple shell script to copy live data files
# to staging area and to rename the staging area into a live
# production site. It also renames the old production
# area into a staging area.
#
# Copyright (c) 2001 Mohammed J. Kabir
# License: GNU Public License

# You will need to change these variables to use this script.
DATA_FILES="/www/mycompany/public/htdocs/cgi-data/*.dat";
TEMP_DIR="/www/mycompany/public.old";
PRODUCTION_DIR="/www/mycompany/public";
STAGE_DIR="/www/mycompany/staging";

# Copy the live data to the staging directory.
/bin/cp $DATA_FILES $STAGE_DIR

# Temporarily rename current production directory to TEMP_DIR
/bin/mv $PRODUCTION_DIR $TEMP_DIR

# Rename the current staging site to
# production directory
/bin/mv $STAGE_DIR $PRODUCTION_DIR

# Rename the temporary (old) production directory
# to staging directory
/bin/mv $TEMP_DIR $STAGE_DIR

# To be safe, change the current production directory's
# permission setting so that the Apache user (httpd)
# and Apache group (httpd) can read all files.
# If you use some other user and group for Apache, you
# have to modify this command according to
# your setup.
/bin/chown -R httpd:httpd $PRODUCTION_DIR

# Change the file permission so that the owner
# (httpd in this case) has read, write, and
# execute permission, the group (httpd in this case)
# has read and execute permission, and everyone no
# one else has permission to see the production
# directory files
/bin/chmod -R 750 $PRODUCTION_DIR
```
