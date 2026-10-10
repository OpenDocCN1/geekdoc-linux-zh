

## 内部机制

诊断信息在运行时如果可用，则源自 *perldiag.pod* 文件。否则，当构建 splain 包时，这些信息可能嵌入在文件本身中。详情参见 *Makefile*。

如果检测到已存在的 `$SIG{__WARN__}` 处理程序，它将继续被遵循，但这仅发生在 *diagnostics::splainthis()* 函数（即该模块的 `$SIG{__WARN__}` 拦截器）处理完你的警告之后。

如果你迫切地想知道正在拦截哪些类型的内容，可以设置 `$diagnostics::DEBUG` 变量。

```
BEGIN { $diagnostics::DEBUG = 1 }
```

### 缺陷

无法声明“不需要诊断信息”是很烦人的，但这种情况或许并非不可克服。  
-pretty 指令调用得太晚，无法产生影响。你必须改为执行以下操作，并且要在加载模块*之前*完成。

```
BEGIN { $diagnostics::PRETTY = 1 }
```

如果我可以通过延迟编译直到需要时为止来加快启动速度，但当在 Perl 5.001e 中使用 pragma 形式时，这会导致出现“panic: top_level”错误。

虽然确实如此，但这份文档相当随意，如果你使用某个程序和 *splain*，你应该期待有一点诙谐意味。

## 作者

Tom Christiansen <>，1995年6月25日。

## SPROF

### 名称

sprof - 读取并显示共享对象配置文件数据

### 概要

sprof [选项]... shared-object-path [配置文件数据路径]

### 描述

**sprof** 命令显示作为第一个命令行参数指定的共享对象的配置文件摘要。该配置文件摘要使用之前生成的配置文件数据（位于可选的第二个命令行参数中）创建。如果省略配置文件数据路径，则 **sprof** 将尝试使用共享对象的名称推导该路径，在当前目录中查找名为 `<name>.profile` 的文件。

### 选项

以下命令行选项指定要生成的配置文件输出：

- **-c, —call-pairs**
  - 打印由共享对象导出的接口的调用路径对列表，以及每个路径被使用的次数。

- **-p, —flat-profile**
  - 生成受监控对象中所有函数的平铺配置文件，包含计数和滴答数。

- **-q, —graph**
  - 生成调用图。

如果未指定上述任何选项，则默认行为是显示平铺配置文件和调用图。

可用以下附加命令行选项：

- **-h, —help**
  - 显示命令行选项和参数的摘要并退出。

- **—usage**
  - 显示简短的使用信息并退出。

- **-V, —version**
  - 显示程序版本并退出。

### 标准

**sprof** 命令是 GNU 扩展，不存在于 POSIX.1 中。

### 示例

以下示例演示了 **sprof** 的用法。该示例由一个主程序组成，该程序调用共享库中的两个函数。首先，是主程序的代码：

```
$ cat prog.c
#include <stdio.h>
void x1(void);
void x2(void);
int main(int argc, char *argv[]) {
    x1();
    x2();
    exit(EXIT_SUCCESS);
}
```

函数 x1() 和 x2() 定义在以下源文件中，该文件用于构建共享库：

```
$ cat libdemo.c
#include <unistd.h>
void consuCpu1(int lim) {
    int j;
    for (j = 0; j < lim; j++)
        getpid();
}
void x1(void) {
    int j;
    for (j = 0; j < 100; j++)
        consuCpu1(200000);
}
void consuCpu2(int lim) {
    int j;
    for (j = 0; j < lim; j++)
        getpid();
}
void x2(void) {
    int j;
    for (j = 0; j < 1000; j++)
        consuCpu2(10000);
}
```

现在，我们将使用实际名称 **libdemo.so.1.0.1** 和 soname **libdemo.so.1** 构建共享库：

```
$ cc -g -fPIC -shared -Wl,-soname,libdemo.so.1 \
    -o libdemo.so.1.0.1 libdemo.c
```

然后，我们为库的 soname 和库链接器名称创建符号链接：

```
$ ln -sf libdemo.so.1.0.1 libdemo.so.1
$ ln -sf libdemo.so.1 libdemo.so
```

接下来，我们编译主程序，将其链接到共享库，然后列出程序的动态依赖项：

```
$ cc -g -o prog prog.c -L. -ldemo
$ ldd prog
    linux-vdso.so.1 =>  (0x00007fff86d60000)
    libdemo.so.1 => not found
    libc.so.6 => /lib64/libc.so.6 (0x00007fd4dc138000)
    /lib64/ld-linux-x86-64.so.2 (0x00007fd4dc51f000)
```

为了获取共享库的配置文件信息，我们定义环境变量 **LD_PROFILE**，值为库的 soname：

```
$ export LD_PROFILE=libdemo.so.1
```

然后，我们定义环境变量 **LD_PROFILE_OUTPUT**，值为应写入配置文件输出的目录的路径名，如果该目录尚不存在则创建该目录：

```
$ export LD_PROFILE_OUTPUT=$(pwd)/prof_data
$ mkdir -p $LD_PROFILE_OUTPUT
```

**LD_PROFILE** 会导致配置文件输出*追加*到已存在的输出文件中，因此我们确保没有预先存在的配置文件数据：

```
$ rm -f $LD_PROFILE_OUTPUT/$LD_PROFILE.profile
```

然后我们运行程序以生成配置文件输出，该输出将写入 **LD_PROFILE_OUTPUT** 中指定的目录下的文件：

```
$ LD_LIBRARY_PATH=. ./prog
$ ls prof_data
libdemo.so.1.profile
```

然后我们使用 **sprof -p** 选项生成包含计数和滴答数的平铺配置文件：

```
$ sprof -p libdemo.so.1 $LD_PROFILE_OUTPUT/libdemo.so.1.profile
Flat
profile: Each sample counts as 0.01 seconds.
% cumulative       self       self    total
               time      time      time     calls  us/call  us/call
   na      60.00   0.06   0.06       100  600.00 consuCpu1
   40.00   0.10   0.04      1000   40.00 consuCpu2
   0.00   0.10   0.00         1    0.00 x1
   0.00   0.10   0.00         1    0.00 x2
```

**sprof -q** 选项生成调用图：

```
$ sprof -q libdemo.so.1 $LD_PROFILE_OUTPUT/libdemo.so.1.profile
  index % time     self  children    called     name
  0.00 0.00         100/100 x1 [1] [0]
  100.0 0.00       100 consuCpu1 [0]
------------------------
  0.00 0.00         1/1 <UNKNOWN> [1]
  0.00 0.00       100/100 consuCpu1 [0]
------------------------
  0.00 0.00      1000/1000 x2 [3] [2]
  0.00 0.00      1000 consuCpu2 [2]
------------------------
  0.00 0.00         1/1 <UNKNOWN> [3]
  0.00 0.00      1000/1000 consuCpu2 [2]
------------------------
```

在上方和下方，“<UNKNOWN>”字符串表示位于受配置文件监控对象之外的标识符（在本示例中，这些是 main() 的实例）。

**sprof -c** 选项生成调用对及其出现次数的列表：

```
$ sprof -c libdemo.so.1 $LD_PROFILE_OUTPUT/libdemo.so.1.profile
<UNKNOWN> x1 1
x1 consuCpu1 100
<UNKNOWN> x2 1
x2 consuCpu2 1000
```

### 参见

(1), (1), (8)

### 结语

本页是 Linux *man-pages* 项目版本 4.00 的一部分。有关该项目的说明、报告错误的信息以及本页的最新版本，请参阅

## SSH-ADD

### 名称

**ssh-add** - 将私钥身份添加到认证代理

### 概要

**ssh-add** `[-cDdkLlXx]` `[-E` *fingerprint_hash*` ]` `[-t` *life*`]` `[`*file*`...]`  
**ssh-add** `-s` *pkcs11*  
**ssh-add** `-e` *pkcs11*

### 描述

**ssh-add** 将私钥身份添加到认证代理 ssh-agent(1)。在没有参数运行时，它会添加文件 `~/.ssh/id_rsa` `~/.ssh/id_dsa` `~/.ssh/id_ecdsa` `~/.ssh/id_ed25519` 和 `~/.ssh/identity`。加载私钥后，**ssh-add** 将尝试从文件加载相应的证书信息：该文件名是通过在私钥文件名称后追加 `-cert.pub` 获得的。可以在命令行上提供替代的文件名。

如果任何文件需要密码短语，**ssh-add** 会向用户询问密码短语。密码短语从用户的 tty 读取。如果提供了多个身份文件，**ssh-add** 会重试最后一次使用的密码短语。

认证代理必须正在运行，并且环境变量 `SSH_AUTH_SOCK` 必须包含其套接字名称，**ssh-add** 才能正常工作。

选项如下：

- **-c**
  - 指示添加的身份在用于认证之前应经过确认。确认由 ssh-askpass(1) 执行。成功的确认由 ssh-askpass(1) 的零退出状态表示，而不是请求者输入文本。

- **-D**
  - 从代理中删除所有身份。

- **-d**
  - 不添加身份，而是从代理中删除身份。如果未运行 **ssh-add** 参数，默认身份及其相应证书的密钥将被删除。否则，参数列表将被解释为公钥文件路径列表，以指定要从代理中删除的密钥和证书。如果在指定路径未找到公钥，**ssh-add** 将追加 `.pub` 并重试。

- **-E** *fingerprint_hash*
  - 指定显示密钥指纹时使用的哈希算法。有效选项为："md5" 和 "sha256"。默认为 "sha256"。

- **-e** *pkcs11*
  - 移除由 PKCS#11 共享库 *pkcs11* 提供的密钥。

- **-k**
  - 在将密钥加载到代理或从代理中删除密钥时，仅处理普通私钥并跳过证书。

- **-L**
  - 列出当前由代理表示的所有身份的公钥参数。

- **-l**
  - 列出当前由代理表示的所有身份的指纹。

- **-s** *pkcs11*
  - 添加由 PKCS#11 共享库 *pkcs11* 提供的密钥。

- **-t** *life*
  - 向代理添加身份时设置最大生存时间。生存时间可以指定为

