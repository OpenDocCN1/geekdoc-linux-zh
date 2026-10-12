
```c
static int iCMAX_I03 = { 0, };

static char *name = NULL;
```

```c
int init_module(void)
{
  int dev;

  for (dev = 0; dev < HAX_IO; ++dev) if (io[dev]) {
    /* address was passed */
  } if (name) {
    /* name was passed */
  }
}
```

调用 `insmod module io=0x300,0x308 name="test"` 会将 `io` 数组初始化为 `0x300` 和 `0x308`，并将 `name` 指针设置为传递的字符串。

## 9.5 内核守护进程（kernel daemon）

LINUX 内核 2.0 版本的新特性之一是内核守护进程。这是一个自动加载和移除模块，无需系统用户察觉。但内核守护进程是如何知道需要加载模块的？

Linux 内核与内核守护进程之间的通信通过 `IPC` 完成。内核守护进程带有新标志 `IPC_KERNEL` 打开一个消息队列。随后，内核将自动使用该队列作为内核守护进程的消息队列。为此目的，现有的 `IPC` 实现扩展了以下函数：

```c
int kerneld_send(int msgtype, int return_size, int msgsz, const char *text, const char *return_value);
```

该函数负责向内核守护进程发送消息。传输的结构如下：

```c
struct kerneld_msg {
  long mtype;
  long id;
  short version;
  short pid;
  char text[13];
};
```

`mtype` 组件包含消息；`id` 表示内核是否期望一个回答。如果 `id` 不等于 `0`，则在请求的操作完成后，内核守护进程会发送一条消息，以 `id` 的内容作为 `mtype`，并将执行命令的返回值作为新的 `id` 值。`pid` 组件持有触发请求的进程 PID。内核守护进程将此 PID 传递到环境变量 `KERNEL_TRIGGER`。加载和释放模块的责任由以下函数负责：

```c
int request_module(const char *name);
int release_module(const char *name, int wait_flag);
int delayed_module(const char *name);
int cancel_module(const char *name);
```

通过 `request_module` 内核请求加载并等待直到操作完成。`delayed_module` 标记模块带有指定的延迟。`cancel_module` 允许移除模块。

| 表 9.1 可以作为模块实现的功能单元。 |（注：除了标题和描述外，未提供表格内容） |
| :--- | :--- |
| *此处原文未提供具体表格数据，仅保留标题行* | |

如果在挂载时未找到文件系统类型，内核将执行以下代码：

```c
for (fs = file_systems; fs && strcmp(fs->name, name))
  fs = fs->next;

#ifdef CONFIG_KERNELD
if (!fs && (request_module(name) == 0)) {
  for (fs = file_systems; fs && strcmp(fs->name, name))
    fs = fs->next;
}
#endif
```
