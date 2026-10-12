
```html
<HTML>
<HEAD>
<TITLE>CGI Survey</TITLE>
</HEAD>
<script>
function sendToCGI() {
    var results = "";
    var surveyForm = document.forms["survey"];
    for (var i = 0; i < surveyForm.length; i++) {
        if (surveyForm.elements[i].checked) {
            results += surveyForm.elements[i].value + "\n";
        }
    }
    // 这会将结果发送给 CGI
    alert("Results:\n" + results);
}
</script>
</HEAD>
<BODY>
<form name="survey">
<p>对产品的感觉：</p>
<input type="radio" name="g1" value="Strongly like"><br>
<input type="radio" name="g1" value="Like"><br>
<input type="radio" name="g1" value="Neither like nor dislike"><br>
<input type="radio" name="g1" value="Dislike"><br>
<input type="radio" name="g1" value="Strongly dislike">
</p>

<p>产品质量：</p>
<input type="radio" name="g2" value="Very high quality"><br>
<input type="radio" name="g2" value="High quality"><br>
<input type="radio" name="g2" value="Average quality"><br>
<input type="radio" name="g2" value="Poor quality"><br>
<input type="radio" name="g2" value="Very poor quality">
</p>

<p>产品定价：</p>
<input type="radio" name="g3" value="Price is very high"><br>
<input type="radio" name="g3" value="Price is high"><br>
<input type="radio" name="g3" value="Price is about right"><br>
<input type="radio" name="g3" value="Price is low"><br>
<input type="radio" name="g3" value="Price is very low">
</p>

<p>购买计划：</p>
<input type="radio" name="g4" value="Plan to purchase"><br>
<input type="radio" name="g4" value="May purchase"><br>
<input type="radio" name="g4" value="May purchase if price is lowered"><br>
<input type="radio" name="g4" value="May purchase if quality is improved"><br>
<input type="radio" name="g4" value="Do not plan to purchase">
</p>

<input type="button" value="Submit" onclick="sendToCGI()">
</form>
</BODY>
</HTML>
```

列表 7.5：带有 JavaScript 处理的调查表单。

![](img/6e99147f217994f89499215b2cff677f_244_2.png)

FIGURE 7.6：使用 JavaScript 显示的调查结果。

`js2cgi.htm` 文件包含一个带有四组单选按钮的 HTML 表单。用户点击单选按钮来填写产品调查。`sendToCGI()` 函数通过确定选了哪些按钮来处理提交按钮的 `onClick` 事件，并创建一个四个字符的文本字符串（存储在 `results` 变量中），来总结表单数据。例如，假设用户选择了第一组单选按钮的第三个值、第二组的第四个值、第三组的第一个值以及最后一组（第四组）的最后一个值。那么 `results` 变量的值将是 `2305`。

`results` 变量的值作为查询字符串附加到 CGI 程序的 URL 后，并将当前窗口位置对象的 `href` 属性设置为该 URL。这导致请求 CGI 程序的 URL。

当 Web 服务器接收到 `add2db.cgi` 的 URL 请求时，它会执行列表 7.4 所示的 Perl 脚本。由于 `js2cgi.htm` 传递的查询字符串是一个值而不是 `name=value` 对，Web 服务器假设该请求是一个 INDEX 查询，并将 URL 查询字符串中包含的数据作为命令行参数传递。

# 列表 7.4：在服务器上存储表单数据的 Perl 程序 (`add2db.cgi`)

```perl
#!/usr/bin/perl
open (OUTPUT, >>db.txt);
print OUTPUT @ARGV;
print OUTPUT "\n\n";
close (OUTPUT);
print "Location: /javascript/results.htm\n\n";
```

`add2db.cgi` 脚本的工作如下：第一行识别 Perl 解释器的位置。第二行以追加模式打开文件 `db.txt`；这意味着写入 `db.txt` 的任何内容都将追加到文件末。第三行将命令行参数的值写入 `db.txt` 文件。该值就是附加到 `add2db.cgi` URL 上的四个字符表单处理结果。第四行向 `db.txt` 写入换行符。第五行关闭 `db.txt` 文件，最后一行返回位于 `http://www.jaworski.com/javascript/results.htm` 的文件作为 CGI 程序处理的结果。图 7.6 显示了 `results.htm` 如何显示。

![](img/6e99147f217994f89499215b2cff677f_245_0.png)

# 从 CGI 程序返回 JAVASCRIPT

将客户端脚本与 CGI 程序整合的最强大的技术之一，就是使用 CGI 程序返回 JavaScript 代码。通过这样做，你的 Web 应用程序变得更加动态和高效，允许浏览器执行部分 CGI 程序的处理。CGI 程序不再通过静态 Web 页面响应，而是执行最少的服务器端处理，并返回一个 JavaScript 脚本来在浏览器上完成应用程序的处理。

接下来的示例展示了你如何使用 CGI 程序返回 JavaScript 代码。此示例基于上一节的 `add2db.cgi` 示例。

在列表 7.4 的最后一行中，返回了 `results.htm` 文件以完成 `add2db.cgi` 的处理。列表 7.5 显示了 `results.htm` 的内容。它在文档头部中包含两个脚本。第一个脚本包含了来自 URL `http://www.jaworski.com/cgi-bin/getdb.cgi` 的 JavaScript 代码——但这是一个 CGI 程序的 URL。列表 7.6 显示了 `getdb.cgi` 的源码。

#### 列表 7.5：显示产品调查结果 (`results.htm`)
