
# 致谢模板配置

在表单处理完成后，脚本必须向用户确认系统已接收数据。这通过一个“Thank You”（后文称为 `thankyou`）消息实现。

在此处设置 `thankyou` 模板的名称：

```
thankyou_template = thanks.html
```

---

# 重定向 URL 配置

如果你希望将用户重定向到另一个 URL，请在此处设置该 URL。如果你希望显示 `thankyou` 消息而不是重定向，请勿设置此 URL。

如果设置了 URL，它将始终优先于显示 `thankyou` 消息而被使用。

---

# 重定向时发送数据配置

脚本将显示 `thankyou` 消息或将用户重定向到另一个 URL。

如果你希望通过 GET 方法向重定向 URL 发送数据，请将此项设置为 `yes`；否则，设置为 `no`。

```
send_data_on_redirect = no
```

---

# 表单字段白名单配置

拥有一个特定的表单字段列表可以确保我们只使用所需的字段。任何额外的字段都会被忽略。

```
# ... (field list would go here)
```

### 分析 formwizard.ini

现在，让我们更仔细地查看此脚本，以便你可以根据具体需求进行配置。

第一行是一个特殊行：

```
#!/usr/bin/perl
```

此行告知系统在执行此脚本时运行 Perl。如果你将 Perl 安装在非标准目录中，则必须相应地更改此行。例如，如果你将 Perl 安装在 `/usr/local/bin/perl`，则需将此行修改以反映该路径。

下一段代码块是：

```
use strict;

use Config::IniFiles;

use File::Basename;

use HTML::Template;

use Fcntl qw(:DEFAULT :flock);

use CGI;
```

这将加载所有必要的标准模块和 CPAN 模块。此脚本使用的 CPAN 模块包括 `Config::IniFiles`、`HTML::Template` 和 `CGI`。实际上，`CGI` 模块现在作为标准 Perl 模块发行，但你必须使用 `CPAN` 模块安装其他两个模块。以下是两个快速命令，可以在 `root` shell 中为你安装这些模块：

```
perl -MCPAN -e 'CPAN::Shell->install('Config::IniFiles')'

perl -MCPAN -e 'CPAN::Shell->install('HTML::Template')'
```

你也可以运行

```
perl -MCPAN -e 'CPAN::Shell->install('CGI')'
```

以确保你的 `CGI.pm` 模块是 CPAN 网络上的最新版本。

下一段代码是

```
my $cfg      = new Config::IniFiles -file => "formwizard.ini";

my $query    = new CGI;

my $formName = get_form_name($ENV{HTTP_REFERER});
```

此段代码创建了一个名为 `$cfg` 的配置对象，该对象加载了 `formwizard.ini` 文件。`formwizard.ini` 文件是此脚本的核心配置文件，它必须与 CGI 脚本 `formwizard.pl` 位于同一目录中。如果你希望将其保存在与 CGI 脚本不同的目录中，你需要更改路径。例如，若要将在目录 `/www/myscripts/conf` 中存储配置文件，请按如下方式修改脚本：

```
my $cfg      = new Config::IniFiles

                 -file => "/www/myscripts/conf/formwizard.ini";
```

确保 Apache 用户（即在 `httpd.conf` 文件中 `User` 指令中使用的用户）可以读取该配置文件。脚本创建的 `CGI` 对象称为 `$query`。接下来，脚本调用一个名为 `get_form_name()` 的子例程，以获取调用它的 Web 表单的名称。该子例程为：

```
sub get_form_name {
    my $referrer = shift;
    # If the HTTP referrer has a query string in it
    # return only the non-query string part of it
    #
    if ($referrer =~ /\?/) {
        ($referrer, undef) = split(/\?/,$referrer);
    }

    return basename($referrer);
}
```

调用此子例程时，它会从 CGI 环境变量 `HTTP_REFERER` 获取值。此变量被设置为调用该脚本的 URL。例如，如果 `register.html` 表单可以通过 `http://rhat.mitec.com/asb2/chi2/forms/register.html` 这样的 URL 访问，那么当它被提交给 `/cvs.dll/formwizard.pl` 脚本时，CGI 对象 `$query` 会将 `HTTP_REFERER` 设置为 `http://rhat.mitec.com/asb2/chi2/forms/register.html`。`get_form_name()` 代码返回 URL 中的 `register.html` 部分。

然后，脚本将 Web 表单名称存储在一个名为 `$formName` 的全局变量中。

下一段代码是：

```
my $templateDir = $cfg->val($formName, 'template_dir');

my @fieldInfo = $cfg->val($formName, 'form_field_info');
```

此段代码将 Web 表单名称作为节名传递给配置对象，并检索当前 Web 表单的模板目录和表单字段信息的配置信息。这些信息分别存储在 `$templateDir` 和 `@fieldInfo` 数组中。配置文件示例 `formwizard.ini` 在列表 12-4 中展示，该列表显示了名为 `register.html` 的 Web 表单的示例配置。配置文件格式非常简单：

```
[section1]

key1 = value

key2 = value

key3 = value

key4 = <<MULTIPLE_VALUES
value1
value2
value3
...
valueN
MULTIPLE_VALUES
...
keyN = value

[section2]
```
