
在某些文件系统实现中使用 `-b` 时，保存 `.orig` 文件可能会产生意想不到的结果。在支持最大 14 个字符文件名的文件系统上，对于 12、13 或 14 字符的文件名，`.orig` 文件将覆盖新文件。

## 环境变量

参见 `environ(5)` 以获取影响 `patch` 执行的环境变量的描述：`LC_TYPE`、`LC_MESSAGES`、`LC_TIME` 和 `NLPATH`。

## 输出文件

补丁保存文件（`.orig` 后缀）和拒绝文件（`.rej` 后缀）的输出为文本文件。

## 扩展说明

补丁文件可以包含多个文件的补丁指令。当你指定 `-b` 选项时，对于每个补丁的文件，原始文件将保存在同名但附加 `.orig` 后缀的文件中。

对于每个补丁的文件，还可以如第 981 页“应用补丁”所示创建一个拒绝文件。在没有 `-r` 选项的情况下，该文件的名称通过在原始文件名后附加 `.rej` 后缀形成。

## 补丁文件格式

补丁文件必须包含零或多行头部信息，随后是一个或多个补丁。每个补丁必须包含零或多行 `diff -c` 格式的文件名识别行，以及一组或多个 `diff` 输出（通常称为块/hunks）。

`patch` 识别头部信息中的以下表达式：

`Index: pathname` 要补丁的文件名为 `pathname`。

如果补丁中的所有行（包括头文件）都以相同的起始空白字符序列开头，`patch` 会在继续之前移除该序列。在每个补丁中，如果差异类型为上下文（context），`patch` 会识别以下表达式：

`*** filename timestamp` 补丁来自 `filename`。
`-- filename timestamp` 补丁应应用于 `filename`。

补丁中的每个块（hunk）必须是更改原始文件中某行行范围的 `diff` 输出。一个补丁内连续块的行号必须升序出现。

## 文件名确定

如果你未指定操作数，`patch` 将执行以下步骤获取补丁名称：

1. 如果补丁包含字符串 `***` 和 `--`，`patch` 将从每个补丁名称的开头提取组件（取决于 `-p` 选项的存在或取值），然后测试当前目录（或用 `-d` 选项指定的目录）是否存在文件。
2. 如果两个文件都存在，`patch` 假设无法从此步骤获取补丁名称。如果头部信息包含带有 `Index:` 的行，`patch` 将从补丁名称的开头提取组件（取决于 `-p`），然后测试当前目录（或用 `-d` 选项指定的目录）中是否存在该文件。
3. 如果当前目录存在 `SCCS` 目录，`patch` 尝试执行 `get -e SCCS/filename` 以检索文件的可编辑版本。
4. 如果无法通过上述步骤获取补丁名称，或者补丁名称不存在，`patch` 将向标准输出写入提示并从标准输入交互式请求文件名。

## 应用补丁

如果你指定 `-c`、`-e` 或 `-n` 选项，`patch` 将将每个块中的信息解释为上下文差异（context difference）、`ed` 差异（ed difference）或普通差异（normal difference）。在没有这些选项之一的情况下，`patch` 根据块内信息的格式确定差异类型。

对于每个块，`patch` 开始从块开头的行号搜索应用补丁的位置，该行号加上减去应用上一个块时使用的任何偏移量。如果未找到匹配块上下文的行，`patch` 将向前和向后扫描 1,000 字节，以寻找匹配块上下文的一组行。

如果未找到此类位置且是上下文差异，`patch` 将再次进行扫描，忽略上下文的第一行和最后一行。如果仍然失败，则忽略第一行和第二行上下文并进行另一次扫描。

如果未找到位置，`patch` 将该块添加到拒绝文件中。无论补丁文件的格式如何，被拒绝的块都以上下文差异格式写入。如果输入是普通或 `ed` 风格差异，拒绝文件可以包含零上下文行的差异。拒绝文件中块的行号可能与补丁文件中的行号不同，因为它们反映了失败块在新文件近似位置，而不是旧文件。

如果补丁类型是 `ed diff`，实现可以通过调用 `ed` 命令完成补丁。

### 示例

`diff(1)` 比较两个文本文件并创建一个包含差异的第三个文本文件。由 `diff` 创建的输出文件包含类似于 `ed(1)` 命令的行。你可以通过运行 `diff` 命令生成 `file1 file2`。

以下示例显示了 `file1` 和 `file2` 的内容。

```
# cat file1

bill

tom

pete

joe

mike

# cat file2

patti

tom

pete

joe

glenda
```

```bash
else

echo Investigate problems before importing files.

exit 1

fi
```

以下示例可以将当前目录层次结构下的所有文件移动到任何符合 X/Open 规范且支持 `pax(1)` 命令的系统。

```bash
find . -print | xargs pathchk -p

if [ $? -ne 0 ]; then

    pax -w -f archive

else

    echo Portable archive cannot be created.

    exit 1

fi
```

以下示例验证了用户提供的路径是否指向一个可读文件，以及应用程序是否可以创建一个扩展给定路径的文件，而不会截断或覆盖任何现有文件。

```bash
case $1 in

    "C") reset="";

    *) reset="set +C";

esac

test -r "$path" && pathchk "$path.out" && \
rm "$path.out" > "$path.out"

if [ $? -ne 0 ]; then

    printf "%s is not found or %s fails \n" "$path" "$path"

    printf "creation errors.\n"

fi

reset # reset the noclobber option in case a trap

    # on EXIT depends on it

    exit 1

reset
```

上一个示例存在以下假设：

- `PROCESSING` 代表应用程序在验证 `$path.out` 按预期工作后使用 `$path` 的代码。
- 当调用此代码时，`noclobber` 选项的状态是未知的，它应该被设置为调用此代码时的状态。（在此处使用 `reset` 变量来恢复初始状态。）
- 注意 `rm "$path.out" > "$path.out"` 的用法。
- 在此点，`pathchk` 命令已经验证了 `$path.out` 未被截断。
- 在设置了 `noclobber` 选项的情况下，`shell` 在调用 `rm` 之前会验证 `$path.out` 是否已经存在。
- 如果 `shell` 成功创建了 `$path.out`，则 `rm` 将其删除，以便应用程序可以在 `PROCESSING` 步骤中再次创建该文件。
- 如果 `PROCESSING` 步骤在调用时期望文件已经存在，请将 `rm "$path.out" > "$path.out"` 替换为 `> "$path.out"`，这在验证文件是否已存在的同时，保留了 `$path.out` 以供 `PROCESSING` 使用。

### 环境变量

请参见 `environ(5)` 以获取影响 `paxchk` 执行的以下环境变量描述：`LC_CTYPE`、`LC_MESSAGES` 和 `NLSPATH`。

### 退出状态

- `0` 所有路径操作数都通过了检查。
- `1` 发生了错误。

### 属性

参见 `attributes(5)` 以获取以下属性的描述：

| 属性类型 | 属性值 |
|---|---|
| 可用性 | `SUNWcwsu` |

### 参见

`pax(1)`, `test(1)`, `attributes(5)`, `environ(5)`, `largefile(5)`

## pax — 可移植归档交换

### 概要

```bash
/usr/bin/pax [-f archive] [-s replstr...] [pattern...]

/usr/bin/pax [-cdnikuv] [-f archive] [-o options]...[-p string...]

 [-s replstr...] [pattern...]

/usr/bin/pax -w [-dituv] [-bblocksize] [-a] [-f archive] [-o options]...

 [-s replstr...] [-x format] [v...]

/usr/bin/pax -r -w [-dnikuv] [-p string]...[-s replstr]... [file...

directory
```
