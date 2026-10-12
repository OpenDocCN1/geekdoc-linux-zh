
`rpm -ivh http://ftp.linux.net/pub/suse/10.0/abc.i586.rpm`

在此示例中，`-i` 选项允许安装，`-v` 选项详细输出。如果存在依赖问题，`rpm` 会提示你。否则，如果软件包已安装，则使用 `-U` 选项。

### 查询 RPM 数据库
`RPMset` 最棒的功能之一是可以获取有关已安装软件包的大量信息。查询选项（`-q`）允许你以各种方式列出名称、描述和内容。这里是一些示例：

```bash
rpm -qa xxms
rpm -ql xxms
rpm -qi xxms
```

第一个示例（`-q`）搜索 `xxms` 包并报告其当前版本。第二个 `-ql` 列出 `xxms` 包的所有文件。最后，`-qi` 显示有关软件包的描述和其他信息。

### 验证已安装的包
使用 `rpm` 验证 `RPM` 包的内容。`-V` 选项允许你检查包中的任何文件是否被篡改。这里有一个示例：

```bash
rpm -V aaa_base
.....T /etc/inittab
S.S.T /etc/profile.d/alias.ash
```
