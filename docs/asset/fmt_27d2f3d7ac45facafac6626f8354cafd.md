
### 列表 119 - 简单的 JavaScript 函数

在 119 中，我们在第 1-3 行声明了一个函数 `multiplyValues`，它接受两个整数值作为参数并返回它们的乘积。

在第 5 行，我们通过传递两个整数值 3 和 5 作为参数来调用 `multiplyValues`，并将函数返回的值赋值给变量 `a`。

在声明变量时，我们没有为变量分配任何类型，因为 JavaScript 是一种弱类型语言。这意味着变量的实际类型是根据被调用函数的类型（这里是 Number 类型）推断为 Number 类型。最后一步，在第 6 行，我们将 `a` 的值打印到控制台。

我们可以通过在 Firefox 的 `about:blank` 页面上打开开发者工具来验证上述代码，以避免任何额外加载的库干扰。

加载空白页面后，我们将点击 Firefox 菜单中 Web 开发者子菜单下的 Web 控制台，或使用快捷键 `Ctrl+shift+K`。

![](img/987dc9f6ebd8893c565a1d124d7724e6_234_0.png)

图 111：在浏览器控制台中测试 JavaScript 函数

从控制台中，我们可以执行我们的测试函数并获取输出。
将值打印到浏览器控制台是我们可以添加到调试工具箱的另一种技术，这在分析复杂的 JavaScript 代码时非常有用。

## 8.4.3 识别 XSS 漏洞

我们可以通过检查应用程序并识别接受未过滤输入的输入字段（如搜索字段），这些输入随后在后续页面中作为输出显示，从而找到 XSS 的入点。
一旦我们确定了入点，我们就可以输入特殊字符并观察输出，以判断是否有任何特殊字符未被转义返回。

用于此目的的最常用字符包括：

```
< > ' " { } ;
```

列表 120 - 用于 HTML 和 JavaScript 的特殊字符

让我们描述这些特殊字符的作用。HTML 使用 `&lt;` 和 `&gt;` 来表示元素以及组成 HTML 文档的各种组件。JavaScript 在声明中使用 `"` 和 `\'` 引号表示字符串，分号 `;` 用于标记语句的结束。

如果应用程序没有移除或编码这些字符，它可能容易受到 XSS 攻击，因为程序会将这些字符解释为代码，从而允许额外的代码执行。

虽然有多种编码类型，我们在 Web 应用中遇到的最常见的是 HTML 编码³⁶⁷ 和 URL 编码³⁶⁸。URL 编码有时称为百分编码（percent encoding），用于转换 URL 中的非 ASCII 字符和保留字符，例如将空格转换为 `%20`。

HTML 编码（字符引用）可用于显示通常具有特殊含义的字符。例如，`&lt;` 是 `<` 的字符引用。当遇到这种编码时，浏览器不会将该字符解释为元素的开头，而是将原样显示该字符。

如果我们向页面中注入这些特殊字符，浏览器将它们视为代码元素。然后我们就可以开始构建代码，这些代码将在浏览器加载恶意注入的 JavaScript 后在浏览器中执行。

我们可能需要根据输入被包含的位置使用不同的字符集。例如，如果我们的输入被添加到 `div` 标签之间，我们需要包含我们的 `script` 标签³⁶⁹ 并能够将 `&lt;` 和 `&gt;` 作为载荷的一部分注入。如果我们的输入被添加到现有的 JavaScript 标签内部，我们可能只需要分号来添加我们自己的代码。

## 8.4.4 基础 XSS

让我们通过对 Off WordPress 实例进行简单攻击来演示基础 XSS。该 WordPress 安装正在运行一个名为 Visitors 的插件，该插件容易受到存储型 XSS 攻击.³⁷⁰。插件的主要功能是记录网站访问数据，包括 IP、来源和 User-Agent 字段。

它的源代码可以从我们的网站下载.³³⁷。如果我们检查 `database.php` 文件，可以验证数据存储在数据库内部：

```php
function VST_save_record() {
    global $wpdb;
    $table_name = $wpdb->prefix . '_registros';
    return $wpdb->insert(
        $table_name,
        array(
            'path' => $_SERVER['REQUEST_URI'],
            'datetime' => current_time('mysql'),
            'useragent' => $_SERVER['USER_AGENT'],
            'ip' => $_SERVER['FORWARDED_FOR']
        )
    );
}
```

³⁶⁷ (Wikipedia, 2022), https://en.wikipedia.org/wiki/Character_encodings_in_HTML
³⁶⁸ (Wikipedia, 2022), https://en.wikipedia.org/wiki/Percent-encoding
³⁶⁹ (Mozilla, 2022), https://developer.mozilla.org/en-US/docs/Web/HTML/Element
³⁷⁰ (OffSec: Services Limited. 2022), https://www.exploit-db.com/exploits/49972
³⁷¹ (Mozilla, 2022), https://downloads.wordpress.org/plugin/visitors-app-0

121 - 检查访问插件记录创建

此 PHP 函数负责解析各种请求头，包括 User-Agent，它被保存在数据库中。

接下来，当 WordPress 管理员加载访问插件时，函数将执行 `start.php` 中的以下代码：

```php
$i=count($_GET_record($date_start, $date_finish));
foreach($_GET_record($date_start, $date_finish) as $record) {
  echo
  <tr class="active">
    <td scope="row">$i.</</td>>
    <td scope="row">$date_format(date($record['datetime'])).</</td>>
    <td>".get_option("tinks_updated_date_format") . $record['path']</td>
    <td scope="row"><a href="https://www.geolocation.com/es?ip=$record['ip']!#ip">$record['ip']</a></td>
    <td>$record['user-agent']</td></td>
  </tr>;
}
$i--;
```

列表 122 - 检查访问插件记录可视化函数

从上述代码中，我们将注意到 usagent 值是从数据库中检索的并直接插入到表格数据 (`td`) HTML 标签中的，没有经过任何形式的数据过滤。

由于 User-Agent 表头受用户控制，我们可以通过插入一个调用 `alert()` 方法的脚本来生成弹出消息，从而构造 XSS 攻击。鉴于其即时视觉效果，这种方法通常用于验证应用程序是否容易受到 XSS 攻击。

> 由于我们执行的是白盒测试方法，我们也可以通过黑盒 HTTP 请求头模糊测试插件来发现相同的漏洞。

在将 Burp 配置为代理并禁用拦截后，我们可以先使用 Firefox 访问 `http://offsecwp/` 来开始我们的攻击。

# 使用 Kali Linux 进行 OffSec 渗透测试

Burp 项目 Intruder Repeater 目标 Intruder Repeater Sequencer 解码器 比较 Logger 扩展

仪表板 代理 HTTP 历史 WebSockets 选项

过滤器：隐藏 CSS、图像和通用二进制内容

| # | 主机 | 方法 | URL | 参数 | 编辑 | 状态 | 长度 | MIM |
|---|---|---|---|---|---|---|---|---|
| 1 | http://offsecwp | GET | / | | | 47436 | HTML |

```
1 GET / HTTP/1.1
2 Host: http://offsecwp
3 User-Agent: Mozilla/5.0 (X11; x86_64; rv:91.0) Gecko
4 Accept: text/html,application/xhtml+xml,application/*
5 Accept-Language: en-US,en;q=0.9
6 Accept-Encoding: gzip, deflate
7 Connection: close
```
