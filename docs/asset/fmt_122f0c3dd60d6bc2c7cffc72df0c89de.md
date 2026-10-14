
### `void gnome_vfs_uri_set_host_name(const GnomeVFSURI *uri, const gchar *hostname)`

设置 `uri` 中的主机名。

### `guint gnome_vfs_uri_get_host_path(const GnomeVFSURI *uri)`

返回 `uri` 中的端口。

### `void gnome_vfs_uri_set_host_port(const GnomeVFSURI *uri, guint port)`

设置 `uri` 中的端口。

### `const gchar *gnome_vfs_uri_get_user_name(const GnomeVFSURI *uri)`

返回 `uri` 中的用户名。

### `void gnome_vfs_uri_set_user_name(const GnomeVFSURI *uri, const gchar *user_name)`

设置 `uri` 中的用户名。

### `const gchar *gnome_vfs_uri_get_password(const GnomeVFSURI *uri)`

返回 `uri` 中的密码。

### `void gnome_vfs_uri_set_password(const GnomeVFSURI *uri, const gchar *password)`

设置 `uri` 中的密码。

### 8.8.4 URI 列表

有几个函数可以操作 URI 列表：

#### `GList *gnome_vfs_uri_list_ref(GList *uri_list)`

增加 `uri_list` 中每个 URI 的引用计数；返回指针。

#### `GList *gnome_vfs_uri_list_unref(GList *uri_list)`

减少 `uri_list` 中每个 URI 的引用计数；返回列表。

#### `GList *gnome_vfs_uri_list_copy(GList *uri_list)`

完全复制 `uri_list` 并返回副本。

#### `GList *gnome_vfs_uri_list_free(GList *uri_list)`

完全释放 `uri_list`。

## 8.9 杂工具

本节中的函数不适合本章的任何部分：

#### `char *gnome_vfs_get_local_path_from_uri(const char *uri_string)`

如果 `uri_string` 是本地文件系统上的文件，则返回包含该路径的新分配字符串。

#### `char *gnome_vfs_get_uri_from_local_path(const char *full_path)`

如果存在 `full_path`，则添加 `file://` 并返回结果作为新分配字符串。否则，此函数返回 `NULL`。

#### `gboolean gnome_vfs_is_executable_command_string(const char *command)`

如果 `command` 在当前路径（`PATH` 环境变量）中，或者 `command` 是完整的可执行路径名，则返回 `TRUE`。

#### `GnomeVFSResult gnome_vfs_get_volume_free_space(const GnomeVFSURI *uri)`

将 `uri` 空间写入 `bytes_addr`。仅当 `uri` 在本地文件系统上工作。

#### `char *gnome_vfs_uri_from_filename(const char)`

### 8.10 GnomeVFS 结果代码

本节中所有的 `GnomeVFSResult` 值如下：

- `GNOME_VFS_OK`: 操作成功。
- `GNOME_VFS_ERROR_NOT_FOUND`: 文件或目录不存在。
- `GNOME_VFS_ERROR_GENERIC`: 未定义。
- `GNOME_VFS_ERROR_INTERNAL`: 内部错误，可能存在 bug。
- `GNOME_VFS_ERROR_BAD_PARAMETERS`: 参数无效。
- `GNOME_VFS_ERROR_NOT_SUPPORTED`: 不支持的操作。
- `GNOME_VFS_ERROR_IO`: 读写时出错。
- `GNOME_VFS_ERROR_CORRUPTED_DATA`: 数据损坏。
- `GNOME_VFS_ERROR_WRONG_FORMAT`: 格式不匹配。
- `GNOME_VFS_ERROR_BAD_FILE`: 文件句柄无效。
- `GNOME_VFS_ERROR_TOO_BIG`: 文件太大。
- `GNOME_VFS_ERROR_NO_SPACE`: 文件系统空间不足。
- `GNOME_VFS_ERROR_READ_ONLY_FILE_SYSTEM`: 文件系统为只读。
- `GNOME_VFS_ERROR_INVALID_URI`: URI 格式错误。
- `GNOME_VFS_ERROR_NOT_OPEN`: 尝试访问关闭的句柄。
- `GNOME_VFS_ERROR_INVALID_OPEN_MODE`: 打开文件时模式无效。
- `GNOME_VFS_ERROR_ACCESS_DENIED`: 拒绝访问。
- `GNOME_VFS_ERROR_TOO_MANY_FILES`: 无法打开更多文件句柄。
- `GNOME_VFS_ERROR_EOF`: 访问超出文件末尾。
- `GNOME_VFS_ERROR_NOT_DIRECTORY`: 尝试将普通文件作为目录。
- `GNOME_VFS_ERROR_IN_PROGRESS`: 因为另一个操作正在挂起。
- `GNOME_VFS_ERROR_INTERRUPTED`: 访问被中断。
- `GNOME_VFS_ERROR_FILE_EXISTS`: 尝试创建已存在的文件。
- `GNOME_VFS_ERROR_LOOP`: 循环链接。
- `GNOME_VFS_ERROR_NOT_PERMITTED`: 操作不允许（例如，指定了带有危险字符的 URI）。
- `GNOME_VFS_ERROR_IS_DIRECTORY`: 尝试将目录作为普通文件。
- `GNOME_VFS_ERROR_NOT_MEMORY`: GnomeVFS 内存耗尽。
- `GNOME_VFS_ERROR_HOST_NOT_FOUND`: uri 中找不到主机。
- `GNOME_VFS_ERROR_INVALID_HOST_NAME`: URI 中的主机名无效。
- `GNOME_VFS_ERROR_HAS_NOT_ADDRESS`: 无法确定 URI 主机的地址。
- `GNOME_VFS_ERROR_LOGIN_FAILED`: 用户名或密码无效。
- `GNOME_VFS_ERROR_CANCELLED`: 用户中断了操作。
- `GNOME_VFS_ERROR_DIRECTORY_BUSY`: 尝试访问被锁定的目录。
- `GNOME_VFS_ERROR_DIRECTORY_NOT_EMPTY`: 尝试删除非空目录。
- `GNOME_VFS_ERROR_TOO_MANY_LINKS`: 尝试为单个节点创建过多的链接。
- `GNOME_VFS_ERROR_SERVICE_NOT_AVAILABLE`: 请求的服务不可用（可能尚未实现）。

# GNOME 开发者官方指南

- `GNOME_VFS_ERROR_SERVICE_OBSOLETE`: 请求的服务已过时且无法使用。
- `GNOME_VFS_ERROR_PROTOCOL_ERROR`: 网络错误。

要获取与错误代码对应的字符串，请调用：

```
gnome_vfs_result_to_string(result_code)
```

> 警告：不要尝试释放或修改此字符串。你可以直接将该函数放在 `g_printerr()` 中。如果你想操作错误消息，请使用 `g_strdup()` 复制一份。

## 8.11 移植性说明

位置值（偏移量）和文件大小随系统而异；某些平台支持非常大的文件，需要更大的整数类型。

尽管 GNOME 使用 `GNOMEVFSFileSize` 和 `GNOMEVFSOffset` 封装了大小，但你仍然可能会遇到文件大小和偏移量的问题。以下宏和函数可以帮助你编写更具移植性的代码：

- `GNOME_VFS_OFFSET_IS_LONG_LONG`: 在 GNOME–VFS 偏移量类型比 `long` 更长的系统上定义。
- `GNOME_VFS_SIZE_FORMAT_STR`: 在打印文件大小时，在 `printf()` 格式字符串中使用此宏配合 `%`。
- `GNOME_VFS_OFFSET_FORMAT_STR`: 在打印文件位置时，在 `printf()` 格式字符串中使用此宏配合 `%`。
- `gchar *gnome_vfs_format_size_for_display(GnomeVFSFileSize size)`

在一个新分配的字符串中以人类可读的形式返回大小（例如，“180 bytes”或“1.8 GB”）。

## 8.12 文件信息示例
