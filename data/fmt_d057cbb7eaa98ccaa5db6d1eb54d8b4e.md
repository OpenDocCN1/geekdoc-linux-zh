
# 第 8 章 Nagios 事件代理器接口 (Event Broker Interface)

包含此行。`void` 指针声明是一个全局作用域句柄，它最终指向模块的内存地址。它的声明是为了可以在全局上下文中引用。稍后，当你开始注册回调时（如列表 8.5 所示），你将使用此句柄来告诉事件代理器如何找到你。

## 列表 8.5 init 函数。

```c
/* 当模块被事件代理器
加载时，会调用此函数 */
int nebmodule_init(int flags, char *args, nebmodule *handle) {
    basic_module_handle = handle;
    write_to_logs_and_console("Loading FS Module...",
        NSLOG_INFO_MESSAGE,TRUE);
    neb_register_callback(NEBCALL_SERVICE_STATUS_DATA, handle,
        '1', (void *)&handle_service_status);
    write_to_logs_and_console("Done",NSLOG_INFO_MESSAGE,TRUE);
    return 0;
}
```

每个 `Neb` 模块都要求包含一个入口函数和一个退出函数。列表 8.5 是你模块的入口函数。如你所见，它返回一个 `int` 形式的退出码，并接受三个参数。第一个参数 `int flags` 旨在提供模块初始化时的上下文。第二个参数是一个名为 `args` 的字符串指针。你可以通过在 `nagios.cfg` 文件中向 `broker_module` 指令的模块名末尾添加参数，来向你的模块传递参数。例如，你的文件系统模块将其基础目录编码为 `/var/lib/nagios/status`，但你可以通过 `nagios.cfg` 中的以下定义将目录作为参数传递给模块。

```
broker module=/path/to/your/modules/fs.o \
base=/usr/lib/nagios/status
```

为了保持示例代码简单，我没有这样做；但如果将其指定为参数，我本可以在 `init` 函数中使用 `args` 指针对其进行解析。第三个参数是一个类型为 `nebmodule` 的指针，指向一个定义模块的结构体。简而言之，这是一个唯一标识我们模块内存地址的句柄。`nebmodule` 结构体定义在 `nebmodule.h` 中。如果你对模块由什么组成感兴趣，列表 8.6 包含了该定义。

# NEB 架构

## 列表 8.6 nebmodule 结构体。

```c
/* NEB 模块结构 */
struct nebmodule_struct {
    char *filename;
    char *args;
    char *info[NEBMODULE_MODINFO_NUMITEMS];
    int should_be_loaded;
    int is_currently_loaded;
};

#ifndef USE_LTDL
lt_dlhandle module_handle;
lt_ptr          init_func;
lt_ptr          deinit_func;
#else
    void *module_handle;
    void *init_func;
    void *deinit_func;
#endif

#ifndef HAVE_THREAD_H
pthread_t thread_id;
#endif

struct nebmodule_struct *next;
} nebmodule;
```

正如所说，`Nagios` 是一个巧妙的 `C` 程序。关于你自己的模块，你可以查询到许多有趣的信息。其他函数可能想知道其中一些信息。因此，在 `init` 函数中要的第一件事是使用以下代码缓存你自己内存句柄的副本。

```c
basic_module_handle = handle;
```

之后，如果需要，开始解引用关于自己的信息。例如，如果你想知道自己的线程 ID，可以这样做：

```c
pthread_t t_id=handle->thread_id
```

在你获得句柄副本后，向控制台和日志文件写入一些输出，让外界知道你还活着且运行正常。这是通过 `nagios.h` 中定义的 `write_to_logs_console` 函数实现的。该函数接受三个参数：第一个是指向消息的字符串；第二个是定义消息类型的常量（有几种常量，它们也在 `nagios.h` 中指定）；我使用的是信息性消息。最后一个参数是一个切换控制台输出的布尔值，如果为 `true`，消息将发送到控制台和日志。

## 184 第 8 章 Nagios 事件代理器接口

通过下一行向事件代理器注册以接收事件：

```c
neb_register_callback (NEBCALL_SERVICE_STATUS_DATA, handle,
'42', (void*)&handle_service_status);
```

`neb_register_callback` 函数定义在 `callbacks.h` 中。其定义如下：

```c
int neb_register_callback(int callback_type, void *mod_handle,
int priority, int (*callback_func)(void *));
```

`neb_register_callback` 接受四个参数。第一个是描述你感兴趣的事件类型的常量。第二个是句柄，当代理器需要向你发送通知时，可以使用该句柄来查找你的模块。第三个是优先级数字。通常情况下，当多个模块注册相同类型的事件时，它们将按照它们被代理器在启动时加载的顺序执行。你可以通过指定优先级数字来覆盖这一点。

`neb_register_callback` 的最后一个参数是一个函数指针，如“`C`语言中的函数引用和回调”部分所述。该函数指针必须指向一个返回 `int` 类型退出码并接受两个参数的子程序（注：原文此处与定义的 `void *` 略有出入，翻译遵循逻辑）。

最后，`neb_register_callback` 是一个句柄副本，我本在 `init` 函数中进行解析。简而言之，这是一个唯一标识我们模块内存地址的句柄。`nebmodule` 结构体定义在 `nebmodule.h` 中。如果你对模块由什么组成感兴趣，列表 8.6 包含了该定义。

正如所说，`Nagios` 是一个巧妙的 `C` 程序。关于你自己的模块，你可以查询到许多有趣的信息。其他函数可能想知道其中一些信息。因此，在 `init` 函数中要执行的第一件事是使用以下代码缓存你自己内存句柄的副本。

```c
basic_module_handle = handle;
```

之后，如果需要，开始解引用关于自己的信息。例如，如果你想知道自己的线程 ID，可以这样做：

```c
pthread_t t_id=handle->thread_id
```

在你获得句柄副本后，向控制台和日志文件写入一些输出，让外界知道你还活着且运行正常。这是通过 `nagios.h` 中定义的 `write_to_logs_console` 函数实现的。该函数接受三个参数：第一个是指向消息的字符串；第二个是定义消息类型的常量（有几种常量，它们也在 `nagios.h` 中指定）；我使用的是信息性消息。最后一个参数是一个切换控制台输出的布尔值，如果为 `true`，消息将发送到控制台和日志。

## 209 第 8 章 Nagios 事件代理器接口

## 列表 8.7 事件代理器发送数据。

```c
/* 发送数据（状态、等） */
void broker_state(int type, int flags, struct timeval *timestamp){
    nebstruct_process_data ds;
    if(!event & BROKER_STATE)
        return;
    /* 填充结构体数据 */
    ds.type=type;
    ds.flags=flags;
    ds.timestamp=get_timestamp(timestamp);
    /* 回调 */
    make_callbacks(NEBCALL_PROCESS_DATA, (void *)&);
    return;
}

/* 向代理器发送定时事件 */
void broker_timed_event(int type, int flags, struct timed_event *event, struct timeval *timestamp){
    nebstruct_timed_event_data ds;
    if(!event & BROKER_TIMED_EVENTS)
        return;
    if(event==NULL)
        return;
    /* 填充结构体数据 */
    ds.type=type;
    ds.flags=flags;
    ds.timestamp=get_timestamp(timestamp);
    ds.event_type=event->event_type;
    ds.recurring=event->recurring;
    ds.run_time=event->run_time;
    ds.event_data=event->event_data;
    /* 回调 */
    make_callbacks(NEBCALL_TIMED_EVENT_DATA, (void *)&ds);
    return;
}
```

## 186 第 8 章 Nagios 事件代理器接口

这里有一个模式。你可以看到两个函数（再次由表 8.1 中的常量定义）由代理器发送。代理器首先填充一个与要发送的事件相关的结构体 `ds`，然后在填充 `ds` 后，它使用 `make_callbacks` 函数发送事件类型常量和 `ds` 的指针。代理器对表 8.1 中的每种类型都执行相同的操作，因此空指针处理器接收代理器填充的 `ds`。这些数据特定于事件类型；例如，当代理器对定时事件模块调用回调时，`ds` 的类型是 `nebstruct_timed_event_data`。

现在看列表 8.8 中的事件函数。程序的大部分内核都在那里。

## 列表 8.8 事件函数。

```c
int handle_service_status(int neb_event_type, nebstruct_service_status_data *ds) {
    // 获取服务结构体
    service *svc = ds->object_ptr;
    // 为各种输出创建一些名称缓冲区
    char outbuf[100];
    char host_path[100];
    char service_path[100];
    // 创建带有一些日志信息的字符串
    printf(outbuf,"捕到状态码：'%i' 来自主机 '%s' 服务 %s", svc->current_state, svc->host_name,
    svc->description );
    // 写入日志
    write_to_logs_and_console(outbuf , NSLOG_INFO_MESSAGE, TRUE );
    // 创建主机和服务的路径字符串
    printf(host_path,"/usr/share/nagios/status/%s",
    svc->host_name );
    printf(service_path,"/usr/share/nagios/status/%s/%s",
    host_name, svc->description);
    // 创建目录
    (继续)
```

## NEB 架构

## 列表 8.8 event_path, S_IRWXU|S_IRGRP|S_IXGRP|S_IROTH|S_IXOTH ) (续)

```c
mkdir( host_path, S_IRWXU|S_IRGRP|S_IXGRP|S_IROTH|S_IXOTH );
//写入文件
FILE *outfile=fopen(service_path,"w");
printf(outfile,"%i:%i",svc->current_state,svc->state_type);
close(outfile);
return 0;
```

如前所述，事件处理程序通过两个参数传递：事件类型常量和一个包含特定类型信息的 `ds` 结构体的引用。
但是对于类型为 `SERVICE_STATUS` 的事件，`ds` 结构体会包含什么？让我们查看列表 8.9 中来自 `broker.c` 的相关代码段。

## 列表 8.9 broker 用于 SERVICE_STATUS_DATA 的 make_callback 代码。

```c
 /* 向 broker 发送服务更新 */
void broker_service_status(int type, int flags, int attr,
service *svc,
struct timeval *timestamp) {
nebstruct_service_status_data ds;
if(!event_broker_options & BROKER_STATUS_DATA)
return;
 /* 用相关数据填充结构体 */
ds.type=type;
ds.flags=flags;
ds.attr=attr;
ds.timestamp=get_broker_timestamp(timestamp);
ds.object_ptr=(void *)svc;
 /* 创建回调 */
neb_make_callbacks (NEBCALLBACK_SERVICE_STATUS_DATA,
(void &)&ds);
return;
}
```

首先需要注意的是以下这一行：

```c
nebstruct_service_status_data ds;
```

## 第 8 章 Nagios 事件 Broker 接口

这告诉我们事件的 `ds` 结构体类型为 `nebstruct_service_status_data`。该结构体似乎有五个元素：`type`、`flags`、`attr`、一个时间戳以及指向 `svc` 的指针，`svc` 是描述 `Nagios` 服务的结构体。查看 `nebstruct.h` (`列表 8.10`) 以获取该结构体的描述。

## 列表 8.10 nebstruct_service_status_data 结构体。

```c
```
