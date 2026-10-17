
尽管 MacOS X 和其他平台多年一直包含了对某些直接 IPv6 服务的支持，但其广泛普及仍然缓慢，在全球范围内尚未被普遍使用。这部分是因为对于许多客户端节点（通常是那些运行网络地址转换 `NAT` 的宽带路由器和调制解调器）来说，与 IPv6 完全集成非常困难。解决此问题的方案逐渐出现，MacOS X 现在已提供一种解决方案，名为 `Miredo`，它构建自 `Teredo` 项目，提供了一种在通往 IPv6 节点的路由中成功穿透 `NAT` 的巧妙方法。尽管对于那些加密通信前沿的人士来说，这种支持非常令人兴奋，但其开发仍处于非常早期阶段。（更多信息请访问 <http://www.remlab.net/miredo/>）。

# 第 8 章 · 加密技术与操作系统

# 总结

结论，Apple 已经从 OS9 的暗淡时代走了很远，现在 MacOS X 内部提供了丰富的加密选择。通过将大量的强加密工具集成到 MacOS X 中，Apple 为 Macintosh 用户提供了明显且即时改进的安全选项，但该公司也表明它仍然紧紧关注着未来，这种姿态在过去曾是它的救星。

另一方面，尽管苹果声称正在使用开源软件，但它尚未履行其声明的在自家后院与开源项目紧密合作（例如 `Open Darwin` 项目）的承诺。鉴于今天许多加密服务和程序都是使用纯开源平台大量开发的，并源于显然致力于开放精神本质的开源社区；苹果却露出了它真实的、传统意义上的“异同不同”中流出的企业色彩。

对于全球数字安全社区，以及其他领域的几代计算机专业人士来说，Apple 始终代表了常识战胜商业主义的最佳希望。通往真正安全的道路是显而易见的。世界期待 Apple 上路。

# 参考文献

- Appelbaum, J., Calandrino, J.A., Clarkson, W., Feldman, A.J., Felten, E.W., Halderman, A.J., Heninger, N., William, P., & Schoen, S.D., 2008, “We Remember: Cold Boot Attacks on Encryption Keys,” 于 2008 年 2 月 25 日，<http://citp.princeton.edu/pub/coldboot.>

- Driben, G., “How Mac OS X Implement Password Authentication Part 2,” Dave Driben 的博客，于 2008 年 2 月 12 日，<http://www.driben.org/blog/archives/2006/04/28/os_x_passwords_2/>。

- Fluhher, S., Mantin, I., Shamir, A., 2001, “Weaknesses in the Key Scheduling Algorithm of RC4,” Selected Areas in Cryptography, 第 1–23 页。

- IEEE, 2004.,“802.11i IEEE Standard for information technology – Amendment 6: Medium Access Control (MAC) Security Enhancements,”IEEE Standards Association,于 2008 年 2 月 3 日，<http://standards.ieee.org/getiee802/download/802.11i-2004.pdf>.

- Johnston, M., “Mac OS X stores login/Keychain/FileVault passwords on disk, 2004,” Security Focus，于 2008 年 3 月 2 日，<http://www.securityfocus.com/archive/1/367116/2004-06-24/2004-06-30/0>

- Levy, S., 2000, Penguin Books, London.

- Moskowitz, R., 2003, “Weakness in Pasphrase Choice in WPA Interface Wi-fi Net News，于 2008 年 1 月 28 日，<http://www.finewetnews.com/archives/002452.html>.

- NIST ITL, 1997, “Advanced Encryption Standard - ITL Security Bulletin,”National Institute for Standards and Technology USA,于 2008 年 2 月 7 日，<http://csrc.nist.gov/publications/nistbul/itl97-02.txt>.

- Schneier, B., 2000, “Secrets & Lies,”Wiley Publishing, Inc., Indianapolis, Indiana.

# 索引

## A

- Abrams, Randy, 134
- `ACID` (入侵数据库分析控制台), 196
- Activity Monitor (活动监视器), 36–37
- address resolution protocol (`ARP` 解析协议), 200
- Address Space Randomization (`ASLR` 地址空间随机化), 124, 301
    - 概念与基础, 269
    - 在 Leopard 上的缺点, 271
    - 内核内存缓冲区报告, 270
- Month of Apple Bugs (`MoAB` 苹果漏洞月)
- application enhancer (`APE` 应用程序增强), 273
    - 后果, 273
    - 格式字符串漏洞, 276–277
    - Quick Time 漏洞, 274
- Month of Kernel Bugs (`MoKB` 内核漏洞月)
    - 文件系统相关漏洞, 280
    - 堆缓冲区溢出漏洞, 281
    - `paxstest` 工具, 269–270
- Advanced Encryption Standard (`AES` 高级加密标准) 块密码, 298–299
- Advance Settings (高级设置), `CCC`, 13
- Analysis Console for Intrusion Databases (`ACID`), 196
- Antibody (抗体, 捕猎病毒), 282
- anti-malware program (反恶意软件程序), `avast!`, 147–148
- anti-malware technology (反恶意软件技术), 132
- anti-rootkit program (反 rootkit 程序), 132
- `APE` (应用程序增强), 273, 279
- Apple Developer Tools (Apple 开发者工具), 171–172
- Apple Mail.app bug, 54–55
- `AppleScript`, 87, 90
- Apple security features (Apple 安全特性), 125
- Apple’s SimpleCarbon, binary package (二进制包安装), 188–189
- Apple’s X11 Installation (Apple X11 安装), 171–172
- attacker’s control (攻击者控制), 寄存器, 26
- Apple’s deactivation (Apple 去激活), 144
- Apple’s library randomization (Apple 库随机化), 124
- Apple’s update mechanisms (Apple 更新机制), 95
- application-specific malware (特定应用程序恶意软件), 128
- Archibald, Neil, 62
- `ARP` (地址解析协议), 200
- asymmetric ciphers (非对称密码), 293
- authentication (认证), 109
- AutoStart disabling of (禁用 AutoStart), 144
- and Mac users (以及 Mac 用户), 94
- and- AutoStart variants (AutoStart 变体), 92–93
- AutoStart worm (AutoStart 蠕虫), 72
- `avast!` Mac Edition, 147–148
- algorithmic scanning (算法扫描), 139
- antivirus (反病毒软件), 155
- as-virus (病毒), 143
- as-attacks (攻击), 102–103
- codec (解码器), 96
- Code 252, system and application infector (系统和应用程序感染器), 83
- Code 98, system and application infector (系统和应用程序感染器), 84
- Command and Control (`C&C` 命令与控制机制), 77–78
- command prompt (命令提示符), 47
- compiling vs. porting, open source software, code (开源软件编译与移植), 180–181
- Comprehensive Perl Archive Network (`CPAN`), 172
- commands (命令), 176
- configuring (配置), 173–174
- interactive mode of (交互模式), 175–176
- `dns-mine.pl` script, dependency problem (`dns-mine.pl` 脚本依赖问题), 175
- Perl dependency (Perl 依赖), 175
- compromised matches (受损匹配), 77–78
- computer starts up (电脑启动), 3
- CrossOver Office buffer overflow (CrossOver Office 缓冲区溢出), 37–38
- `gdb` interface (`gdb` 接口), 40
- links for OSX (OSX 软链接), 46–48

## C

- `calc.exe`, 43. 参见 PowerPC shellcheck
- Carbon Copy theoretically (`CCC`) 数据备份, 11
- Macintosh formatted volumes (Macintosh 格式化卷), 12
- Carbon framework (Carbon 框架), 263–264
- `C&C` servers (`C&C` 服务器), 77–78
- Certificate Authorities (证书机构), 312

## D

- DarwinPorts package. 参见 OpenDarwin
- Data Encryption Standard (`DES`) algorithm (数据加密标准算法), 295–296
- Data Fork (数据叉), 8
- `_DATA` region, `libSystem`, 57–58
- DelProtect INIT, 144
- desktop AV software (桌面反病毒软件), 129
- detection technologies (检测技术), 142
- diffie-Hellman Key Exchange (Diffie-Hellman 密钥交换), 310–311
- Directory Scan (目录扫描), 7–8
- disinfectant, AV scanner (消毒剂, 反病毒扫描器), 145
- `dns-mine.pl` script, dependency problem (`dns-mine.pl` 脚本依赖问题), 175–176
- `dylib_stubs` (`dylib` 存根), 267–268
- `dylib` functions (dynamic library) (动态库函数), 261–264

## E

- `EFI` (Extensible Firmware Interface 扩展固件接口), 4
- interactive console (交互控制台), 5
- EICAR test file (`EICAR` 测试文件), 133
- purpose of (目的), 134
- `EIMS` (Eudora Mail Server), 21
- `EIP` address 2-byte representation of (`EIP` 地址的双字节表示), 31
- overwriting (覆盖), 61–62
- ethereal network analyzer (ethereal 网络分析仪), 204
- etnetack, packet-switched network (etnetack 包交换网络), 311
- Eudora Mail Server (`EIMS`), 21
- extensible authentication protocol over local area network (`EAPOL`) (局域网扩展认证协议), 242
- Extensible Firmware Interface (`EFI`), 4

## G

- `gdb` interface (`gdb` 接口), 40
- GDB Listener (`GDB` 监听器), 33
- generic detection (通用检测), 140
- GPS preferences (`GPS` 选项), 229

## H

- Hash functions (哈希函数), 294–295
- HC 9507 and HC 9603, 82
- HeaderBuilder, 9–10
- heterogeneous malware transmission (`HMT`) (异构恶意软件传输), 91–92
- heuristics (启发式算法), 140–141
- heuristic scanning technology (启发式扫描技术), 142
- Hierarchical File System (`HFS`) (分级文件系统), 88, 93
- `HMT` (heterogeneous malware transmission) (异构恶意软件传输), 128–129
- hook functions (钩子函数), 263
- host computer worms (主机蠕虫), 73
- HyperCard infectors (HyperCard 感染器), 81–86
- hypetext transfer protocol (`HTTP`) (超文本传输协议), 194
- hypetext transfer protocol over secure sockets layer (`HTTPS`) (基于安全套接字的超文本传输协议), 1193

## I

- iAdware (i广告软件), 49–50, 52
- `i` command (`i` 命令), 176
- `_IMPORT` sections writable status (`_IMPORT` 段可写状态), 59
- Init 29 and Init 1984 (Init 29 和 Init 1984), 84
- 电气电子工程师学会 (`IEEE`), 305
- 互联网消息访问协议 (`IMAP`), 196
- iPhoto Photocast XML 字符串格式漏洞, 276–277
- 映射, 228
- 使用接口, 233–234
- WEP 破解方法, 238–249, 242
- 窗口视图按钮, 234
- WPA 破解, 242
- `IPsec` 协议, 317–318
- `IPv6` 协议, 318–319
- iSight 摄像头
- 初始化, 254
- 光二极管 (`LED`), 255
- 对 应用程序接口 (`API`), 253
- `iSOAP`, 177

## J

- 联合图像小组 (`JPEG`), 244

## K

- 内核保护失败错误, 56–57, 61
- KisMac
    - 无线发现工具, 306
    - 使用其攻击 WLAN 加密, 238
    - 暴力破解攻击和字典列表攻击, 243
    - 兼容的网卡和芯片组, 225
    - 配置, 220–221
    - 使用其取消客户端认证, 240
    - 过滤选项, 223
    - 图形用户界面, 236
    - 地图服务器和地图类型, 230–231
    - 菜单，声音效果配置, 224
    - 渗透测试, 238
    - 偏好窗口, 227
    - 拒绝包, 240–241
    - 卫星地图, 232
    - 扫描选项, 222
    - 声音偏好, 223–224
    - 流量引用, 226
    - 使用 GPS 设备, 228–229
    - 选项, 236
    - WarDriving
- Kismet 声音偏好, 224

## L

- 2 层层隧道协议 (`L2TP`), 317
- Leopard 应用防火墙, 252–253
- 轻量级目录访问协议 (`LDAP`), 202
- 轻量级扩展认证协议 (`LEAP`), 243
- 登录窗口, 52–53

## M

- MacDrive6/7
    - 选项, 15
    - Windows 程序, 13–14
- Macintosh 文件系统, 8
- Macintosh Forensic Suite
    - 目录扫描工具, 7–8
    - FileSpy, 8–9
    - 取证套件工具栏, 6–7
