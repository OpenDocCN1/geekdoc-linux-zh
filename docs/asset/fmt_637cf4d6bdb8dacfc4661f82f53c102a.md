
在此，脚本调用 `validate_data()` 子例程，将 `@fieldinfo` 数组引用传递给它，以验证输入的用户数据没有错误。该子例程执行以下操作：

1. 它遍历在 `@fieldinfo` 数组中（作为引用传递给子例程）找到的每个表单字段的具体信息，并获取字段名称、字段类型、字段要求等。
2. 对于每个表单字段，它使用 `$query->param($fieldname)` 方法从 `$query` 对象中获取值。该值存储在 `$value` 变量中。
3. 如果该字段是必需的且值为空，则错误消息被存储在 `@errors` 数组中，循环继续处理下一个字段。如果该字段是可选的且用户未输入值，循环继续处理下一个字段。
4. 当存在值时（无论是必需字段还是可选字段），都会调用 `check_data_field()` 子例程，以验证该值是否符合配置文件中陈述的字段要求。
5. 如果字段值通过了由 `check_data_field()` 子例程执行的验证检查，则根据配置要求更改该值的大小写。换句话说，该值要么转换为大写，要么转换为小写，要么保持混合大小写，并使用 `$query->param()` 方法存储在 CGI 对象中。`check_data_field()` 例程返回一个错误列表（如果有）。
6. 如果 `check_data_field()` 子例程返回了错误，脚本使用 `alert()` 子例程显示错误消息并中止。另一方面，如果没有错误需要报告，脚本继续使用 `write_data()` 子例程将数据写入磁盘。`write_data()` 使用配置文件中的数据文件名。完全限定的数据文件路径基于配置参数 `data_directory` 和 `data_filename`。该例程按照 `data_field_order` 配置参数中给出的顺序，使用 `data_field_separator` 参数中命名的字段分隔符，写入用户输入的大写修改后的数据。请注意，数据文件仅以追加模式打开，并且在文件操作期间它是独占锁定的，以便在此期间没有其他 `formwizard.pl` 副本可以访问它。
7. 然后，脚本使用在 `formwizard.ini` 中发现的 `thankyou_redirect_url` 配置选项来确定是否应将用户重定向到另一个 URL，或是否应向用户显示致谢消息。如果配置文件中的 `thankyou_redirect_url` 不为空，脚本使用 `redirect_data()` 子例程将用户重定向到指定的 URL。`redirect_data()` 子例程将所有表单字段作为键值对打包在 URL 中，并将用户的 Web 浏览器重定向到该 URL。例如，如果 `register.html` 填写为 name=محمد كبريت, zipcode=95833, email=MRKABILRO@gmail.com 和 optin=yes，并且 `thankyou_redirect_url` 设置为 `http://www.domain.com/friends.pl`，那么 `redirect_data()` 子例程将 Web 浏览器重定向到：

```
http://www.domain.com/friends.pl?name=Mohammed%20Kabir&zipcode=95833&email=mrkabir@hotmail.com&opt-in=yes
```

这使得远程站点能够通过 HTTP GET 方法接收清理过的用户数据。请注意，如果你只是想将用户重定向到另一个页面而不通过 GET 提交数据，请将配置文件中的 `send_data_on_redirect` 参数设置为 `no`。

8. 如果未设置 `thankyou_redirect_url`，脚本使用 `thankyou_template` 配置参数从配置文件中加载**致谢模板文件名**。假设该模板位于由 `template_dir` 配置参数指向的模板目录中。脚本使用 `show_thanks()` 子例程显示致谢页面。`show_thanks()` 子例程通过用用户输入（但已清理）的数据字段值替换特殊标记来个性化**致谢**内容。这是通过创建一个 `HTML::Template` 对象实例来实现的，该对象通过 `thankyou_template` 参数指向的模板页面进行初始化。称为 `$template` 的 `HTML::Template` 对象使用其 `$template->param()` 方法用通过 `$query->Vars()` 方法创建的哈希来替换特殊标记。最后，显示脚本的输出，脚本终止。

此示例中使用的致谢模板如清单 12-5 所示。

### 清单 12-5: thankyou.html 页面

```html
<html>
<body bgcolor="white">
<font face="Arial" size=+1>User Registration Complete</font><br>
<p>
<form action="CTMPL_VAR name=REFERER" method="GET">
<table border=0 cellpadding=3 cellspacing=0 bgcolor="#000000">
<tr>
<td>
<table border=0 cellpadding=5 cellspacing=5 bgcolor="#abcdef">
<tr>
<td>
<TMPL_VAR NAME=name>, <p>
Thank you for taking the time to register. We will send you information via
<TMPL_VAR NAME=email>.  
</td>
<tr>
<td align=center> <input type=submit value="Return"</td>  
</tr>
</table>
</td>
<tr>
</table>
</form>
<p>  
</html>
```

请注意此 HTML 模板中的 `<TMPL_VAR NAME=name>` 和 `<TMPL_VAR NAME=email>` 标记。这两个标记将被用户输入的 **name** 和 **email** 字段值替换。请记住，在数据验证期间，脚本会更新用户输入字段的大小写，以便显示的实际值格式良好，这在向用户显示信息时非常有用。因此，用户可以在名称字段中输入 **carol godsave**，但致谢页面将显示 **Carol Godsave**，这应该比按原样显示数据让用户更满意。这是四次 `register.html` 表单提交后的一个示例数据文件。

```text
kahir@domain.com,Mohammed J. Kabir,12345,no
carol@domain.com,Carol Godsave,95833,yes
joegunchy007@aol.com,Joe Gunchy,07024,yes
jennygunchy007@aol.com,Jennifer Gunchy,07024,no
```

## 使用 formwizard.ini 管理 Web 表单

如前几节所述，使用 `formwizard.ini` 配置文件的 `formwizard.pl` 脚本非常可配置，并且允许你使用单个脚本和单个集中配置文件来管理许多单页 Web 表单。要管理新的 Web 表单，只需复制 `register.html` 的配置文件，并在 `formwizard.ini` 文件中创建一个新的部分。以下是使用此脚本管理名为 **feedback.html** 的 Web 表单所需执行的步骤。

1. 在 `formwizard.ini` 文件中创建一个新的部分，称为 `[feedback.html]`，如下所示：

```ini
[register.html]
template_dir        = /path/to/feedback/template/dir

thankyou_template = thanks.html
send_data_on_redirect = no
form_field_info=<<FORM_FIELDS
#
# insert field info here
#
FORM_FIELDS

data_error_msg = 请输入缺失的数据并重新提交。
data_directory=//feedback/data/directory
data_filename=feedback.csv
data_field_separator=,
data_field_order=此处填写逗号分隔的字段列表
```

通过查看 `[register.html]` 部分进行必要的更改。

2. 将反馈表单的 action 行更改为：

```html
<form action="/c/s.dll/formwizard.pl" method="POST">
```

3. 在 `[feedback.html]` 部分中由 `template_dir` 参数指定的目录中创建 `thanks.html` 模板。该模板文件应使用 `<TMPL_VAR name=fieldname>` 标签来个性化感谢信息。

这就是使用 `formwizard.pl` 管理新 Web 表单的全部内容。对于大多数网站而言，Web 表单管理是 CGI 工作量的重要组成部分，而 `formwizard.pl` 脚本有助于您集中管理 Web 表单，从而轻松支持这些表单。

**提示** 在开发该脚本期间，我让许多人试用。他们不断发现该脚本的新功能和酷调整。我创建了一个 SourceForge 项目站点，用于发布我在 GNU 通用公共许可证 (GPL) 下发布的所有 CGI 脚本，因此你应该随时可以在 `https://sourceforge.net/projects/mkweb/` 上获取此脚本的最新版本。[MK01]

## 创建通过电子邮件发送页面的脚本

许多热门网站都具有让用户通过电子邮件向朋友或同事发送 Web 页面的功能。这类功能有助于网站增加流量，并且经常被市场部门视为一种优秀的病毒营销工具。在本节中，我将向您展示如何在您的网站上添加一个 CGI 脚本，使您的访问者能够通过电子邮件将您的任何 Web 页面发送给其他人。首先，让我们看看其工作原理。

用户可以输入朋友或同事的电子邮件地址，然后单击发送按钮将此 Web 页面发送给可能对此感兴趣的人。页面的实际 HTML 内容并不重要；重要的是这里显示的小嵌入式 HTML 表单：

```html
<form action="/cgin-bin/mime-mail.pl" method="POST">
  <input type=text name="name"   value="your-name" size=12
         maxsize=50>&nbsp;<br>
  <input type=text name="email"  value="friend-email" size=12
         maxsize=100>&nbsp;
  <input type=submit value="Send">
</form>
```

当用户输入其姓名以及朋友或同事的电子邮件地址并单击“发送”时，将调用 `/c/s.dll/mime-mail.pl` 脚本，该脚本如列表 12-6 所示。

### 列表 12-6: /cgin-bin/mime-mail.pl

```perl
#!/usr/bin/perl -w

#
#  Name: mime-mail.pl
#
#  Purpose:
#
#  Sends the referrer page via email
#
############################################

use strict;
use CGI;
use MIME::Lite;
use MIME::Lite::HTML;
use Config::IniFiles;
use File::Basename;

#
# Create a CGI object
#
my $query = new CGI;

#
# Create a configuration object by loading the mime-mail.ini
#  file from the physical directory pointed by /cgin-bin/
#
my $cfg     = new Config::IniFiles -file => "mime-mail.ini";

#
# Get the referrer URL
#
my $referrerURL = $ENV[HTTP_REFERER];

#
# Get the referrer page name from the referrer
# information
my $pageName = get_form_name($referrerURL);

#
# Print content type header to be text/html
#
print $query->header;

#
# If the referrer page does not have a [section] in
# the mime-mail.ini file, then use default section
$pageName = 'defaults' if ($cfg->val($pageName, 'from') eq '');

#
# Get the e-mail address. If no e-mail address is supplied,
# show error message
#
my $to = ( $query->param('email') eq '' ||
	! check_email($query->param('email'), 'email')) ?
	abort('Email address is missing.') : $query->param('email');

my $senderName = ( $query->param('name') eq '') ?
	abort('Your name is missing.') : $query->param('name');

$senderName = format_name($senderName);

#
# Create a MIME::Lite::HTML object and initialize
# it with referrer, an
my $mailHTML = new MIME::Lite::HTML 	From: => $senderName . '<' .
			$cfg->val($pageName, 'from') . '>',
			To 	=> $to,
			Subject => $cfg->val($pageName, 'subject');

#
# Parse the referrer URL and create a MIME mail object
#
my $MIMEEmail = $mailHTML->parse($referrerURL);

#
# Send the MIME mail
#
$MIMEEmail->send;

#
#
# Check error string for errors
#
my @errors = $mailHTML->errstr;

#
# If no error found, tell the user that page was
# sent to her friend; otherwise, show error message
#
if ($#errors > -1 ) {
  print abort("Error(s) found: ' . join('\n', @errors));

} else {
  print abort("Page sent to $to.\nThank you.")

}

#
# Terminate
#
exit 0;

sub abort {
  # Print javascript abort message
  print sprintf("<script>alert('$s');history.go(-1);

</script>",shift));

  exit 0;
}

sub get_form_name {
  my $referrer = shift;
  # If the HTTP referrer has a query string in it
  # return only the nonquery string part of it
  #
  if ($referrer =~ /^/()) {
     ($referrer, undef) = split(//?, $referrer);
  }

  return basename($referrer);
}

sub format_name {
  my @str = ();
  foreach my $part (split(\//,shift)) {
    push(@str, ucfirst(lc($part)));
  }

  return join(' ',@str);
}

sub check_email {
    my $email = shift;
    my $fieldName = shift;
    # Special note
    # This e-mail checker routine might return false (0)
    # for some rarely used RFC-compliant e-mail addresses
    # that are not common. For example, bob&sandra@domain.com
    # will fail. If you wish to allow such "technically" valid
```
