

# 脚本结果

```
测试 HTML
粗体文本
斜体
```

## 10.4.2 使用 html_library 回调：加载图像和超链接

为了显示图像，`html_library` 需要一个图像部件句柄（image widget handle）。如果库尝试自己创建图像，它将需要代码来处理所有获取图像数据的方法，而且很有可能你为应用程序使用的技术将无法被支持。

为了解决这个问题，`html_library` 会调用你提供的过程（`HMset_image`）来获取图像句柄。这种技术使得库变得具有通用性。你的脚本可以使用任何必要的方法来获取图像数据：从 Web加载、从数据库中提取、将其编码到脚本中等。

处理超链接的要求也是类似的。浏览器会从远程站点下载超链接，在线超链接可以帮助加载帮助文件，而指向数据库引擎的 GUI 超链接可能会生成 SQL 查询语句。当用户点击超链接时，`html_library` 会调用用户提供的过程 `HMlink_callback` 来处理请求。

注意，你必须在定义回调过程之前加载（source）`html_library.tcl`。在 `html_library` 包中存在 `HMset_image` 和 `HMlink_callback` 的空实现版本，如果你的脚本在加载 `html_library.tcl` 脚本之前定义了这些过程，它们会被它们覆盖。

## 第 10 章 text 部件和 html_library

事件驱动 GUI 编程的要求之一是过程必须快速返回。当脚本在评估一个过程时，它并没有评估事件循环以检查用户是否点击了某个按钮（可能是取消按钮！）。特别是，如果获取图像的过程正在等待从远程站点读取数据，你甚至无法使用 update 来强制事件循环运行。因此，`html_library` 包的设计允许检索图像的过程立即返回，并在图像准备就绪时使用另一个过程。

以下流程图显示 `html_library` 遇到 `<IMG>` 标签时的控制流。注意，图像的创建需要连接到已创建的 socket 流（即 `HMset_image` 过程）。当调用 `HMset_image` 时，会将标识该图像的句柄传递给 `html_library`。当脚本调用 `HMgotimage` 时，包含了新图像的句柄。

### 语法：HMset_image
从适当的数据创建图像部件，并通过调用 `HMgotimage` 将其传回 `html_library`。
- `win`：text 部件的名称
- `src`：图像的文本描述，这是 `SRC` 字段

## 10.4 HTML 显示包

[image](img/fdcc2919568b5c6f5301d5a10d88.png)

### 语法：HMgotimage
将图像句柄映射到由数据定义的 text 部件位置中。
- `handle`：作为 `HMset_image` 参数传递的值

## 第 10 章 Widget 和 html_library
由 `create` 命令的图像句柄。在下一个示例中，`HMset_image` 调用是由硬编码创建完成的。在实际应用程序中，将使用代码解析 `src` 参数。

### 示例 10.4.2 脚本
source_library.txt

```
set list (R01GdDhkWWBAAKUAAP///r6+v19e3tF7pZ28+j60umd4GNX4Y5e
M11vdcifb1Utra5fn/5T09cvr6+zs7s0H4xh7t1lJSUSXf9/fFhYeT5kI+P
3jJyccn13IJYol4un/5T9ccZmn22ididAAAA
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAkAAkBABAk
pGA
MdGACqCHQ0YtCDGIfGKL7fKH5H94kL26uUA1NNIQ2t2+z9tICA
ZZgkCakIFeI47fLYAYAMMnoIqqcSGANIBP5N4wQO28YhmndubPP
AwpBwkII0wNIJ+jFAJBUIwgd6A5bxlQ++wkwO10JUEBMHH4ygygc/eQwcwBENMUFIFIZFF/EEJJ44zdzdtX899VV3
jjjkukuBBADAD7CHBNGLGL00t4XwGH0D3bbfwjix0qQXJAL
5dfgtIS2YEOEDARQAADL3fFB/r6gJ2YMSFCKUAMPK40B2ITX2cg
if1gl8hbYwCvc68pgGq33Y31ALcFKF880D27Y9BHHJVIQ34G1GSz26wgb
qqxenMAEYIWJS3IK13KL1A72ROC0B51ff1Q02DgYNLmB4G1GSz26wgb
nnuAKK07REZXKYP38l77RnwMC6QY4zh002K8KSI1KE1EH8FBCnI101s
t+E3gn+0QAW1NDL286mjBIU3DU35+HDF829gG6GT7WTA0XXfawMrmbaG
C3xQuz/v1O1RYYUBJMRB4H4392RFfBf311F+EbI101wV5PSH6jDA
ibEbXjnGwYjGcmT1NXRHW2mNHHAUidRp/fFBK2fVwX5fXfQ4UQjn
IACU8Euu0SBXf2LZ3gEKA44EMB2908YKAJib25NNHHO1I8Qe7zFX5ZYGIex
0nKseYCUzzZa95Vq34B11NHGEAGGKkahXkmkmInxweXKi1pplt14jnnbaomwukwt5b64gw4wkFRk5B
```

