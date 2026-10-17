
```java
18. public class Authentication extends AppCompatActivity {
19. public boolean saveCache(Context context, String username, String password) {
20. String content = username + password;
21. Log.i("savelogInfo", "username = " + username + " | password = " + password + ");\n22. try {
23. File outputFile = File.createTempFile("cache", context.getCacheDir());
24. String content2 = Encryption.hashMessageDigest(Algorithms.MD5, content);
25. Log.i("savelogInfo", "Saving to file " + outputFile.getAbsolutePath() + " | md5 content " + content2);
26. BufferedWriter bw = new BufferedWriter(new FileWriter(outputFile.getAbsolutePath()));
27. }
```

图 6.17：PIVAA 创建临时文件

- 4. **PIVAA 创建可写文件**：当创建文件时带有可写权限，任何应用都可以向其写入。

查看 `com/htbridge/pivaa/handlers/Authentication.java` 的源码，我们看到它将 2 作为模式：

```java
51. public boolean createFile(Context context, String text) {
52. try {
53. FileOutputStream fs = context.openFileOutput("lock", 2);
54. fs.write(text.getBytes());
55. fs.close();
56. Log.i("info", "createFile: done");
57. return true;
58. } catch (Exception e) {
59. }
```

图 6.18：PIVAA 创建可写文件

- 5. **PIVAA 使用 SQLite 数据库并执行查询**：原始查询中的不可信用户输入可能导致 SQL 注入。考虑 `com/htbridge/pivaa/handlers/DatabaseHelper.java` 中的其中一个示例（如图 6.19 所示）。在这里，我们可以看到 `id` 直接传递给了 `rawQuery()`：

图 6.19：PIVAA 原始查询执行

图 6.20：不安全的数据库处理

## 代码动态加载

动态代码加载（DCL）允许应用程序加载不属于其静态代码库的代码。额外的代码可以从远程位置并在并在执行。

`com/htbridge/pivaa/handlers/LoadCode.java` 的源码（图 6.21）揭示了它是如何从存储在变量 `path` 中的路径加载 `test.jar` 的。

图 6.1：PIVAA 动态代码加载

影响质量的常见漏洞包括：

- 缓冲区溢出，特别是用 C 和 C++ 编写的代码，为黑客提供了运行任意代码或获得未经授权访问的机会

- 允许代码执行的漏洞，允许攻击者绕过验证和各种其他安全协议

- 与不安全的第三方集成

- 使用错误或不安全的 API

- 糟糕或不安全的编码语言结构，由格式字符串错误组成

或知识产权（IP）和信息窃取。可以通过多种方法来提高整体代码质量，例如使用高级混淆、多样化和完整性监控，这最终会让黑客难以理解代码。他们还可以识别出由于代码质量不完善导致的漏洞。

## 代码篡改漏洞

代码篡改是指黑客操纵应用程序的源代码以创建相同应用程序的修改或伪造版本。这些操作可能是恶意的，也可能是无意的，但在大多数情况下，修改后的应用程序将不会按照发布者预期的方式运行。

### 代码篡改漏洞的严重性

应用程序开发者或发布者需要对他们的资产和知识产权（IP）拥有完全控制权，才能保护消费者和业务。代码篡改是 OWASP 移动端前 10 最典型的威胁之一。黑客创建应用程序的克隆并为了自己的目标对其修改，最终颠覆了应用发布者的意图。

此处列出了此漏洞相关的已知风险：

- 旨在绕过支付需求的盗版视频游戏应用

- 银行或金融应用被篡改以收集用户信息

- 进行直接或间接的在线诈骗

- 禁用内置安全功能

- 窃取广告收益

### 代码篡改的攻击向量

一旦黑客反向工程应用程序的代码并理解其流程和逻辑，他们就有各种方法注入恶意代码，改变应用的核心属性和功能。这包括对应用程序的核心二进制文件进行直接修改、方法钩子（`method hooking`）、对应用程序包内的资源进行更改，以及通过重路由或替换系统 API 以执行有害代码。显然，这种方法让黑客更容易对应用程序代码进行静态分析。

PIVAA 没有实现任何形式的代码篡改保护，这就是为什么我们能够反编译整个应用并查看其源代码。因此，整个应用程序可以被认为存在代码篡改保护不足。

### 代码篡改的缓解策略

移动应用程序应该能够识别是否包含了新代码，或者是否与其运行时学习的完整性信息发生了更改。应用程序需要在运行时对代码完整性违规做出适当响应。

此类风险的修复方法在 OWASP 反向工程以及代码修改防止项目的更多技术详情中：

`https://owasp.org/index.php/OWASP_Reverse_Engineering_and_Code_Modification_Prevention_Project`

Android 根检测：通常，经过自定义的应用程序会在越狱或 root 环境下执行工具程序。因此，尝试在运行时识别此类受操纵设备并做出相应反应（记录事件到 Web 服务器或关闭）是合理的。有几种检测已 root Android 工具的常用方法。这些是：

- 开发者可以检查 `build.prop` 是否包含 `ro.build.tags= test-keys` 行，这表明是设计构建或非官方 ROM。

- 开发者还可以检查 OTA 证书。检查名为 `/etc/security/otacerts.zip` 文件是否存在。

- 开发者还可以检查许多已知的 root 后 APK。其中一些列如下：

- `eu.chainfire.supersu`

- `com.thirdparty.superuser`

- `com.koushikdatta.superuser`

- `com.noshufou.android.su`

或者，开发者可以寻找 `su` 二进制文件的存在，它们是超级用户。这些二进制文件在有人尝试 root Android 设备时被安装，可以在以下设备路径找到：

- `/system/su`

- `/system/xbin/su`

- `/system/bin/su`

- `/sbin/su`

- `/system/bin/.ext/.su`

我们还可以尝试执行 `su` 命令并查看是否成功。如果返回 0，则意味着 `su` 命令执行成功。

## 反向工程漏洞

反向工程是 OWASP 移动端前 10 威胁中大多数主要攻击的起点。它涉及黑客下载并安装应用程序，然后使用反编译器或调试器对其最后的核心二进制文件进行分析，以识别其源代码、算法、库以及各种其他组件。基本上，它是从最终类型开始，解构并弄清楚应用程序是如何工作的。如果你注意到了，对于 MobSF 静态分析器，它是从反编译 APK 开始的，这仅仅是反向工程的第一阶段。

### 反向工程漏洞的严重性

当应用程序被高效地反向工程时，黑客可以获取许多他们可以窃取或生成的信息。

开关、测试代码、日志文件、后门或存在漏洞的管理员端点在开发或更新后被遗留或未受到充分保护。

## 冗余功能漏洞的严重性

根据功能的性质，它可能给应用所有者带来的担忧可能有所不相同。最严重的结果之一包括：黑客获得对系统后端的未经授权访问、执行管理员级功能的能力，或者对某些普通应用用户无法直接访问的隐藏功能的访问权限。

## 冗余功能漏洞的攻击向量

由于它不是应用程序刻意暴露的部分，多余能力可能会成为一个问题，因为软件工程师在寻找漏洞时可能不会留意它。为了发现并利用这些隐藏的漏洞，攻击者最初会检查应用程序以确定存在哪些功能。这让他们了解后端可以实现哪些操作。同样，他们可以记录数据以查看是否有任何遗留的端点或功能，并据此开发利用策略。

### 在 PIVAA 中验证冗余功能

MobSF 的清单分析模块尝试寻找开发者所犯的配置错误。PIV 的 `AndroidManifest.xml` 将调试能力设置为 `true`（如图 6.24 所示），这使得反向工程师更容易对其挂载调试器。这允许转储堆栈跟踪并访问调试器类：

```
:protectionLevel="dangerous" android:debuggable="true" android:allow
```

图 6.24：PIVAA 调试标志设置
