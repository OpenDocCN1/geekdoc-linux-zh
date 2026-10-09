
## 11.3 使用基于非 TET 的测试

```
200|1 5 14:50:07|Check header id EL_MAG3 is ELFNG3
220|1 5 0 14:50:07|PASS
410|1 5 14:50:07|IC End
400|1 6 14:50:07|IC Start
200|1 6 14:50:07|Check header id EL_CLASS is ELFCLASS32
220|1 6 0 14:50:07|PASS
410|1 6 14:50:07|IC End
400|1 7 14:50:07|IC Start
200|1 7 14:50:07|Check header id EL_DATA is ELFDTATA2LSB
220|1 7 0 14:50:07|PASS
410|1 7 14:50:07|IC End
400|1 8 14:50:07|IC Start
200|1 8 14:50:07|Check header id EL_VERSION is EV_CURRENT
220|1 8 0 14:50:07|PASS
410|1 8 14:50:07|IC End
400|1 9 14:50:07|IC Start
200|1 9 14:50:07|Check header id EL_OSABI is ELFOSABI_SVSV
220|1 9 0 14:50:07|PASS
410|1 9 14:50:07|IC End
400|1 10 14:50:07|IC Start
200|1 10 14:50:07|Check header id EL_ABIVERSION is 0
220|1 10 0 14:50:07|PASS
410|1 10 14:50:07|IC End
400|1 11 14:50:07|IC Start
200|1 11 14:50:07|Check header field e_type is ET_DYN
220|1 11 0 14:50:07|PASS
410|1 11 14:50:07|IC End
400|1 12 14:50:07|IC Start
200|1 12 14:50:07|Check header field e_machine is EM_386
220|1 12 0 14:50:07|PASS
410|1 12 14:50:07|IC End
400|1 13 14:50:07|IC Start
200|1 13 14:50:07|Check header field e_version is EV_CURRENT
220|1 13 0 14:50:07|PASS
410|1 13 14:50:07|IC End
400|1 14 14:50:07|IC Start
200|1 14 14:50:07|Check header field e_flags is 0
220|1 14 0 14:50:07|PASS
410|1 14 14:50:07|IC End
10|2 libc.so.6 14:50:07|
200|2 1 14:50:07|Looking for library libc.so.6
520|2 1 0 0.0|Found match for libc.so.6 as /lib/tls/libc.so.6
```

### 11.3.2 使用 lsb-test-pam

lsb-test-pam 测试验证应用程序的认证机制，并允许本地系统管理员选择单个应用程序如何验证用户。

#### 11.3.2.1 安装 lsb-test-pam

按照以下步骤安装 lsb-test-pam：

- 1. 从 LSB 下载网站下载该软件包。<sup>7</sup>
- 2. 使用以下命令安装二进制 RPM 软件包：

```
# rpm -ihv lsb-test-pam-version.architecture.rpm
```

#### 11.3.2.2 运行 lsb-test-pam

- 1. 注销并以用户 vsx0 的身份登录。您可能需要先为此账户设置密码，因为在安装该软件包时未为其设置任何密码。
- 2. 使用以下命令执行 run_tests：

```
vsx0$ ./run_tests
```

示例 11.6 展示了如何运行 lsb-test-pam。

**示例 11.6：运行 lsb-test-pam**

```
Name of person running tests (Automated)? Sparky
Organization (NONE)? TSMA
Test System (UNKNOWN)? lsbtest1
Block special filename (!)?
Enter name of the user for PAM tests [vsx0] :
Enter password of the user for PAM tests : ******
Enter password of the test user vsx1 : ******
Enter password of the test user vsx2 : ******
Install /etc/pam.d/lsbpam_conf . ? [y]
Enter root password: ******
Password:
Updating the account properties of users vsx1 and vsx2
sets the vsx1 account to have a password that needs to be updated
sets the vsx2 account to be expired

Enter root password: ******
Password:
```

示例 11.7 展示了 lsb-test-pam 的日志文件。

![](img/d75cffbcb54aabfb0f9854162061d394_178_0.png)

## 11.4 扩展 LSB 测试套件

本节描述了如何通过添加新测试来扩展测试套件。

### 11.4.1 新测试套件的准则

为了对认证测试有用，测试用例应满足以下若干准则：

![](img/d75cffbcb54aabfb0f9854162061d394_179_0.png)

这些准则取自 Open Group 的测试套件验收标准。<sup>8</sup>

### 11.4.2 编写基于 TET 的测试套件

本节将帮助您从高层面理解测试开发过程。该过程包括以下高层步骤。

#### 11.4.2.1 制定规范

该规范应包含关于测试套件的以下信息：

- 测试方法
- 功能覆盖范围
- 测试架构
- 假设条件
- 开发计划

#### 11.4.2.2 制定正式断言集合

此步骤的目的是从规范中创建可测试语句列表。这是规范语言与实际测试代码之间的中间步骤。

正式的测试断言应弥合规范语言与测试套件代码之间的差距。同样，测试代码的目标是产生规范需求的可执行表示。使用基于断言的技术开发的测试套件应满足以下要求：

- 必须遵循 IEEE 标准测试方法 (1003.3)。
- 必须为受测规范中的每个确定性语句开发一个断言。
- 每个断言的设计都必须用于测试受测实现中该语句是真是假。

#### 11.4.2.3 断言审查

断言审查有助于识别断言编写者做出的不良假设，以及被测规范中的歧义或错误。

#### 11.4.2.4 测试用例开发

这包括将断言映射到试图验证它们的实际代码。测试用例编写者应尝试遵循第 11.4.1 节中列出的准则，特别是每次只测试一件事，并避免测试用例之间产生副作用。在尝试调试测试失败时，这两个特性尤其有价值。

#### 11.4.2.5 测试用例审查

让其他人在各种实现上运行测试用例有助于发现测试用例代码和底层规范中的问题。测试用例审查用于验证测试套件。审查应遵循以下准则：

- 使用审查准则和预设响应格式。
- 评论应具体。
- 评论应包括具体操作。

### 11.4.3 将现有测试套件转换为使用 TET/VSXgen 框架

有两种方法可以将现有测试用例转换为在 LSB 使用的 TET/VSXgen 框架中可用。本节描述了每种方法。

#### 11.4.3.1 在原始测试用例源代码中添加特定于 TET 的调用

此方法最适合包含一系列宏的测试用例。例如：

```
ASSERT(foo==5, "Foo was not 5");
```

#### 11.4.3.2 用支持 TET 的 Shell 代码封装二进制文件

此方法最适合那些返回信息性退出代码或可解析错误消息的测试用例，以便可以使用 shell 脚本封装器将这些转换为 TET 返回代码。虽然此方法允许重用现有的测试用例代码，但它可能使测试套件更难调试，结果更难理解。

## 11.5 下载 LSB 测试套件

要获取 LSB 测试套件，请访问 LSB 下载网页。<sup>9</sup> 表 11.1 表示可以通过万维网访问的信息。

| 规范版本 | 软件包 | 版本 | 架构 |
| --- | --- | --- | --- |
| 2.0 | `lsb-runtime-test` | 2.0.0-1 | IA86, IA64, PPC, PPC64, S390, S390X, x86_64, SRC |
| 2.0 | `lsb-test-pam` | 2.0.0-1 | IA86, IA64, PPC, PPC64, S390, S390X, x86_64, SRC |
| 2.0 | `lsb-test-vsw4` | 2.0.0-1 | IA86, IA64, PPC, PPC64, S390, S390X, x86_64, SRC |
| 2.0 | `lsb-test-c++` | 2.0.0-1 | IA86, IA64, PPC, PPC64, S390, S390X, x86_64, SRC |
| 2.0 | `lsblibcck` | 2.0.0-1 | IA86, IA64, PPC, PPC64, S390, S390X, x86_64, SRC |

