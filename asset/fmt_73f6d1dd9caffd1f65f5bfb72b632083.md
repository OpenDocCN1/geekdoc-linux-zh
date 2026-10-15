
```c
    int num_options; /* 选项数量 */

    ppd_option_t *options; /* 选项 */

    int num_subgroups; /* 子组数量 */

    struct ppd_group_str *subgroups; /* 子组（最大深度 = 1） */

} ppd_group_t;
```

# ppd_option_t

`ppd_option_t` 结构体包含单个选项的选择和信息。

```c
**** Options ****

typedef struct {
    char            conflicted,      /* 如果存在冲突则为 1 */
    keyword[PPD_MAX_NAME],   /* 选项关键字名称 */
    defchoice[PPD_MAX_NAME],     /* 默认选项值 */
    text[PPD_MAX_TEXT];          /* 人可读文本 */
    ppd_ui_t        ui;            /* UI 选项类型 */
    ppd_section_t   section;       /* 命令所在区域 */
    float           order;         /* 顺序 */
    int             num_choices;   /* 选项数量 */
    ppd_choice_t   choices;      /* 选项选择 */
} ppd_option_t;
```

# ppd_profile_t

`ppd_profile_t` 结构体描述单个色彩配置。

```c
**** sRGB Color Profiles ****

typedef struct {
    char resolution[PPD_MAX_NAME], /* 分辨率或 "-" */
    media_type[PPD_MAX_NAME];      /* 媒体类型或 "-" */
    float density,                 /* 使用的墨水密度 */
    gamma,                          /* 使用的 Gamma 校正 */
    matrix[3][3];                   /* 变换矩阵 */
} ppd_profile_t;
```

# ppd_size_t

`ppd_size_t` 结构体描述单个页面尺寸。

```c
**** Page Sizes ****

typedef struct {
    int    marked;               /* 是否选择了该页面尺寸? */
    char name[PPD_MAX_NAME];      /* 媒体尺寸选项 */
    float width,                  /* 媒体宽度（点） */
    length,                        /* 媒体长度（点） */
    left,                          /* 左侧打印边距（点） */
    bottom,                        /* 下方打印边距（点） */
    right,                         /* 右侧打印边距（点） */
    top;                           /* 上方打印边距（点） */
} ppd_size_t;
```

# 附录 E

# CUPS 函数

本附录描述了 CUPS API 和 CUPS 库提供的函数。关于这些函数使用的常量和结构体的参考，请参阅附录 B、C 和 D。

## cupsAddDest()

### 用法

```c
int
cupsAddDest(const char *name,
               const char *instance,
               int num_dests,
               cups_dest_t **dests);
```

### 参数

| 参数 | 类型 | 描述 |
|---|---|---|
| name | const char * | 目标名称 |
| instance | const char * | 实例或 NULL |
| num_dests | int | 目标数量 |
| dests | cups_dest_t ** | 目标列表 |

### 返回值

新的目标数量。

### 描述

`cupsAddDest()` 函数向目标数组添加一个目标。如果该目标已存在，则不会添加。

### 示例

```c
#include <cups/cups.h>

...

int num_dests;
cups_dest_t *dests;

...
```

`num_dests = cupsAddDest("myprinter", "myinstance", num_dests, &dests);`
``` 

### 另

`cupsFreeDests()`, `cupsGetDest()`, `cupsGetDests()`, `cupsSetDests()`

## cupsAddOption()

### 用法
```c
int
cupsAddOption(const char *name,
               const char *value,
               int num_options,
               cups_option_t **options);
```

### 参数

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| name | const char * | 选项名称 |
| value | const char * | 选项值 |
| num_options | int | 数组中的选项数量 |
| options | cups_option_t ** | 指向选项数组的指针 |

### 返回值

新的选项数量。

### 描述

`cupsAddOption()` 函数向指定的数组添加一个选项。

### 示例
```c
#include <cups.h>
...
/* 声明选项数组 */
int num_options;
cups_option_t *options;

/* 初始化选项数组 */
num_options = 0;
options = (cups_option_t *)0;
```

### 第四部分 附录
```c
/* 使用 cupsAddOption() 添加选项 */
num_options = cupsAddOption("media", "letter", num_options, &options);
num_options = cupsAddOption("resolution", "300dpi", num_options, &options);
```

### 另

`cupsFreeOptions()`, `cupsGetOption()`, `cupsParseOptions()`

## cupsCancelJob()

### 用法
```c
int
cupsCancelJob(const char *dest,
    int job);
```

### 参数

| 参数 | 类型 | 描述 |
|---|---|---|
| dest | const char * | 打印机或类名 |
| job | int | 任务 ID |

### 返回值

成功返回 1，失败返回 0。失败时可以通过调用 `cupsLastError()` 找到错误。

### 描述

`cupsCancelJob()` 函数取消指定的任务。

### 示例
```c
#include <cups.h>

cupsCancelJob("LaserJet", 1);
```

### 另

`cupsLastError()`, `cupsFile()`

## cupsDoFile()

### 用法
```c
ipp_t *cupsDoFile(ipp_t *http,
    const char *resource,
    const char *filename);
```

### 参数

| 参数 | 类型 | 描述 |
| --- | --- |
| http | ipp_t * | HTTP 连接 |
| resource | const char * | 资源名称 |
| filename | const char * | 文件 |

### 返回值

IPP 响应或 NULL。

### 描述

`cupsDoFile()` 函数发送 HTTP 请求并提供 IPP 请求。

### 示例
```c
#include <cups.h>

ipp_t      http;
cups_lang_t *language;
ipp_t       *request;
...
/* 获取默认语言 */
language = cupsLangDefault();

/* 创建一个新的 IPP 请求 */
request = ippNew();

request->op.operation_id = IPP_GET_ATTRIBUTES;

/* 添加属性 */
ippAddString(request, IPP_CHARSET,
    "attributes-charset", NULL, cupsEncoding(language));

ippAddString(request, IPP_LANGUAGE,
    "attributes-natural-language", NULL,
language != NULL ? language : "C");

ippAddString(request, IPP_URI,
    "printer-uri", NULL,":hostname/resource");

/* 执行请求... */
response = cupsDoRequest(http, request, "/resource");
```

### 另

`cupsLangDefault()`, `cupsLangEncoding()`, `cupsUser()`, `httpConnect()`, `ippAddString()`, `ippNew()`

## cupsDoRequest()

### 用法
```c
ipp_t *cupsDoRequest(ipp_t *http,
    ipp_t *request,
    const char *resource);
```

### 参数

| 参数 | 类型 | 描述 |
|---|---|---|
| http | ipp_t * | HTTP 连接 |
| request | ipp_t * | IPP 请求 |
| resource | const char * | 资源名称 |

### 返回值

IPP 响应，如果请求失败则返回 NULL。失败时可以通过 `cupsLastError()` 找到错误。

### 描述

`cupsDoRequest()` 函数发送 HTTP 请求并提供 IPP 请求。它还处理请求提交。

## cupsAddRequestOptions()

### 参数

| 参数 | 类型 | 描述 |
| ---|---|---|
| request | ipp_t * | IPP 请求 |
| num_options | int | 数组中的选项数量 |
| options | cups_option_t * | 指向选项数组的指针 |

## cupsEncodeOptions()

### 用法
```c
void cupsEncodeOptions(ipp_t *request, int num_options, cups_option_t *options);
```

### 描述

`cupsEncodeOptions()` 函数将数组中的选项添加到指定的 IPP 请求中。

### 示例
```c
#include <cups/cups.h>
...
ipp_t *request;
int num_options;
cups_option_t *options;
...
cupsEncodeOptions(request, num_options, options);
```

### 另请

`cupsAddOption()`, `cupsGetOption()`, `cupsMarkOptions()`, `cupsParseOptions()`

## cupsEncryption()

### 用法
```c
http_encryption_t
cupsEncryption(void);
```

### 描述

`cupsEncryption()` 函数返回当前的默认加密模式。

### 示例
```c
#include <cups/cups.h>

printf("Default encryption = %d\n", cupsEncryption());
```

### 另请

`cupsSetEncryption()`, `httpConnectEncrypt()`, `httpEncryption()`

## cupsFreeDests()

### 用法
```c
void
cupsFreeDests(int num_dests,
cups_dest_t *dests);
```

### 参数

| 参数 | 类型 | 描述 |
|---|---|---|
| num_dests | int | 数组中的目的数量 |
| dests | cups_dest_t * | 指向数组的指针 |

### 描述

`cupsFreeDest()` 函数释放与指定目的数组相关的所有内存。

### 示例
```c
#include <cups/cups.h>

int num_dests;
cups_dest_t *dests;
...
cupsFreeDests(num_dests, dests);
```

### 另请

`cupsAddDest()`, `cupsGetDest()`, `cupsGetDests()`, `cupsSetDests()`

## cupsFreeJobs()

### 用法
```c
void cupsFreeJobs(int num_jobs, cups_job_t *jobs);
```

### 参数

| 参数 | 类型 | 描述 |
| num_jobs | int | 数组中的任务数量 |
| jobs | cups_job_t * | 指向任务数组的指针 |

### 描述

`cupsFreeJobs()` 函数释放与指定任务数组相关的所有内存。

### 示例
```c
#include <cups/cups.h>

int num_jobs;

cups_job_t *jobs;
...
cupsFreeJobs(num_jobs, jobs);
```

### 另请

`cupsGetJobs()`

## cupsFreeOptions()

### 用法
```c
void
cupsFreeOptions(int num_options,
cups_option_t *options);
```

### 参数

| 参数 | 类型 | 描述 |
| num_options | int | 数组中的选项数量 |
| options | cups_option_t * | 指向选项数组的指针 |

### 描述

`cupsFreeOptions()` 函数释放与指定选项数组相关的所有内存。

### 示例
```c
#include <cups/cups.h>
int num_options;
cups_option_t *options;
...
cupsFreeOptions(num_options, options);
```

### 另请

`cupsAddOption()`, `cupsGetOption()`, `cupsMarkOptions()`, `cupsParseOptions()`

## cupsGetClasses()

### 用法
```c
int
cupsGetClasses(char ***classes);
```

### 参数

| 参数 | 类型 | 描述 |
|---|---|---|
| classes | char *** | 指向字符指针数组指针的指针 |

### 返回

可用打印机类的数量。

### 描述

`cupsGetClasses()` 函数获取可用打印机类的列表。当不再需要时，应使用 `free()` 函数来释放返回的数组。

### 示例
```c
#include <cups/cups.h>

int i;
int num_classes;
char **classes;
...
num_classes = cupsGetClasses(
...
if (num_classes > 0)
{
    for (i = 0; i < num_classes; i ++)
free(classes[i]);

free(classes);
}
```

### 另请

`cupsGetDefault()`, `cupsGetPrinters()`

## cupsGetDefault()

### 用法
```c
const char *
cupsGetDefault(void);
```

### 返回

指向默认目的的指针。

### 描述

`cupsGetDefault()` 函数获取默认目的打印机或类。默认目的存储在静态字符串中，并在每次调用后会被重写（通常为相同的值）。

### 示例
```c
#include <cups/cups.h>

printf("The default destination is %s\n", cupsGetDefault());
```

### 另请

`cupsGetClasses()`, `cupsGetPrinters()`

## cupsGetDest()

### 用法
```c
cups_dest_t *
cupsGetDest(const char *name,
const char *instance,
int num_dests,
cups_dest_t *dests);
```

| 参数 | 类型 | 描述 |
| --- | --- | --- |
