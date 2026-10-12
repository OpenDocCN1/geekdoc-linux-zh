# ## Chapter 6

# **noescape**\NE

When *mod_rewrite* performs its transformations, it goes to great lengths to make sure special characters in the rewritten URL are escaped before performing any internal or external redirection. For example:

```
RewriteRule ^somedir/? index.php?page=foo\%3b [R]

```

Given this rule, Apache would redirect the *somedir/* directory as requested, and the `$_GET` value for *page* will be a “safe” escaped value of *foo\%3b* — *mod_rewrite* has escaped the `\%3b` value instead of replacing it with its semicolon substitute. To tell *mod_rewrite* to avoid any automatic escaping, you use the **noescape** flag:

```
RewriteRule ^somedir/? index.php?page=foo\%3b [R,NE]

```

Given this rule, the new value of the *page* query-string parameter will be *foo;*. `foo;`

# **passthrough**\PT

Use the **passthrough** flag when you want to combine *mod_rewrite* with other Apache modules that provide similar URL-handling functionality, such as *mod_alias*. For example, if you wanted to rewrite */foo/* to *point to /bar*, and then use *mod_alias* to translate */bar/* to */baz*, you might try the following:

```
RewriteRule ^/foo /bar
Alias /bar /baz

```

Unfortunately, because of the way Apache handles URLs internally, it would not work as written. To make it work, add the **passthrough** flag:

```
RewriteRule ^/foo /bar [PT]
Alias /bar /baz

```

A general rule of thumb is to use **passthrough** if you are using more than one URL translating module to process a file.

# **nosubreq**\NS

Use the **nosubreq** flag to force the rewrite engine to skip a rule if the request is actually an internal sub-request. When using PHP and Apache together, there are seldom situations when this flag is actually needed. There are, however, some CGI scripting instances where this flag comes into play. For more information, see the Apache manual section on *RewriteRule*: `http://httpd.apache.org/docs/2.0/mod/mod_rewrite.html#rewriterule`.

# **proxy**\P

The **proxy** flag tells the rewrite engine to stop processing the rule-set immediately and force the request through the Apache proxy module, *mod_proxy*.

With all this attention being given to *RewriteRule*, you might think that it’s the main force behind *mod_rewrite*. In reality, its best role is part of the dynamic duo that is *RewriteRule* and *RewriteCond*.