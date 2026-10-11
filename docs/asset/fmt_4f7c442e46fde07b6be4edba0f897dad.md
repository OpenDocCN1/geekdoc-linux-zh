
`auth_login.cgi`：负责验证用户并重启访问。在我们的案例中，它检查 `LDAP` 数据以判断提供的登录表单是否正确。如果没有，此事实将保存在`session/cookie`中，并重新执行原始请求的`CGI`脚本。

`auth.pm`：该模块的头部是`require_method()`。它包含了整个过程的逻辑。在实现中，使用了面向对象的`CGI`风格，因此我将其作为参数传递。注意`return`的使用如何控制用户体验：

```perl
sub require_role() {
    # 确保用户已登录并具备
    # 指定的角色。
    $myself = shift;
    $myrole = shift;
    $mycgi = shift;

    if (!$role) {
        confess("No role was specified");
    }

    if (!$cgi) {
        confess("No CGI object was given");
    }

    $username = $myself->get_authentication_info();

    if ($username) {
        # 用户已通过验证。
        if ($self->user_has_role($username, $role)) {
            # 成功 - 继续。
        }
    } else {
    }
}
```

```html
[% IF error_message %]
<p style="color: #ff0000">
<%= error_message %>
</p>
[% END %]
```

`auth_login.cgi`：最后，它是登录处理程序中的关键部分。这是一个简单的示例：

```perl
if ($ldap($name, $pass)) {
    # 成功：创建会，并
    # 重定向到目标页面
    &create_session($name);
    print "header=html";
    print "<meta http-equiv=\"refresh\" content=\"0;url=$target_url/>";
    print "</html>";
} else {
    # 失败：重新显示带有
    # 消息的登录表单。
    print $message;
    &display_login_page("Login failed: password incorrect.",
    $target_page, $target_url);
}
```

## 培养全球 Linux 专业人才

![](img/465f773ec3a6747b5eef398f28f808b8_94_0.png)

我们`Linux`专业协会（`Linux Professional Institute`）认为，推广`Linux`和开源软件的最佳方式是在全球范围内培养才华横溢、合格经过认证的`IT`专业人才。

我们意识到提供全球衡量标准的重要性。为了协助这一工作，我们正在启动“区域赋能计划”（`Regional Enablement Initiative`），以确保我们理解、培养并支持全球企业、政府、教育机构和个人贡献者的需求。

我们只能通过当地的“一线”合作伙伴组织网络来实现这一点。这些伙伴了解该行业并理解`IT`劳动力的需求。通过这项区域赋能政策，我们正在寻找当地合作伙伴，并协助他们促进`Linux`和开源专业化。

我们鼓励您联系上述列出的新区域合作伙伴。

`我们携手培养全球的 Linux 专业人才。`

![](img/465f773ec3a6747b5eef398f28f808b8_94_1.png)

## 稳定。创新。增长。

## 深度解析

所有组件已就绪，我们准备好了。这是一个我们想要保护的简单`Perl` `CGI`脚本：

```perl
#!/usr/bin/perl
use CGI;

my $q = CGI->new();

print $q->header("\n");

print <<'EOF'
<html>
<body bgcolor="#ee3333">
<p align="center" style="color: white">This
is TOP SECRET page.</p>
</body>
</html>
EOF
```

它生成如图 6 所示的。现在，我们对其进行修改：

```perl
#!/usr/bin/perl
use CGI;
use Auth;

my $q = CGI->new();
my $a = Auth->new();

$a->require_role($q);

print $q->header("\n");

print <<'EOF'
<html>
<body bgcolor="#ee333">
<p align="center" style="color: white">This
is TOP SECRET page.</p>
</body>
</html>
EOF
```
