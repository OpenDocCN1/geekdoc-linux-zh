
```c
#include <gnome.h>

GnomeProgram *app;

app = gnome_program_init(application_id,
                          application_version,
                          module_info,
                          argc,
                          argv,
                          [property list],
                          NULL);
```

参数如下：

- `application_id` (`char *`): 标识符。标识符通常是可执行文件的名称。该字符串在 GNOME 目录树中作为应用程序特定文件的目录名。
- `application_version` (`char *`): 字符串格式的应用版本号。
- `module_info` (`GnomeModuleInfo*`): GNOME 模块标识符。最有用的值是图形应用程序的 `LIBGNOME_MODULE` 和其他程序的 `LIBGNOME_MODULE`。
- `argc` (`int`): 命令行参数计数；通常来自 `main()` 中的 `argc`。
- `argvy` (`char **`): 命令行参数；通常来自 `main()` 中的 `argvy`。

- `property list`: 键值属性列表。重要的键有：

  - `GNOME_PARAM_POPT_TABLE`: pop 库的命令行参数表（GNOME 使用 pop 解析参数）。如果你有应用程序特定的参数，可以使用 pop API 识别它们。更多信息请参阅 Johnson。
  - `GNOME_PARAM_POPT_FLAGS`: pop 的选项。
  - `GNOME_PARAM_POPT_CONTEXT`: pop 的上下文。
  - `GNOME_PARAM_ENABLE_SOUND` (`boolean`): 如果为 TRUE，应用程序可以发出声音。
  - `GNOME_PARAM_HUMAN_READABLE_NAME` (`chararray`): 应用程序的人类易读名称，即人们可能能够识别的名称。该字符串出现在菜单和其他位置。例如，“MiracleText" 可以是 miracleatext 的人类易读名称。
  - `GNOME_PARAM_SM_CONNECT` (`boolean`): 如果你想让程序忽略信号管理器，请将其设置为 FALSE。通常情况下你能够响应，因此该属性的默认值为 TRUE。

除了上述属性外，你应该在列表中指定 `GNOME_PARAM_STANDARD_PROPERTIES`。这不是真正的键；你不需要为它提供值。相反，这是一个宏，用于扩展 GNU 风格的目录标识符和位置：

- `PREFIX`: 安装路径（例如 `/opt/gnome` 或 `/usr/local`）。
- `SYSCONFDIR`: 安装文件目录（例如 `$(PREFIX)/etc`）。
- `DATADIR`: 应用程序数据目录（例如 `$(PREFIX)/share`）。
- `LIBDIR`: 库目录（例如 `$(PREFIX)/lib`）。

GNU autools（见第 6.2 节）可以设置这些宏。否则，你应该在 Makefile 中定义它们。

这里有一个简单的程序程序骨架：

```c
#include <gnome.h>

int main(int argc, char **argv)
{
    GnomeProgram *program;
    program = gnome_program_init("skeleton",
                                 "0.1",
                                 LIBGNOME_MODULE,
                                 argc, argv,
                                 GNOME_PROGRAM_STANDARD_PROPERTIES,
                                 GNOME_PARAM_HUMAN_READABLE_NAME, "Skeleton",
                                 GNOME_PARAM_ENABLE_SOUND, FALSE,
                                 NULL);
    /* 主程序的其余部分在这里 */
    gtk_main();
    exit(0);
}
```

如果没有 GNU autotools，Makefile 看起来像这样：

```make
PREFIX = /opt/gnome
CFLAGS = `pkg-config --cflags libgnomeui-2.0` -ansi -Wall \
    -DPREFIX="${PREFIX}" \
    -DDATADIR="${PREFIX}/share" \
    -DSYSCONFDIR="${PREFIX}/etc" \
    -DLIBDIR="${PREFIX}/lib"
CC = gcc
LIBS = `pkg-config --libs libgnomeui-2.0`
skeleton: skeleton.c
	$(CC) $(CFLAGS) skeleton.c -o skeleton $(LIBS)
```

`gnome_program_file_locate()` 函数是 GNOME 认可的查找配置和文件的方法，它保证了正确的路径（至少在系统安装正确的情况下）并更容易追踪问题。这是一个示例：

```c
char *path;
/* 寻找绿色苹果图像；它应该在标准的 GNOME 像素图中 */
path = gnome_program_file_locate(program,
    GNOME_FILE_DOMAIN_PIXMAP,
    "apple-green.png",
    TRUE,
    NULL);
g_print("绿色苹果: %s\n", path);
g_free(path);
```

```c
/* 查找应用程序特定的文件 - 不验证其是否存在 */
path = gnome_program_file_locate(program,
    GNOME_FILE_DOMAIN_APP_SOUND,
    "plop.wav",
    FALSE,
    NULL);
g_print("假设的 plop 音: %s\n", path);
g_free(path);
```

```c
/* 查找同一个应用程序特定的文件 - 这一次仅在文件存在时才返回路径 */
path = gnome_program_file_locate(program,
    GNOME_FILE_DOMAIN_APP_SOUND,
    "plop.wav",
    TRUE,
    NULL);
if (path) {
    g_print("... 实际位置是 %s\n", path);
    g_free(path);
} else {
    g_print(" ... plop.wav 不在那里。\n");
}
```

另一个有用的函数

`gnome_util_prepend_user_home(relative_path)`

它返回一个新分配的字符串，在 `relative_path` 之前加上用户的主目录。如果你想更进一步，指定用户 GNOME 目录 (.gnome2) 中的文件，请调用
`gnome_util_home_file(relative_path)`

一如既常，你可以自由释放返回值：

```c
/* 目录前缀函数 */
path = gnome_util_prepend_user_home("pictures/home.png");
g_print("* home.png 的路径: %s\n", path);
g_free(path);
```

# GNOME 2 官方开发者指南

```c
g_free (path);
path = gnome_util_home_file("meta-app/config");
g_print("*Path for meta-app configuration: %s\n*", path);
g_free(path);
```

你可能会调用 `gnome_util_home_file()` 的次数超过它的对应的其他函数，因为在用户的主目录中堆积非标准（有时甚至是很异）的配置文件和子目录并不是良好的做法。此外，你应该使用 `GtkConf` 来存储应用程序配置（见第 7 章）。如果你需要在路径中查找扩展名，可以使用这个命名奇特的函数：

```c
g_extension_pointer (path)
```
