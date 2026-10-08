
有很多工具可以帮助发现和探索 Web 应用程序漏洞，其中许多已预装在 Kali 中。在本节中，我们将探索其中一些工具，包括几个简单的浏览器扩展，在随后的章节中，我们将重点转向手动漏洞枚举和利用。

> ⁴¹ (Apache Software Foundation, 2019), https://tomcat.apache.org/tomcat-7.0-doc/manager-howto.html

> ²⁴² (phpMyAdmin, 2019), https://www.phpmyadmin.net/

自动化工具可以提高渗透测试人员的效率，但我们也必须识别手动利用技术，因为工具并非在每情况下都可用，而且手动技术提供了更大的灵活性和定制性。记住，工具和自动化让我们的工作变得简单，它们不会替你完成工作。

# 9.3.2 DIRB

`DIRB`²⁴³ 是一种 Web 内容扫描器，它使用字典列表通过向服务器发送请求来查找目录和页面。即使主索引页缺失，`DIRB` 也能识别 Web 服务器上有效的 页面。

默认情况下，`DIRB` 会识别服务器上的目录，但也可以进行自定义以搜索特定目录，使用自定义字典、在每个请求中使用 `set cookie` 或标头等。

让我们在 `megacorpone.com` 上运行 `DIRB`。我们将提供几个参数：要扫描的 URL、`-r` 表示非递归，以及 `-z 10` 表示每个请求添加 10 毫秒的延迟：

```
kali@kali:$ dirb http://www.megacorpone.com -r -z 10
...
URL_BASE: http://www.megacorpone.com/
WORDLIST_FILES: /usr/share/dirb/wordlists/common.txt
OPTION: not Recursive
SPEED_DELAY: 10 milliseconds

GENERATED WORDS: 4612

- Scanning URL: http://www.megacorpone.com/-
+ http://www.megacorpone.com/about (CODE:200|SIZE:12180)
+ http://www.megacorpone.com/admin (CODE:403|SIZE:292)
== DIRECTORY: http://www.megacorpone.com/assets/
+ http://www.megacorpone.com/contact (CODE:200|SIZE:7721)
+ http://www.megacorpone.com/index (CODE:200|SIZE:12519)
+ http://www.megacorpone.com/index.html (CODE:200|SIZE:12519)
+ http://www.megacorpone.com/index.html (CODE:200|SIZE:12519)
== DIRECTORY: http://www.megacorpone.com/assets/
+ http://www.megacorpone.com/contact (CODE:200|SIZE:7721)
+ http://www.megacorpone.com/index (CODE:200|SIZE:12519)
+ http://www.megacorpone.com/index.html (CODE:200|SIZE:12519)
== DIRECTORY: http://www.megacorpone.com/assets/
+ http://www.megacorpone.com/contact (CODE:200|SIZE:7721)
+ http://www.megacorpone.com/index (CODE:200|SIZE:12519)
+ http://www.megacorpone.com/index.html (CODE:200|SIZE:12519)
== DIRECTORY: http://www.megacorpone.com/assets/
+ http://www.megacorpone.com/contact (CODE:200|SIZE:7721)
+ http://www.megacorpone.com/index (CODE:200|SIZE:12519)
+ http://www.megacorpone.com/index.html (CODE:200|SIZE:12519)
== DIRECTORY: http://www.megacorpone.com/assets/
+ http://www.megacorpone.com/contact (CODE:200|SIZE:7721)
+ http://www.megacorpone.com/index (CODE:200|SIZE:12519)
+ http://www.megacorpone.com/index.html (CODE:200|SIZE:12519)
== DIRECTORY: http://www.megacorpone.com/assets/
+ http://www.megacorpone.com/contact (CODE:200|SIZE:7721)
+ http://www.megacorpone.com/index (CODE:200|SIZE:12519)
+ http://www.megacorpone.com/index.html (CODE:200|SIZE:12519)
== DIRECTORY: http://www.megacorpone.com/assets/
+ http://www.megacorpone.com/contact (CODE:200|SIZE:7721)
+ http://www.megacorpone.com/index (CODE:200|SIZE:12519)
+ http://www.megacorpone.com/index.html (CODE:200|SIZE:12519)
== DIRECTORY: http://www.megacorpone.com/assets/
+ http://www.megacorpone.com/contact (CODE:200|SIZE:7721)
+ http://www.megacorpone.com/index (CODE:200|SIZE:12519)
+ http://www.megacorpone.com/index.html (CODE:200|SIZE:12519)
== DIRECTORY: http://www.megacorpone.com/assets/
+ http://www.megacorpone.com/contact (CODE:200|SIZE:7721)
+ http://www.megacorpone.com/index (CODE:200|SIZE:12519)
+ http://www.megacorpone.com/index.html (CODE:200|SIZE:12519)
== DIRECTORY: http://www.megacorpone.com/assets/
+ http://www.megacorpone.com/contact (CODE:200|SIZE:7721)
+ http://www.megacorpone.com/index (CODE:200|SIZE:12519)
+ http://www.megacorpone.com/index.html (CODE:200|SIZE:12519)
== DIRECTORY: http://www.megacorpone.com/assets/
+ http://www.megacorpone.com/contact (CODE:200|SIZE:7721)
+ http://www.megacorpone.com/index (CODE:200|SIZE:12519)
+ http://www.megacorpone.com/index.html (CODE:200|SIZE:12519)
== DIRECTORY: http://www.megacorpone.com/assets/
+ http://www.megacorpone.com/contact (CODE:200|SIZE:7721)
+ http://www.megacorpone.com/index (CODE:200|SIZE:12519)
+ http://www.megacorpone.com/admin (CODE:403|SIZE:292)
```

> `Diruster` 是一个 Java 应用程序，类似于 `DIRB`，提供多线程和 GUI 界面。

# 9.3.3 Burp Suite

`Burp Suite`²⁴⁴ 是一个面向 Web 安全的工具集，被誉为强大的代理工具。虽然社区版包含手动测试工具，商业版包含额外功能，如强大的 Web 扫描器。`Burp Suite` 在 `OSCP` 考试中是允许的，但它并不是必要的。

> ²⁴⁴ (PortSwigger, 2019), https://portswigger.net/burp

# 使用 Kali Linux 进行渗透测试 2.0

![](img/f99f528ca9845f4c256ce54e882b1345_250_0.png)

图 90：启动 Burp Suite

我们也可以从命令行启动它：

```
kali@kali:~ burpsuite
```

> 282 - 从终端启动 Burp Suite

一旦启动，我们将选择临时项目并点击“下一步”。

# OFFENSIVE SECURITY
www.offensive-security.com
Penration Testing with Linux 2.0

欢迎使用 Burp Suite 社区版。使用以下选项创建或打开项目。

注意：基于磁盘的项目仅支持 Burp Professional。

![](img/f99f528ca9845f4c256ce54e882b1345_251_0.png)

图 91：Burp启动

- 临时项目
- 在磁盘上新建项目
  - 文件：[选择文件...]
  - 标识：
- 打开现有项目
  - 标识 | 文件
  - 文件：[选择文件...]
暂停爬虫和扫描器

- 选择您想要为此项目加载的配置
  - 使用 Burp 默认设置
  - 使用保存的项目选项
  - 从配置文件加载
    - 文件：[选择文件...]
  - 后续默认使用上述设置
  - 禁用扩展
取消  返回  启动 Burp

![](img/f99f528ca9845f4c256ce54e882b1345_251_1.png)

图 92：Burp 配置

# 使用 Kali Linux 2.0 进行渗透测试

稍等片，界面（UI）将加载。

```
Burp: Project Intruder Repeater Window Help

Target Proxy Intruder Repeater Sequencer Decoder Compar Comparator Extender Project options User options
```
