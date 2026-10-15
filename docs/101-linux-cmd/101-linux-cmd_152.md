
# `cpio` 命令

`cpio`（输入，输出）命令是一个多功能的归档工具，可以创建和提取归档，复制文件，并处理特殊文件类型。它特别适用于系统备份、创建 `initramfs` 图像和与磁带归档一起工作。

## 语法

```sh
cpio [options] < name-list
cpio [options] -i [patterns] < archive
cpio [options] -o > archive
cpio [options] -p destination-directory
```

## 操作模式

### 1. 输出模式（`-o`）

```sh
# 从文件列表创建归档
find . -name "*.txt" | cpio -o > archive.cpio

# 创建压缩归档
find . -type f | cpio -o | gzip > archive.cpio.gz

# 详细输出
find . -name "*.conf" | cpio -ov > config_backup.cpio
```

### 2. 输入模式（`-i`）

```sh
# 提取归档
cpio -i < archive.cpio

# 提取到特定目录
cd /restore && cpio -i < /backup/archive.cpio

# 提取特定文件
cpio -i "*.txt" < archive.cpio
```

### 3. 透明模式（`-p`）

```sh
# 复制文件到另一目录
find /source -type f | cpio -p /destination

# 复制时保留属性
find /etc -name "*.conf" | cpio -pdm /backup/configs
```

## 常用选项

### 基本选项

```sh
# -o：复制输出（创建归档）
find . | cpio -o > archive.cpio

# -i：复制输入（提取归档）
cpio -i < archive.cpio

# -p：透传（复制文件）
find . | cpio -p /destination

# -v：详细输出
find . | cpio -ov > archive.cpio

# -t：列出归档内容
cpio -tv < archive.cpio
```

### 高级选项

```sh
# -d：按需创建目录
cpio -id < archive.cpio

# -m：保留修改时间
cpio -im < archive.cpio

# -u：无条件提取（覆盖）
cpio -iu < archive.cpio

# -H：指定归档格式
cpio -oH newc > archive.cpio

# -B：使用 5120 字节块
cpio -oB > archive.cpio
```

## 归档格式

### 可用格式

```sh
# 二进制格式（默认，已过时）
cpio -o > archive.cpio

# 新 ASCII 格式（推荐）
cpio -oH newc > archive.cpio

# 旧 ASCII 格式
cpio -oH odc > archive.cpio

# CRC 格式
cpio -oH crc > archive.cpio

# TAR 格式
cpio -oH tar > archive.tar

# USTAR 格式
cpio -oH ustar > archive.tar
```

## 实际示例

### 1. 系统备份

```sh
# 备份整个系统（排除特定目录）
find / -path /proc -prune -o -path /sys -prune -o -path /dev -prune -o -print | \
sudo cpio -oH newc | gzip > system_backup.cpio.gz

# 备份特定目录
find /etc /home /var -type f | cpio -oH newc > important_files.cpio

# 详细输出备份
find /home/user -type f | cpio -ovH newc > user_backup.cpio
```

### 2. 创建 initramfs

```sh
# 创建 initramfs 镜像（Linux 启动过程中的常见操作）
cd /tmp/initramfs
find . | cpio -oH newc | gzip > /boot/initramfs.img

# 提取现有 initramfs
cd /tmp/extract
zcat /boot/initramfs.img | cpio -id
```

### 3. 选择性文件操作

```sh
# 仅归档配置文件
find /etc -name "*.conf" -o -name "*.cfg" | cpio -oH newc > configs.cpio

# 归档最近 7 天修改的文件
find /home -type f -mtime -7 | cpio -oH newc > recent_files.cpio

# 归档大于 1MB 的文件
find /var/log -type f -size +1M | cpio -oH newc > large_logs.cpio
```

### 4. 与压缩归档一起工作

```sh
# 创建压缩归档
find . -type f | cpio -oH newc | gzip > archive.cpio.gz
find . -type f | cpio -oH newc | bzip2 > archive.cpio.bz2
find . -type f | cpio -oH newc | xz > archive.cpio.xz

# 提取压缩归档
zcat archive.cpio.gz | cpio -id
bzcat archive.cpio.bz2 | cpio -id
xzcat archive.cpio.xz | cpio -id
```

## 特殊文件类型

### 1. 设备文件和特殊文件

```sh
# 归档包含设备文件
find /dev -type c -o -type b | sudo cpio -oH newc > device_files.cpio

# 归档符号链接
find . -type l | cpio -oH newc > symlinks.cpio

# 归档所有文件类型并保留
find . | sudo cpio -oH newc > complete_backup.cpio
```

### 2. 保留属性

```sh
# 保留所有者和权限
find . | sudo cpio -oH newc > backup.cpio
sudo cpio -idm < backup.cpio

# 保留修改时间
cpio -im < archive.cpio

# 透传模式下保留所有属性
find /source | sudo cpio -pdm /destination
```

## 文件过滤和选择

### 1. 模式匹配

```sh
# 提取特定文件模式
cpio -i "*.txt" "*.conf" < archive.cpio

# 提取特定目录中的文件
cpio -i "etc/*" < archive.cpio

# 使用 shell 通配符提取
cpio -i "*backup*" < archive.cpio
```

### 2. 排除模式

```sh
# 创建归档时排除特定文件
find . -type f ! -name "*.tmp" ! -name "*.log" | cpio -oH newc > clean_archive.cpio

# 使用 grep 过滤
find . -type f | grep -v -E '\.(tmp|log|cache)$' | cpio -oH newc > filtered.cpio
```

## 网络操作

### 1. 远程备份

```sh
# 通过网络发送归档
find /home | cpio -oH newc | ssh user@remote "cat > backup.cpio"

# 压缩网络备份
find /data | cpio -oH newc | gzip | ssh user@remote "cat > data_backup.cpio.gz"

# 从网络接收归档
ssh user@remote "cat backup.cpio" | cpio -id
```

### 2. 磁带操作

```sh
# 写入磁带设备
find /home | cpio -oH newc > /dev/st0

# 从磁带读取
cpio -itv < /dev/st0  # 列出内容
cpio -id < /dev/st0   # 提取

# 多卷归档
find /large_dataset | cpio -oH newc --split-at=700M > /dev/st0
```

## 归档管理

### 1. 列出归档内容

```sh
# 列出归档中的所有文件
cpio -tv < archive.cpio

# 列出详细信息
cpio -itv < archive.cpio

# 统计归档中的文件数量
cpio -it < archive.cpio | wc -l

# 搜索特定文件
cpio -it < archive.cpio | grep "filename"
```

### 2. 验证归档

```sh
# 测试归档完整性
cpio -it < archive.cpio > /dev/null

# 与文件系统比较
find . | cpio -oH newc | cpio -it | sort > archive_list.txt
find . | sort > filesystem_list.txt
diff archive_list.txt filesystem_list.txt
```

### 3. 更新归档

```sh
# 追加到现有归档（不直接支持）
# 替代方法：提取，添加文件，重新创建
mkdir /tmp/archive_work
cd /tmp/archive_work
cpio -id < /path/to/archive.cpio
# 添加新文件
find . | cpio -oH newc > /path/to/new_archive.cpio
```

## 性能优化

### 1. 块大小调整

```sh
# 使用更大的块大小以获得更好的性能
cpio -oB > archive.cpio          # 5120 字节
cpio -o --block-size=32768 > archive.cpio  # 32KB 块

# 对于磁带驱动器
cpio -o --block-size=65536 > /dev/st0  # 64KB 块
```

### 2. 压缩策略

```sh
# 不同的压缩方法
find . | cpio -oH newc | gzip -1 > fast_compress.cpio.gz    # 快速
find . | cpio -oH newc | gzip -9 > best_compress.cpio.gz    # 最佳压缩比
find . | cpio -oH newc | lz4 > lz4_compress.cpio.lz4        # 非常快
find . | cpio -oH newc | xz -9 > xz_compress.cpio.xz        # 最佳压缩比
```

### 3. 并行处理

```sh
# 使用并行压缩
find . | cpio -oH newc | pigz > parallel_compressed.cpio.gz

# 并行解压缩
pigz -dc archive.cpio.gz | cpio -id
```

## 与其他工具的集成

### 1. 与 `find` 结合

```sh
# 复杂的 find 表达式
find /var/log -name "*.log" -size +10M -mtime +30 | cpio -oH newc > old_large_logs.cpio

# 在 find 期间执行命令
find . -name "*.txt" -exec grep -l "important" {} \; | cpio -oH newc > important_texts.cpio
```

### 2. 与 `rsync` 结合

```sh
# 创建增量备份
rsync -av --link-dest=/backup/previous /source/ /backup/current/
find /backup/current -type f | cpio -oH newc > incremental.cpio
```

### 3. 与 `tar` 兼容

```sh
# 将 tar 转换为 cpio
tar -cf - files | cpio -oH tar > archive.tar

# 将 cpio 转换为 tar
cpio -it < archive.cpio | tar -cf archive.tar -T -
```

## 故障排除

### 1. 常见错误

```sh
# "Premature end of file" 错误
# 检查归档是否完整或损坏
file archive.cpio

# 权限拒绝错误
# 对系统文件使用 sudo
sudo cpio -id < archive.cpio

# "Cannot create directory" 错误
# 使用 -d 选项
cpio -id < archive.cpio
```

### 2. 调试

```sh
# 详细模式用于调试
cpio -idv < archive.cpio

# 检查归档格式
file archive.cpio
hexdump -C archive.cpio | head

# 提取前测试归档
cpio -it < archive.cpio > /dev/null
echo $?  # 成功应返回 0
```

### 3. 恢复



# cpio 归档与恢复指南

本文介绍使用 `cpio` 命令进行归档创建、恢复及自动化管理的核心方法，并涵盖部分损坏归档的恢复技巧。

```sh
# Partial archive recovery
dd if=damaged_archive.cpio of=partial.cpio bs=512 count=1000
cpio -id < partial.cpio

# Skip damaged portions
cpio -id --only-verify-crc < archive.cpio
```

## 脚本和自动化

### 1. 备份脚本

```sh
#!/bin/bash
# Automated backup script
BACKUP_DIR="/backup/$(date +%Y%m%d)"
SOURCE="/home /etc /var/log"

mkdir -p "$BACKUP_DIR"
for dir in $SOURCE; do
    find "$dir" -type f | cpio -oH newc | gzip > "$BACKUP_DIR/$(basename $dir).cpio.gz"
done
```

### 2. 恢复脚本

```sh
#!/bin/bash
# Automated restoration script
ARCHIVE="$1"
DEST="${2:-/restore}"

if [ ! -f "$ARCHIVE" ]; then
    echo "Archive not found: $ARCHIVE"
    exit 1
fi

mkdir -p "$DEST"
cd "$DEST"

if [[ "$ARCHIVE" =~ \.gz$ ]]; then
    zcat "$ARCHIVE" | cpio -idm
else
    cpio -idm < "$ARCHIVE"
fi
```

## 最佳实践

### 1. 归档命名

```sh
# Use descriptive names with dates
backup_$(hostname)_$(date +%Y%m%d_%H%M%S).cpio.gz

# Include source information
home_backup_$(date +%Y%m%d).cpio
etc_configs_$(date +%Y%m%d).cpio
```

### 2. 验证

```sh
# Always verify critical archives
find /important | cpio -oH newc > critical.cpio
cpio -it < critical.cpio | wc -l
find /important | wc -l
```

### 3. 文档

```sh
# Document archive contents
cpio -itv < archive.cpio > archive_contents.txt
echo "Created: $(date)" >> archive_info.txt
echo "Source: /path/to/source" >> archive_info.txt
```

## 重要注意事项

- **选择合适的格式**：对于现代系统，使用`newc`格式
- **保留权限**：使用`-m`并以适当的用户运行
- **测试归档**：始终验证归档完整性
- **使用压缩**：与`gzip`/`bzip2`/`xz`结合以实现空间效率
- **处理特殊文件**：小心处理设备文件和符号链接
- **网络安全**：使用安全通道进行远程操作
- **备份策略**：定期备份并进行验证

`cpio`命令在创建灵活的归档和系统备份方面非常强大，尤其是在与`find`和压缩工具结合使用时。

更多详细信息，请查看手册：`man cpio`
