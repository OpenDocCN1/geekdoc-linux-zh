
| 条件 | 描述 |

|---|---|

| `-name` | 按名称匹配。可以使用正则表达式作为参数。 |

| `-iname` | 按名称匹配，忽略大小写。 |

| `-user` | 按所有者的用户名称或 UID 匹配。 |

| `-group` | 按所有者的组或 GID 匹配。 |

| `-size` | 按大小匹配。 |

| `-perm` | 按符号或八进制权限匹配。 |

| `-type` | 按文件类型匹配。 |

| `-newer` | 通过比较修改时间进行匹配。返回修改时间晚于参照文件的文件。 |

| `-atime` | 按天数匹配访问时间。 |

| `-mtime` | 按天数匹配修改时间。 |

| `-ctime` | 按文件最近一次状态更改的时间进行匹配。参数以天数计算。 |

## 条件的逻辑运算符

您可以使用逻辑运算符组合条件。当指定了多个标准时，默认情况下，仅返回满足所有条件的文件。但是，可以通过在条件之间使用 `-o` 来对这些条件应用逻辑运算符 OR。此外，还可以使用 `-not` 对条件取反来应用 NOT 运算符。

## 数字参数

数字参数用于指定一个数值。下表列出了大小相关的数字参数及其描述。

| 使用此参数 | 如果您需要 |

|---|---|

| `n` | 列出等于 `n` 个单位大小的文件（默认选项）。 |

| `+n` | 列出大于 `n` 个单位大小的文件。 |

| `-n` | 列出小于 `n` 个单位大小的文件。 |

下表列出了时间相关的数字参数及其描述。

| 使用此参数 | 如果您需要 |

|---|---|

| `n` | 列出在 `n` 天前被访问的文件（默认选项）。 |

| `+n` | 列出在多于 `n` 天前被访问的文件。 |

| `-n` | 列出在少于 `n` 天前被访问的文件。 |

## 如何定位文件

### 程序参考：从数据库搜索文件

要从数据库搜索文件：

1. 以 `root` 身份登录。
2. 输入 `updatedb` 使用文件名和路径信息更新 mlocate 数据库。
3. 输入 `locate {string}` 在已更新的数据库中搜索指定字符串。

### 程序参考：使用 GNOME 搜索工具搜索文件

要使用 GNOME 搜索工具搜索文件：

1. 在 GUI 中以用户身份登录。
2. 选择 **Places**（位置）→**Search for Files**（搜索文件）以打开搜索工具。
3. 在 **Search for Files**（搜索文件）窗口中，在 **Name contains**（名称包含）文本框中，键入要搜索的字符串。
4. 如有必要，从 **Look in folder**（在文件夹中查找）下拉菜单中，选择执行搜索的位置。
5. 如有必要，点击文本“Select more options”（选择更多选项）旁边的切换按钮，以指定额外的搜索标准，例如 **Date modified less than**（修改日期早于）、**Date modified more than**（修改日期晚于）、**Size at least**（大小至少）、**Size at most**（大小至多）、**File is empty**（文件为空）、**Owned by user**（所有者为用户）、**Owned by group**（所有者为组）、**Owner is unrecognized**（所有者无法识别）、**Name does not contain**（名称不包含）、**Name matches regular expression**（名称匹配正则表达式）、**Show hidden and backup files**（显示隐藏和备份文件）、**Follow symbolic links**（跟随符号链接）以及 **Include other filesystems**（包含其他文件系统）。点击 **Add**（添加）以添加选定的选项。
6. 如有必要，点击 **Help**（帮助）以查看“Search for Files”（搜索文件）的手册。
7. 点击 **Find**（查找）以搜索指定的字符串。

## 练习 4-3

### 从数据库搜索文件

**开始之前：**

1. 您已在 CLI 中以 `root` 身份登录。
2. 输入 `mv /085039Data/Managing_Packages/rhelsource /rhelsource` 移动 `/rhelsource` 目录。
3. 在终端中，输入 `cd /rhelsource/Server` 导航到 Server 目录。
4. 如有必要，输入 `rpm -ivh kernel-headers*` 安装 kernel-headers 包。
5. 输入 `clear` 清除终端屏幕。

**场景：**

您需要报告过去几年购买的所有外设，以计算进一步的需求。您希望获取组织购买的所有软件许可证的详细信息。为了定位包含此信息的文件和目录，您决定对术语“software”（软件）执行本地搜索。

## 您做什么

**您怎么做**

1. 在数据库中搜索包含单词“software”的文件名。

   a. 输入 `updatedb` 更新 mlocate 数据库。

      ![](img/477ccb2f05b6ba1b2d563ea74f18c197_178_0.png)

   b. 输入 `locate -i *software*` 搜索所有名称中包含“software”的文件。

   c. 观察到所有名称中包含“software”的文件（包括系统文件）都被列出。

2. 确保列出所有包含单词 "software" 的目录名称。

   a. 输入 `cd /` 切换到根目录。

   b. 输入 `ls -lR | grep -i "software" | more` 搜索所有包含术语 "software" 的路径名。

   c. 按 **Spacebar**（空格键）直到列表末尾，以检查是否有任何名称中包含术语 "software" 的目录。

   d. 观察到结果中显示了 `/usr/src/kernels/2.6.18-128.el5-i686/` 下的 `include/config` software 目录。

   e. 输入 `clear` 清除终端屏幕。

      ![](img/477ccb2f05b6ba1b2d563ea74f18c197_179_0.png)

   可能会显示关于符号链接的警告，并且这些消息可能会在屏幕上停留几秒钟。但是，这些警告可以忽略。

## 练习 4-4

### 在 GUI 中搜索文件

**开始之前：**

1. 您已在 CLI 中以 `root` 身份登录。
2. 在终端中，输入 `chown -R jsmith /085039Data/Locating_Files/*` 更改所有权。
3. 输入 `mkdir /work_files` 创建 `work_files` 目录。
4. 输入 `cp -pR /085039Data/Locating_Files/* /work_files` 复制文件。
5. 输入 `clear` 清除终端屏幕。

**场景：**

作为系统管理员，执行定期系统清理是您的职责。您希望清除所有不必要的空文件。您决定在 Linux 文件系统上搜索空文件并标记它们以供删除。

| 您做什么 | 您怎么做 |

| :--- | :--- |

| 1. 打开 GNOME 搜索工具。 | a. 切换到 GUI。<br> b. 以 `root` 身份登录。<br> c. 选择 **Places→Search for Files**（位置→搜索文件）以打开 GNOME 搜索工具。 |

| 2. 将搜索位置指定为 `/work_files` 目录。 | a. 在 **Search for Files**（搜索文件）窗口中，在 **Name contains**（名称包含）文本框中，键入 `*` 以将所有文件包括在搜索中。<br> b. 从 **Look in folder**（在文件夹中查找）下拉菜单中，选择 **Other**（其他）以打开 **Browse**（浏览）窗口。<br> c. 在 **Places**（位置）列表框中，双击 **File System**（文件系统）以在右侧窗格中显示更多目标目录。<br> d. 在 **Browse**（浏览）窗口中，在 **Name**（名称）列表框中，向下滚动以查看更多目录。<br> e. 在 **Name**（名称）列表框中，选择 `work_files` 并点击 **Open**（打开）以选择 `/work_files` 目录并退出窗口。 |

3. 搜索空文件。

   a. 点击文本“Select more options”（选择更多选项）旁边的切换按钮以显示更多搜索选项。
