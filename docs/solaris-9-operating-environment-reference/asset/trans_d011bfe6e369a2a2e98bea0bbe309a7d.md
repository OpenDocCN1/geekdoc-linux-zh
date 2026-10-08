

# patch

# 1023

4. 如果通过前面的步骤无法获取路径名，或者获取到的路径名不存在，patch 向标准输出写入提示信息，并从标准输入交互式请求文件名。

# 补丁应用 (Patch Application)

如果你指定了 -c、-e、-n 或 -u 选项，patch 将每个数据块（hunk）中的信息解释为差异、ed 差异或普通差异。在没有这些任何选项的情况下，patch 根据数据块内信息的格式来确定差异的类型。

对于每个数据块，patch 开始从该数据块的开头（加上应用上一个数据块时的任何偏移量）开始搜索应用补丁的位置。如果没有找到匹配数据块上下文的行，patch 将向前和向后扫描至少 1,000 字节，以寻找匹配数据块上下文的行。

如果未找到位置且为上下文差异（context difference），patch 将再次进行扫描，但忽略上下文的第一行和最后一行。如果仍然失败，则忽略上下文的前两行和后两行并再次进行扫描。不同的实现版本会更广泛地搜索安装位置。

如果找不到任何位置，patch 将该数据块发送到拒绝文件（reject file）。无论补丁文件的格式如何，被拒绝的数据块都以上下文差异格式写入。如果输入是普通或 ed 风格的差异，拒绝文件中可能包含零上下文行的差异。拒绝文件中数据块的行号可能与补丁文件中的行号不同，因为它们反映在新文件中失败数据块的大致位置，而不是旧文件。

如果补丁类型为 ed diff，实现可以通过调用 ed 命令来完成补丁。

# 示例 (Examples)

diff(1) 比较两个文本文件并创建一个包含差异的第三文件。diff 创建的输出文件包含类似于 ed(1) 命令的行。你可以通过运行 patch 命令让 file1 看起来像 file2。以下示例显示了 file1 和 file2 的内容。

```
# cat file1
bill
tom
pete
joe
mike
# cat file2
patti
bill
tom
pete
joe
mike
glenda
#
```

然后，运行 diff 将输出重定向到 file3，如下所示。
# diff file1 file2 > file3
```

diff 生成的 file3 输出所示。

# 1024

```
# cat file3
0al
> patti
5a7
> glenda
#
```

你可以对 file3 使用 patch 命令让它看起来像 file1。
# patch -i file3 file1
看起来像一个普通的 diff。
done

# 下面的示例显示了 file2 的内容。

```
# cat file1
bill
tom
pete
joe
mike
#
```

# 退出状态 (Exit Status)

- 0 成功完成。
- 1 有行或多行被写入拒绝文件。
- >1 发生错误。

# 属性 (Attributes)

请参 attributes(5) 获取以下属性的描述：

| 属性类型 | 属性值 |
|---|---|
| 可用性 | SUNWcsu |

# 相关 (See Also)

ed(1), diff(1), attributes(5), environ(5)

# pathchk — 检查路径名

# 概要 (Synopsis)

```
/usr/bin/pathchk [-p] path...
```

# 描述 (Description)

pathchk 命令检查一个或多个路径名是否有效（即它们可以用于访问或创建文件而不会导致语法错误），以及它们是否具有可移植性（即没有文件名截断）。-p 选项提供了更广泛的可移植性检查。

默认情况下，pathchk 根据底层文件系统检查每个路径操作数的每个组件。对于每个路径操作数都会写入诊断信息，其如下：

- 超过 PATH_MAX 字节。
- 其所在目录中包含任何大于 NAME_MAX 字节的组件。
- 包含在不可搜索目录中的任何组件。
- 包含任何在其目录中不有效的字符。

诊断信息的格式未指定，但它指示了检测到的错误和对应的操作数。

如果路径操作数的一个或多个组件不存在，只要可以创建匹配路径名的文件且该文件不违反任何检查，则不被视为错误。

# 选项 (Options)

- -p 根据底层文件系统对每个路径操作数检查：
- 超过 _POSIX_PATH_MAX 字节。
- 包含任何大于 _POSIX_NAME_MAX 字节的组件。
- 组件中包含任何不在可移植文件名字符集中的字符。

# 操作数 (Operands)

- path 要检查的路径。

# 用法 (Usage)

largefile(5) 描述 pathchk 遇到大于或等于 2GB 字节的行为。

# 示例 (Examples)

以下示例验证了导入数据存档中的所有路径在当前系统中是合法且无歧的。

```
pax -f archive | sed -e ' //*/s/// | xargs pathchk
if [ $ -eq 0 ];
then
    pax -r -f archive
else
    在导入文件之前调查问题。
fi
```

此示例验证了当前目录下的所有文件都可以移动到任何符合 X/Open 规范的系统。

```
find . | xargs pathchk -p
if [ $ -eq 0 ];
then
    pax -w -f archive
else
    无法创建可移植存档。
    exit 1
```

以下示例验证了用户提供的路径是一个可读文件，且应用程序可以在不覆盖现有文件的情况下扩展给定路径。

```
case $ - in
    "C*")
        reset=""
        reset="set C"
    set -C;ac
test -r "$path" && pathchk "$path.out" &&
rm "$path.out" > "$path.out"
if [ $? -ne 0 ]; then
    printf "%s not found or %s fails \n%s %s" "$0" "$path"
    reset # 在 trap 情况下重置 noclobber 选项
    # 在 EXIT 依赖它
    exit 1
fi
```

```
$reset < "$path" > "$path.out"
```

前面的示例中做了以下假设：

- 一旦 $path.out 按照预期工作，PROCESSING 将替换应用程序使用的 $path。
- noclobber 选项的状态在调用此代码时未知，应在退出时设置为调用此代码时的状态。（示例中使用 reset 变量恢复初始状态。）
- 在此处，rm "$path.out" > "$path.out" 的用法已验证 $path.out 未被截断。
- 设置了 noclobber 选项，shell 在调用 rm 之前验证 $path.out 是否已存在。
- 如果 shell 成功创建了 $path.out，它将其删除，以便应用程序可以在 PROCESSING 步骤中再次创建文件。
- 如果 PROCESSING 步骤在调用时期望文件已经存在，则将 rm "$path.out" > "$path.out" 替换为 > "$path.out"，这验证了文件不存在但保留 $path.out 供 PROCESSING 使用。

# 环境变量 (Environment Variables)

见 environ(5) 获取以下影响 pathchk 执行的环境变量描述：LC_TYPE, LC_MAGES 和 NLSPATH。

# 1056

# 退出状态 (Exit Status)

- 0 所有路径操作数通过了所有检查。
- >1 发生错误。
>0

# 属性 (Attributes)

请参 attributes(5) 获取以下属性的描述：

| 属性类型 | 属性值 |
|---|---|
| 可用性 | SUNmcu |

# 相关 (See Also)

+   pax(1), test(1), attributes(5), environ(5), largefile(5)

# pax - 可移植存档交换 (Portable Archive Interchange)

# 概要 (Synopsis)

```
/usr/bin/pax [-cdnv] [-f archive] [-s replstr]...[-pattern...]
/usr/bin/pax -r [-cdikuv] [-f archive] [-o options]...[-p string...]
[-s replstr...][-pattern...]
/usr/bin/pax -w [-dituxw@] [-b blocksize] [-a] [-f archive]
[-o options]... [-s replstr...] [-x format] [v...]
/usr/bin/pax -r -w [-dikintuxv@] [-p string]...[-s replstr...] [file...]
dory
```

新！

# 描述 (Description)

pax（portable archive exchange）命令为 POSIX 兼容系统提供了比 tar 或 cpio 命令更好的移植性。使用 pax 命令复制文件、特殊文件、需要多个磁带卷的文件系统，或你想要从 POSIX 兼容系统复制的文件。pax 命令的缺点是它不感知文件系统边界，且全路径长度不能超过 255 个字符。

# 操作模式 (Modes of Operations)

执行的操作取决于 -r（读）和 -w（写）选项的存在。-r 和 -w 的四种组合被称为四种操作模式：列表、读取、写入和复制模式，对应于概要中所示的形式。

- list (列表)

当你既未指定 -r 也未指定 -w 时，向标准输出写入从标准输入读取的存档文件中与指定模式匹配的成员名称。如果命名文件类型为目录，则也以该文件为根写入文件层次结构。

