
```assembly
mov ebx, 1          ; 第一个参数：文件句柄 (stdout)

mov eax, 4          ; 系统调用号 (sys_write)

int 0x80            ; 调用内核

mov ebx, 0          ; 第一个参数：退出代码

mov eax, 1          ; 系统调用号 (sys_exit)

int 0x80            ; 调用内核
```

### 6.2.3. GAS (hello.S)

```assembly
.data # 段声明

msg .ascii "Hello, world!\n" # 我们亲爱的字符串

len - . msg # 我们字符串的长度

.text # 段声明

.global _start # 我们必须导出入口点

_start:

    mov $len, %edx      ; 第三个参数：消息长度

    mov $msg, %ecx      ; 第二参数：要写入的消息的指针

    mov $1, %ebx       ; 第一个参数：文件句柄 (stdout)

    mov $4, %eax       ; 系统调用号 (sys_write)

    int 0x80           ; 调用内核

    mov $0, %ebx       ; 第一个参数：退出代码

    mov $1, %eax       ; 系统调用号 (sys_exit)

    int 0x80           ; 调用内核
```

## 6.3. 构建可执行文件

### 6.3.1. 生成目标代码

构建可执行文件的第一步是从源码编译（或汇编）目标文件：

对于 `nasm` 示例：

```bash
$ nasm -f elf hello.asm
```

对于 `gas` 示例：

```bash
$ as -o hello.o hello.S
```

这产生了 `hello.o` 文件。

### 6.3.2. 生成可执行文件

第二步是通过调用链接器从目标文件生成可执行文件本身：

```bash
$ ld -s -o hello.o
```

这最终构建了 `hello` 可执行文件。

# 第 7 章 资源

## 7.1. 指南与链接

你获取 Linux/UNIX 汇编编程材料的主要资源是：

`http://linuxassembly.org/resources.html`

请访问该网站，获取大量关于不同 UNIX 操作系统和 CPU 的汇编项目、工具、教程、文档、指南等资源。由于其内容更新很快，我将不再在此处罗列。

如果你是汇编语言初学者，这里有一些入门指南：

- `The Art Of Assembly`（汇编语言艺术）
- x86 汇编语言常见问题解答 FAQ
- `ftp.ltuth.se` 镜像了 hornet 和 x2ftp 之前的 msdos 汇编编码相关存档
- CoreWars：一种学习通用汇编语言的趣味方式
- Usenet: `comp.lang.asm.x86`; `alt.lang.asm`

## 7.2. 邮件列表

如果你对 Linux/UNIX 汇编编程感兴趣（或有疑问，或者只是好奇），我特别邀请你加入 Linux 汇编编程邮件列表。

这是一个关于在 Linux、`*BSD`、`BeOS` 或任何其他 UNIX/POSIX 类操作系统下进行汇编编程的开放讨论；同时它不限于 x86 汇编（欢迎 Alpha、Sparc、PPC 等其他架构的开发者！）。

列表地址为 `<linux-assembly@vger.kernel.org>`。

如需订阅，请向 `<majordomo@vger.kernel.org>` 发送邮件，并在正包含以下内容：

```
subscribe linux-assembly
```
