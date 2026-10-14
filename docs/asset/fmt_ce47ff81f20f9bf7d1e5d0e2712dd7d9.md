
如你所见，使用 `uncgi` 是快速编写表单处理 CGI 脚本的简单方法。如果你想尝试 `uncgi`，可以从随附 CD-ROM 安装它，并在 http://www.hyperion.com/-koreth/uncgi.html 阅读文档。

### 示例 11-3：`audioconpl`，一个允许用户访问多种格式声音的 CGI 脚本

```perl
#!/usr/local/bin/perl

#

# audioconpl: 用于转换音频格式的 cgi 脚本

#

# 此处 sox 二进制文件的位置
$sox="/usr/local/bin/sox";

# 服务器上查找音频文件的目录
$sound_dir="/html/sounds";

# sounddir 中音频文件的正则表达式
#
$incl_pat='\.au$|\.aiff$|\.wav$|\.voc$';

# 我们可以转换的音频样本类型
# 及其扩展名的关联数组
format_ext=(
  "Apple/SGI AIFF", "aiff",
  "Sun u-law", "au",
  "MS-Windows WAV", "wav",
  "Sound Blaster VOC", "voc",
);

# 相同扩展名及其
# 适当 MIME 类型的关联数组
%format_type=(
  "aiff", "audio/x-aiff",
  "au", "audio/basic",
  "wav", "audio/x-wav",
  "voc", "audio/x-voc",
);

# 拷贝这些 CGI环境变量
$method = $ENV(REQUEST_METHOD);
$query_string = $ENV(QUERY_STRING);

# 检查访问方法
if ($method ne 'GET') {
    &print_header("text/html", "AudioConvert 方法错误");
    print("AudioConvert 必须使用 GET 方法调用。\n");
    &print_footer();
    exit;
}

# 如果没有查询字符串，则打印表单
if ($query_string eq '') {
    &print_header("text/html", "AudioConvert");
    &print_form("GET", "cgi-bin/audioconvert.pl");
    &print_footer();
    exit;
}

# 否则，转换所需的声音
else
    # 将用户输入解包到关联数组
    %query_values = &break_query($query_string);
    # 确保文件和格式 HTML 变量都存在
    if ($query_values("file") == '') {
        &print_header("text/html", "AudioConvert 错误");
        print("未找到文件名。\n");
        &print_footer();
        exit;
    }
    if ($query_values("format") == '') {
        &print_header("text/html", "AudioConvert 错误");
        print("未找到要转换的格式。\n");
        &print_footer();
        exit;
    }
    # 将特殊的 URL 语法转换为正常
    $file = &normalize_query($query_values("file"));
    $format = &normalize_query($query_values("format"));
    # 在使用它打开文件之前，
    # 确保 $file 不包含任何“危险”符号
    if (!safety_check($file)) {
        &print_header("text/html", "AudioConvert 错误");
        print("文件名包含非法字符。\n");
        &print_footer();
        exit;
    }
    # 找到我们要转换的格式的正确扩展名
    if (($ext = $format_ext($format)) == '') {
        &print_header("text/html", "AudioConvert 错误");
        print($format . ": 未知格式.");
        &print_footer();
        exit;
    }
    # 打开管道到 sox 转换程序，使用
    # -t auto 选项，它可以自动检测格式
    # 奇怪的是，比告诉 sox 实际类型效果更好……尽管我们明明知道它！
    open(SOUND, "sox -t auto $sound_dir/$file $ext |");
    # 关闭缓冲
    $| = 1;
    # 将 sox 的输出到标准输出并关闭管道
    &print_header($ext);
    while (<SOUND>) {
        print $_;
    }
    close(SOUND);
```

## SUBROINES

# 给定的 MIME 类型和标题（如果是 text/html），打印页头
sub print_header (
    ($type, $title) = @_;
    print "Content-type: $type\n";
    if ($type eq "text/html") {
        print "<HTML>\n";
        print "<HEAD>\n";
        print "<TITLE>$title</TITLE>\n";
        print "<BODY>\n";
    }

# 给定的方法和动作，打印表单的主体
sub print_form ($method, $action) = @_;
    print "<h3>Audio Conversions</h3>\n";
    print "<FORM=$method ACTION=\"$action\">\n";
    print "<strong>To:</strong>\n";
    &format_select("format", (keys %format_ext));
    print "<P>\n";
    print "<INPUT TYPE=\"SUBMIT\" VALUE=\"Download\">\n";
    print "</FORM>\n";
}

# 结束 HTML 页面
sub print_footer {
    print "</BODY>\n";
    print "</HTML>\n";
}

# 给定的 URL 格式查询字符串，将其分解为
# 变量名及其值的关联数组
sub break_query {
  local($query_string) = @_;
  local($i);
  @form_names = split('&', $query_string);
  foreach ($i (@form_names) {
    ($html_name, $html_value) = split('=', $i);
    $query_values($html_name) = $html_value;
  }
  return %query_values;
}

# URL 语法将大多数字母数字字符转换为百分号，
# 后接字符的十六进制值。
# 此函数抵消这种奇怪现象
sub normalize_query {
  local($value) = @_;
  $value = tr+/// /;
  $value = s/%([a-f-F0-9])([a-f-F0-9])/pack("C", hex($1$2))/eg;
  return $value;
}

# 确保查询字符串中的所有字符都安全地传递给 perl 解释器
sub safety_check {
  local($tocheck) = @_;
  ($tocheck) = /^[a-zA-Z0-9_\-%.]+\$/;
}

# 给定目录和模式，打印排序后的 HTML 文件列表
sub list_files {
  local($dir_name, $incl_patt) = @_;
  print "<UL>";
