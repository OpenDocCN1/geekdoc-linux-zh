
如果还没有安装 `cervisia` 而你想添加它，请使用你的发行版安装程序安装 KDE 软件开发包（称为 `kdesdk`）。

- 使用命令行创建你的仓库。你可以使用 `cervisia` 快速检出文件或向现有仓库添加文件，但它不是创建仓库的正确工具。

# 将文件放入你的沙箱

启动 `cervisia`，点击桌面上的“在此处”打开 `Konquer`。导航到你的工作目录（沙箱），点击工具栏最右侧砖墙图标。

`cervisia` 是一个 CVS 客户端，可与本地或远程仓库配合，并提供友好且直观的工作氛围，如图 5-1 所示。

或者，要使用 `cervisia` 创建新的沙箱，请遵循以下步骤：

1. 打开 `Konquer` 浏览器并导航到你的工作目录。
2. 从菜单栏选择“Repository: Checkout”。

CVS Checkout 对话框打开，如图 5-2 所示。

![](img/be0c8e25e9bb10f39b0d8bbb67eb22db_413_0.png)

**图 5-1：运行中的 `cervisia`。**

有关在网络上使用 `cervisia` 的更多信息，你可以在 `cervisia.sourceforge.org/net/documentation/index.html` 找到完整文档。

![](img/be0c8e25e9bb10f39b0d8bbb67eb22db_413_1.png)

**图 5-2：`cervisia` Checkout 对话框。**

# 技术 52：使用 CVS 归档更改

3. 在 `Repository` 字段中，输入你的仓库位置（如果你从本技术的开始一直跟着操作，则是 `/cvs`）。
1. 在浏览器的 `Location` 行中输入文件位置。
4. 在 `Module` 字段中输入一个 `.`（点）。
2. 右键点击你想要添加的文件，在弹出的菜单中选择“Add to Repository”。
5. 在 `Working Directory` 字段中输入你工作目录的路径。
2. 右键点击你想要添加的文件，在弹出的菜单中选择“Add to Repository”。
5. 在 `Working Directory` 字段中输入你工作目录的路径。
6. 输入日志消息并点击 `OK`。

```
cervisia checks your changes.
```

# 技术 52：使用 CVS 归档更改

![](img/be0c8e25e9bb10f39b0d8bbb67eb22db_416_0.png)

在遇到困难时，`Diff` 视图可以成为你最好的朋友。如果情况变得非常糟糕，你可以使用 `Diff` 来帮助你快速找到在修订中偏离的地方。

`Annotate`（注释）按钮会按行显示为了达到版本 `A` 所做的的更改（我们之所以称之为 `Annotate` 按钮，是因为你可以看到谁进行了某项修改）。将鼠标悬停在屏幕上会显示该行的信息，如图 52-7 所示。

![](img/be0c8e25e9bb10f39b0d8bbb67eb22db_416_1.png)

**图 52-5**：各种 CVS log 对话框。

从树中选择一个版本，信息将传输到屏幕下半部分并显示在版本 `A` 中。

**图 52-7**：各种 CVS Annotate 对话框。

现在，如果你点击另一个版本，信息将传输到版本 `B`。（左键点击选择版本 `A` 字段中的版本；中键点击选择版本 `B` 字段中的版本。）

# 使用标签标记里程碑

典型的 CVS 仓库包含许多（有时是成千上万）文件。你不太可能只更改仓库中的某一个文件。相反，令人头疼的文件经常被修改，而稳定的文件则保持不变。这意味着在任何时间点，你都会有版本为 `1.5` 的文件，有些是版本 `1.20` 的，还有少数是版本 `4.2` 的。在某些时间点，你可能想为仓库中的所有文件打标签，这样你就可以回到那个时间点，而无需自己查找版本号。标签（Tag）通常标记了一个时间点，包含了截至给定日期和时间的仓库中的所有文件。

> 如果你没有鼠标按钮，请移动到 `List`（列表）视图，并使用方向键以及 `Ctrl-A` 和 `Ctrl-B` 来选择你的版本。

从 CVS log 中，你可以使用 `Diff` 按钮显示版本之间的差异，如图 52-6 所示。

![](img/be0c8e25e9bb10f39b0d8bbb67eb22db_416_2.png)

**图 52-6**：各种 CVS Diff 对话框。

每当你达到集体修订构成一个发布版本或你所跟踪的任何内容的运行版本时，对仓库进行标记是一个好主意。

在 CVS 中，简单的标记既快又方便。要标记版本，请按照以下步骤操作：

- 高亮顶层目录（你的沙箱路径）并选择 `Advanced`（高级）> `Tag/Branch`（标签/分支）。

# 使用 CVS 分支

- 输入标签名称并点击 `OK` 按钮。

这就，呃？

当你的项目发生分支时，通常意味着你的项目一部分维护着开发路径，而另一部分向着新的方向发展。软件开发者经常创建分支。当一个分支保持维护和稳定时，另一个分支正随着剧烈的变化而增长。如果更改没有按预期运行，原始分支对用户仍然可用，你可以在需要时恢复到它。通过分支，你的项目可以在保持一条开发线的同时演变为另一个分支。

在选择标签名称时，请记住以下几点：

- 常见的命名规范是项目名后跟版本号。
- 标签名称不能包含空格或标点符号。
- 当你选择了有意义的名字时，标签最有帮助。

![](img/be0c8e25e9bb10f39b0d8bbb67eb22db_417_0.png)

在开发过程中的任何项目将发生剧烈转折的点，请使用分支或标签。这样，你就有了退路。

# 列表 53-1: CURLUPLOAD.c

```
/* * File: curlupload.c
 **    usage: curlupload <filename> <URL>
 */

#include <stdlib.h>
#include <string.h>
#include <curl/curl.h>

int main(int argc, char * argv[]) {
    CURL *curl = curl;
    FILE *srcfile = fopen(argv[1], "rb");

    if((curl = curl_easy_init()) != NULL) {
        char errorMsg[CURL_ERROR_SIZE];
        curl_easy_setopt(curl, CURLOPT_ERRORBUFFER, errorMsg);
        curl_easy_setopt(curl, CURLOPT_UPLOAD, TRUE);
        curl_easy_setopt(curl, CURLOPT_URL, argv[2]);
        curl_easy_setopt(curl, CURLOPT_READDATA, srcfile);

        if(curl_easy_perform(curl) != 0) {
            printf(stderr, "%s\n", errorMsg);
        }

        curl_easy_cleanup(curl);
    }

    return(EXIT_SUCCESS);
}
```

## 第 7 行：定义函数和类型

libcurl 函数和类型定义在 `curl.h` 头文件中，因此启用 libcurl 的程序应该包含该文件。

## 第 14 行：初始化函数

第 14 行显示了对 libcurl 初始化函数 `curl_easy_init()` 的调用。它返回一个句（handle）。

句是库用于跟踪状态的小块数据。在 libcurl 中，句处理任务的状态。在 libcurl 程序中，句以 `CURL` 指针的形式存在（见第 11 行）。

`CURL` 指针指向哪里？谁知道那是句的值——API 将任何内容放入句后面的结构中，客户端（你）无法看到数据。API 创建句，并在需要时将其交回客户端。

## 第 18–21 行：定义传输

要创建一个传输任务，使用 `curl_easy_setopt()` 来定义传输特征。每次调用 `curl_easy_setopt()` 时，你传递三个参数：

- `curl_easy_init()` 返回的句
- 你想要更改的选项符号名称
- URL 形式指定的选项的新值，并且 `curlupload` 传递第二个参数 `argv[2]`。`CURLOPT_URL` 可能是最重要且强大的传输选项。

要上传文件，必须如第 18–21 行所示设置四个传输选项。libcurl 支持完整的 URL 语法，运行时运行时可以包含主机名、用户名、密码、目录和文件名。这里有一些示例：

## 第 18 行：路由错误消息

第 18 行设置 `CURLOPT_ERRORBUFFER` 选项。该选项告诉 libcurl 在发生错误时存储错误消息的地方。使用 `CURLOPT_ERRORBUFFER` 选项时，第三个参数指定 libcurl 存储错误消息的缓冲区。文档告诉错误缓冲区长度至少为 `CURL_ERROR_SIZE` 字节（见第 16 行）。
