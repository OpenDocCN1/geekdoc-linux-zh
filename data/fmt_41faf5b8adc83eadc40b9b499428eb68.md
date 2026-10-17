
```apache
RewriteEngine On
# Ensure only numeric values for the page
RewriteRule ^article/([0-9]+)/?  article.php?page=$1 [L]
RewriteRule ^article/[^0-9]/?  article.php?page=1  [L]
```

### next|N

`*next*` 标志会在规则列表的开头重新启动重写过程。当规则被重新处理时，匹配的 URL 不是来自客户端的原始请求，而是使用 `*next*` 标志时内部重写后的 URL。例如：

```apache
RewriteRule  ^article/(\d+)/?  article.php?page=$1
RewriteRule  ^catalog/(\w+)/?  catalog.php?cat=$1  [N]
RewriteRule  ^catalog/(\w+)/(\w+)/? catalog.php?cat=$1&item=$2
```

在这个例子中，如果调用的 URL 匹配第二个规则，例如 `http://localhost/catalog/stuff/`，重写过程将在该点停止处理，并自动使用新替换的 URL `catalog.php?cat=stuff` 从规则集的开头重新启动。替换后的 URL 本身会通过整个规则集进行过滤。

使用 `*next*` 标志时应小心，因为可能会出现无限循环。

### chain|C

如果你希望将一组规则视为一个相关的单元，类似于 PHP 中的 `*try*` ... `*catch*` 语法，你可以使用 `*chain*` 标志。使用 `*chain*` 标志时，如果规则匹配，处理按预期继续并忽略 `*chain*` 标志。如果规则不匹配且存在 `*chain*` 标志，则所有链接在一起的后续规则将作为一个整体被跳过。例如，如果第一个不匹配，以下规则集将跳过到最后一个规则：

```apache
RewriteRule  ^article/(\d+)/?  article.php?page=$1 [C]
RewriteRule  ^catalog/(\w+)/?  catalog.php?cat=$1  [C]
RewriteRule  ^catalog/(\w+)/(\w+)/?  catalog.php?cat=$1&item=$2

# Skip to this rule if any of the above don't match
RewriteRule  ^article/(\d+)/?  error.php
```

### skip|$=number

当当前规则匹配时，此标志允许你跳过接下来的若干条规则。虽然 `skip` 标志的行为与 `chain` 标志相似，但它们的行为完全相反——`skip` 在成功匹配时跳转；`chain` 在匹配失败时跳转。

### type|T=mime-type

如果你想覆盖文档发送的 MIME 类型，可以使用 `type` 标志。例如，如果你有一批 `.xhtml` 文件，希望使用正确的 XHTML MIME 类型而不是 text/HTML 来提供它们，可以使用以下代码：

```apache
RewriteRule  ^.+.xhtml$  -  [T=application/xhtml+xml]
```

### cookie|CO=name:value:domain[:lifetime[:path]]

如你可能推断的那样，`cookie` 标志会在客户端浏览器上设置一个 cookie。三个必需字段——`name`、`value` 和 `domain`——分别指定 cookie 的名称、cookie 的值以及设置 cookie 的 `domain`。可选的 `lifetime` 参数代表 cookie 的有效期，以分钟为单位。`path` 参数设置 cookie 的路径。

例如，如果你想设置一个名为 `prevvisit` 的 cookie 来表示用户之前访问过主页（因此不应该被启动画面打扰），你可以使用此代码：

```apache
RewriteRule  ^index\.php$  -  [CO=prevvisit:true:domain.com]
```

### env|E=var:value

`env` 标志允许你将环境变量 `var` 设置为提供的值。该值也可以包含正则表达式反向引用（`$1` 和 `$n`）以实现更复杂的变量控制。可以在一组标志中设置多个环境变量——只需像其他标志列表一样用逗号分隔即可。

### qsappend|QSA

在大多数使用 `mod_rewrite` 的情况下，当执行重写时，提供给原始 URL 的任何查询字符串都会被丢弃。如果你希望保留这些信息而不是丢弃它们，可以使用 `qsappend` 标志。使用此标志时，重写引擎只是获取原始查询字符串并将其附加到重写中提供的任何新查询字符串。例如：

```apache
RewriteRule  ^index\.php$  index.php?foo=bar  [QSA]
```

如果使用 URL `index.php?moo=cow`，该规则会将 `index.php` 文件更改为 `index.php?foo=bar&moo=cow`。

如果原始 URL 中的查询字符串参数与 `RewriteRule` 中的参数名称相同，则原始值优先。

## 第 6 章

### noescape\NE

当 `*mod_rewrite*` 执行转换时，它会采取多种措施确保重写 URL 中的特殊字符在执行内部或外部重定向之前被转义。例如：

```apache
RewriteRule ^somedir/? index.php?page=foo\%3b [R]
```

基于此规则，Apache 会按请求将 `*somedir/*` 目录重定向，而 `*page*` 的 `$_GET` 值将是 `*foo\%3b*` 的“安全”转义值——`mod_rewrite` 对 `\%3b` 值进行了转义，而不是将其替换为其分号替代字符。若要告诉 `*mod_rewrite*` 避免任何自动转义，请启用 `noescape` 标志：

```apache
RewriteRule ^somedir/? index.php?page=foo\%3b [R,NE]
```

基于此规则，`*page*` 查询字符串参数的新值将为 `*foo*`。

### passthrough\PT

当你希望将 `*mod_rewrite*` 与其他提供类似 URL 处理功能的 Apache 模块（如 `*mod_alias*`）结合使用时，请使用 `passthrough` 标志。例如，如果你想将 `*/foo/*` 重写为指向 `*/bar/*`，然后使用 `*mod_alias*` 将 `*/bar/*` 转换为 `*/baz/*`，你可能会尝试以下设置：

```apache
RewriteRule ^/foo /bar
Alias /bar /baz
```

不幸的是，由于 Apache 内部处理 URL 的方式，上述写法无法正常工作。要使其生效，请添加 `passthrough` 标志：

```apache
RewriteRule ^/foo /bar [PT]
Alias /bar /baz
```

一般经验法则是：如果你使用多个 URL 转换模块来处理文件，请使用 `passthrough`。

### nosubreq\NS

使用 `nosubreq` 标志可以强制重写引擎在请求实际上是内部子请求时跳过该规则。在同时使用 PHP 和 Apache 时，很少需要此标志的情况。然而，在某些 CGI 脚本实例中，此标志会发挥作用。更多信息，请参阅 Apache 手册中关于 `RewriteRule` 的章节：`http://httpd.apache.org/docs/2.0/mod/mod_rewrite.html#rewriterule`。

### proxy\P

`proxy` 标志告诉重写引擎立即停止处理该规则集，并强制请求通过 Apache 代理模块 `mod_proxy` 处理。

鉴于 `RewriteRule` 受到了如此多的关注，你可能会认为它是 `mod_rewrite` 的主要动力。实际上，其最佳角色是与 `RewriteCond` 组成的动态双人组的一部分。

#### RewriteCond

`RewriteCond` 指令的行为很像 PHP 的 `if()` 语句：它将字符串与模式或条件进行测试。如果输入匹配模式或字符串，则紧跟在 `RewriteCond` 指令后面的 `RewriteRule` 将被处理。`RewriteCond` 的一般格式如下：

```apache
RewriteCond TestString CondPattern
```

`TestString` 是你正在评估的字符串，而 `CondPattern` 是要检查的正则表达式或比较值。

#### RewriteCond 用法
