
恰好完全相同的大小。然而，第 13 到 17 行的 `while` 循环解决了这个问题。为了防止下载时出现此问题，脚本将 `indexed_downloads` 中显示的尺寸增加了一个（虚拟）字节。

`splitter` 函数剥离字符串以移除逗号，并从范围 4-18 创建一个排序的、用空格分隔的数字字符串。你稍后可以使用这些选择数字来在 `indexed_downloads` 中查找下载。

## 拆分与暂停

列表 5 显示了一个拆分下载的函数。例如，你可以在选择 1, 2, 3, 4-10 后进行操作。在这种情况下，脚本创建从 1 到 18 的下载，然后将其发送到数组 (`1:2:3...`)。

请记住 Bash 数组从 0 开始。例如，通过查询 `indexed[4]` 来选择你需要查找的文件编号。你可以与 `indexed_downloads` 使用相同的索引来检索关联的值。

### 列表 5: 拆分函数

```
function splitter() {
  sed 's/ /\n/g' | sed -r 's/- /\([0-9]+)=\\1\/2' | sort -n
}
```

### 列表 6: 重命名函数

```bash
function rename() {
  echo $1
  for $2
  other_files=$(echo "$3")
  while read -q F "$4"; do
    filename=$(echo "$5" | sed -r 's/(.*)\([a-z]+)/\1_')
    echo "$filename"
  done
  echo "$6"
}
```

列表 6 显示了在下载时重命名文件的函数。你可能需要将 URL 的名称作为参数传递。脚本已经位于文件扩展名的根目录（例如 `/jpg/`）。Bash 使用命令行检查是否存在同名文件。如果是，脚本会在名称和文件扩展名后的点之间插入一个下划线 (`_`)。如果它包含一个下划线，则文件已重命名；如果包含两个；依此类推。

### 列表 7: 下载函数

```bash
function download() {
  name=$(basename "$1")
  suffix=$(echo "$name" | cut -d. -f2)
  if [ ! -d "$download_directory/$suffix" ] && mkdir -p "$download_directory/$suffix";
  cd "$download_directory/$suffix";
  future_name="$name_$"
  wget -O "$future_name" "$1"
}
```

列表 7 显示了下载函数。为了实现这一点，它删除了所有路径信息以及……实际文件名。脚本找到文件扩展名，如果不存在，它会创建一个目录并在运行函数后进入该目录。

### 列表 8: 下载函数

列表 8 显示了下载函数，它首先通过带有关联参数调用该函数来从下载链接中过滤出基名称。

### 列表 9: 菜单函数

```bash
function menu() {
  for i in "${indexed_downloads[@]}"; do
    local base_name="$(basename ${indexed_downloads[$i]}")"
    local size="${size[$i]}"
    echo "$size $base_name"
  done | sort -f | nl -n "$2" | cut -d: -f2 | cut -f1
}
```

列表 9 生成了一个列出可用下载的菜单。它启动一个循环遍历 `indexed_downloads` 数组，并逐行输出数组中的大小和名称。如果循环 6 中的行存在，则继续传递给 `-f cut`，`awk` 知道使用哪个文件作为程序调用。文本有一个赋值 `--free` 选项，以便 `awk` 能够感知 Bash 中确定的空空间；然后 `awk` 逐行提取文件大小和名称并按行输出。

## 格式化显示

列表 1 中的 `awk` 脚本 `cutter` 从我自定义定义的函数开始。我的第一个函数 `cutter` 通过将基本名称切分为两部分并在中间插入三个点来获取显示名称。第二个函数 `separating` 分隔行，为包含大量链接的显示页面提供清晰度。`BEGIN` 块定义格式以及表头格式。它在第一列显示大小（以 `KB`、`MB`、`GB` 为单位），第二列显示名称。如果你正在下载小文件（如壁纸、电子书或 `MP3` 文件），这将非常有用，因为仅以 `GB` 输出将毫无意义。此块还计算了所有下载的总大小，并将其输出到 `END` 块。它在行之后显示磁盘或工作目录的剩余可用空间。

# 控制

最后，列表 1 显示了控制整个程序的主函数。只要你从块（第 1 行）复制并按下 `Ctrl+C` `URL`。如果图形界面使用剪贴板（`FWWM`），你需要使用 `-selection primary` 或 `secondary` 选项来显式指定应该使用哪个剪贴板。

```
function separating_line ( lesser_equal ) {
  for ( p = 0; p <= size; p++) {
    printf "%s\t%10s\t%10s\t%12s\t%12s\t%s\n", "Download", "Kilobytes", "Megabytes", "Filename", "Gigabytes", "Disc", "free/1024\nfree/(1024/1024)," home ""
  }
}
BEGIN {
  if (length($2) > 40) {
    $2 = cutter($2)
  }
  printf "%s\t%21s\t%12s\t%12s\t%12s\t%s\n", "#", "Kilobytes", "Megabytes", "Filename", "Gigabytes", "Disc", "free/1024\nfree/(1024/1024),", $2
}
END {
  separating_line(size)
  printf "%s\t%19s\t%12s\t%12s\t%12s\n", "", "Totals", "All downloads tonight", total/1024,total/(1024)
}
```

### 列表 11: 主函数
