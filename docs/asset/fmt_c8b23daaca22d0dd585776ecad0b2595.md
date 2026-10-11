
```pascal
function variantInit(var V: TVData): HRESULT; stdcall;
function variantClear(var V: TVData): HRESULT; stdcall;
function variantCopy(var Dest: TVData; const Source: TVData): HRESULT; stdcall;
function variantCopyInd(var Dest: TVData; const Source: TVData): HRESULT; stdcall;
function variantChangeEx(var Dest: TVData; const Source: TVData; TVData; LCID: Integer; Flags: Word; varType: Word): HRESULT; stdcall;
```

# 变体测试程序

```pascal
function varType(const V: variant; AvarType: TVarType): Boolean; overload;
function varType(const V: variant; const AvarTypes: array of TVArray): Boolean; overload;
function varByRef(const V: variant): Boolean;
```

```pascal
function varIsEmpty(const V: variant): Boolean;
procedure varCheckEmpty(const V: variant);
function varNull(const V: variant): Boolean;
function varClear(const V: variant): Boolean;
```

```pascal
function varCustom(const V: variant): Boolean;
function varOrdinal(const V: variant): Boolean;
function varFloat(const V: variant): Boolean;
function varNumeric(const V: variant): Boolean;
function varStr(const V: variant): Boolean;
function varIsEmptyParam(const V: variant): Boolean;
```

# WideString 常程

```
function PUCSChars(const S: UCS4): PUCSChar;
function WidstringToUCS4string(const S: Widstring): UCS4string;
function UCS4stringToWidstring(const S: UCS4string): Widstring;
function UnicodeUtf8(Dest: PChar; Source: PWideChar; MaxBytes: Integer): Integer;
function Utf8ToUnicode(Dest: PWideChar; Source: PChar; MaxChars: Integer): Integer;
function Utf8Encode(const WS: Widstring): UTF8string;
function Utf8ToUtf8(const S: UTF8string): Widstring;
function AnsiToUtf8(const S: string): UTF8string;
function Utf8ToAnsi(const S: UTF8string) : string;
```

# 附录 有用的 RFC

意见请求（RFC）包含了理解各种计算机和互联网技术的有用信息。并非所有的 RFC 成为标准，但观察这些注释如何从早期注释演变为标准是非常有趣的。本附录为读者可能感兴趣的话题提供了快速参考。更多信息可以访问 http://www.ietf.org。

| RFC # | 描述 |
| :--- | :--- |
| 768 | 用户数据报协议 (UDP) |
| 788 | 简单邮件传输协议 (SMTP) |
| 791 | 互联网协议 (IP) |
| 792 | 互联网控制消息协议 (Ping) |
| 793 | 传输控制协议 (TCP) |
| 821 | 简单邮件传输协议 (SMTP) |
| 972 | 密码生成协议 |
| 1014 | XDR: 外部数据表示标准 |
| 1034 | 域名 – 概念与设施 |
| 1035 | 域名 – 实现与规范 |
| 1050 | RPC: 远程过程调用协议 |
| 1057 | RPC: 远程过程调用协议版本2 |
| 1081 | 邮局协议 – 版本 3 (POP) |
| 1082 | 邮局协议 – 版本 3 扩展服务提议 (POP) |
| 1094 | NFS: 网络文件系统协议规范 |
| 1180 | TCP/IP 教程 |
| 1270 | SNMP 通信服务 |
| 1301 | 多播传输协议 |
| 1321 | MDS 消息摘要算法 |
| 1487 | X.500 轻量级目录访问协议 |
| 1510 | Kerberos 网络身份验证服务 (V5) |
| 1531 | 超文本主机配置协议 |
| 1597 | 私有网的地址分配 |
| 1700 | 分配数字 (IP 地址与端口) |
| 1704 | 论上的身份认证 |
| 1730 | 互联网消息访问协议 – 版本 4 (IMAP4) |
| 1738 | 统一资源定位符 (URL) |
| 1777 | 轻量级目录访问协议 (LDAP) |
| 1823 | LDAP 应用程序接口 |
| 1866 | HTML 2.0 |
| 1898 | CyberCash 信用卡协议版本 0.8 |
| 1939 | 邮局协议 – 版本 3 |
| 1942 | HTML 表格 |
| 1945 | 超文本传输协议 – HTTP/1.0 |
| 1958 | 互联网体系原则 |
| 1980 | HTML 的提议扩展：客户端图像映射 |
| 2069 | HTTP 的扩展：摘要访问认证 |
| 2109 | HTTP 状态管理机制 (cookies) |
| 2131 | 动态主机配置协议 (DHCP) |
| 2292 | 用于 IPv6 的高级套接 API |
| 2368 | mailto URL 方案 |
| 2373 | IP 版本6 体系 |
| 2376 | XML 媒体类型 |
| 2396 | 统一资源标识符 (URI) : 通用语法 |
| 2616 | 超文本传输协议 – HTTP/1.1 |

PILLAR Technology Group 为您的业务需求提供优质技术解决方案。我们通过以下三步流程，将知识从我们的员工转移到您的员工。

知识转移始于坚实的课堂培训基础。Pillar Technology Group 的教育部门提供各种技术课程，旨在满足管理层和技术人员的期望。我们的讲师经常获得学生的高分以及行业内的认可。

导师制是那些需要 PILLAR 讲师提供更具个性化、短期咨询和建议公司的选项。这有助于公司获得他们感兴趣的话题的详细咨询信息，而不受长期承诺或结构化课堂环境的限制。

使用基于的技术构建企业级应用需要经验丰富的。在 PILLAR，我们的咨询服务提供长期支持，旨在为解决客户最关键的需求提供解决方案。我们在以下领域提供专业咨询服务：

- 业务
- 组件
- 网络
- 测试

欲了解更多关于 PILLAR Technology 及其服务的信息，请访问我们的：www.pillartechnology.com
