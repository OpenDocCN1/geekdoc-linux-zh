
# 语法

`cyg_ErrNo`

```c
cyg_io_lookup(
    const char *name,
    cyg_io_handle_t *handle
);
```

- 参数：`name`，通常为 `"/dev/serial"`
- `handle`：指向设备的句柄
- 描述：在 I/O 表中查找设备。如果设备不存在，则返回 `ENOENT`。

# 语法

`cyg_ErrNo`

```c
cyg_io_write(
    cyg_io_handle_t handle,
    const void *buf,
    cyg_uint32 *len
);
```

- 参数：`handle`，句柄
- `buf`：数据缓冲区
- `len`：发送数据的大小。函数返回时，该参数包含实际发送的大小。
- 描述：向指定的设备发送数据。如果返回 `NOERR`，则表示写入成功。实际写入的字节数在 `len` 参数中。

# 语法

`_Err:`

```c
cyg_io_read(
    cyg_io_handle_t handle,
    void *buf,
    cyg_uint32 *len
);
```

- 参数：`handle`，句柄
- `buf`：用于存储数据的缓冲区
- `len`：接收数据的大小。函数返回时，该参数包含实际接收的大小。
- 描述：从指定的设备读取数据。如果返回 `NOERR`，则表示读取成功。实际读取的字节数在 `len` 参数中。

# 语法

`_Err:`

```c
cyg_io_get_config(
    cyg_io_handle_t handle,
    cyg_uint32 key,
    void *buf,
    cyg_uint32 *len
);
```

- 参数：`handle`，句柄
- `key`：要获取的信息类型。键值根据驱动程序而异，定义在 io 子目录下的 `config_keys.h` 中。
- `buf`：数据放置的位置
- `len`：要获取的数据的大小。函数返回时，该参数包含实际获取的大小。
- 描述：获取指定设备的运行时配置。信息类型由 `key` 参数指定。

# 语法

`cyg_ErrNo`

```c
cyg_io_set_config(
    cyg_io_handle_t handle,
    cyg_uint32 key,
    const void *buf,
    cyg_uint32 *len
);
```

- 参数：`handle`，句柄
- `key`：要设置的信息类型。键值根据驱动程序而异，定义在 io 子目录下的 `config_keys.h` 中。
- `buf`：用于配置设备的数据
- `len`：要设置的数据的大小。函数返回时，该参数包含实际获取的大小。
- 描述：设置指定设备的运行时配置。配置信息类型由 `key` 参数指定。

# I/O 控制系统

```c
#include <cyg/kernel/kapi.h>
#include <cyg/io/io.h>
#include <cyg/infra/diag.h>

// 应用的主启动点。
//
void cyg_user_start( void )
{
    cyg_io_handle_t tty_hdl;
    int err;
    char output_string[] = "Hello There!!\n";
    cyg_uint32 output_len = sizeof( output_string);
    err = cyg_io_lookup("/dev/tty0", &tty_hdl);
    if ( err ) {
        diag_printf("ERROR opening device tty0.\n");
        return;
    }
    err = cyg_io_write(tty_hdl, output_string, &output_len);
    if ( err ) {
        diag_printf("ERROR writing to device tty0.\n");
        return;
    }
}
```
