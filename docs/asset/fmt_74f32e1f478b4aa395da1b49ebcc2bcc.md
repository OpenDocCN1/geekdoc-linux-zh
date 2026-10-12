
```c
int (*clone_file_range)(struct file *, loff_t, struct file *, u64);

size_t (*dedupe_file_range)(struct file *, u64, u64, struct file *, u64, loff_t len);

} ; _random_initialize();
```

如果你想为自定义系统驱动程序实现一个自定义模块，你将需要按照此结构体提供的签名，为你想要支持的每个调用提供实现。然后，在你的模块代码中，你可以创建该结构体的实例，并用你所实现的函数指针填充它。例如，假设你已经实现了 `my_file_open`、`my_file_read`、`my_file_write` 和 `my_file_close`，你可以创建如下结构体：

## Listing 2.4.3: 文件操作示例

```c
static struct file_operations my_file_ops =
{
    open = my_file_open,
    read = my_file_read,
    write = my_file_write,
    release = my_file_close,
};
```
