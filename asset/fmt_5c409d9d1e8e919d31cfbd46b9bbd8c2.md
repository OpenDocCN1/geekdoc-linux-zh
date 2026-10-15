
# ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)

Enter `<ruleset> <address>`

```
> 3.0 kabir@nitec.com.
rewrite: ruleset 3 input: kabir @ nitec . com
rewrite: ruleset 96 input: kabir < @ nitec . com >
rewrite: ruleset 96 returns: kabir < @ ad-engine . com >
rewrite: ruleset 3 returns: kabir < @ ad-engine . com >
rewrite: ruleset 0 input: kabir < @ ad-engine . com >
rewrite: ruleset 199 input: kabir < @ ad-engine . com >
rewrite: ruleset 199 returns: kabir < @ ad-engine .com
rewrite: ruleset 98 input: kabir @ nitec .com
rewrite: ruleset 98 returns: kabir @ nitec .com
rewrite: ruleset 198 input: kabir @ nitec: kabir @ nitec .com
rewrite: ruleset 198 returns: $$ local $: kabir @ nitec .com
rewrite: ruleset 0 returns: $$ local $: kabir @ nitec .com
```

正如你所看到的，`kabir@nitec.com` 地址是通过本地邮件传输器投递的。考虑另一个例子。假设你有以下 `/etc/mail/domaintable` 映射：

```
ad-engine.com nitec.com
```

因此，任何发往 `ad-engine.com` 的邮件都应该重路由到 `nitec.com`。这里是一个测试：

# ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)

Enter `<ruleset> <address>`

```
> 3.0 kabir@nitec.com.
rewrite: ruleset 3 input: kabir @ nitec . com
rewrite: ruleset 96 input: kabir < @ nitec . com >
rewrite: ruleset 96 returns: kabir < @ ad-engine . com >
rewrite: ruleset 3 returns: kabir < @ ad-engine . com >
rewrite: ruleset 0 input: kabir < @ ad-engine . com >
rewrite: ruleset 199 input: kabir < @ ad-engine . com >
rewrite: ruleset 199 returns: kabir < @ ad-engine .com
rewrite: ruleset 98 input: kabir @ nitec .com
rewrite: ruleset 98 returns: kabir @ nitec .com
rewrite: ruleset 198 input: kabir @ nitec: kabir @ nitec .com
rewrite: ruleset 198 returns: $$ local $: kabir @ nitec .com
rewrite: ruleset 0 returns: $$ local $: kabir @ nitec .com
```

正如你所看到的，`kabir@nitec.com` 地址是通过本地邮件传输器投递的。考虑另一个例子。假设你有以下 `/etc/mail/domaintable` 映射：

```
ad-engine.com nitec.com
```

因此，任何发往 `ad-engine.com` 的邮件都应该重路由到 `nitec.com`。这里是一个测试：

# ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)

Enter `<ruleset> <address>`

```
> 3.0 kabir@nitec.com.
rewrite: ruleset 3 input: kabir @ nitec . com
rewrite: ruleset 96 input: kabir < @ nitec . com >
rewrite: ruleset 96 returns: kabir < @ ad-engine . com >
rewrite: ruleset 3 returns: kabir < @ ad-engine . com >
rewrite: ruleset 0 input: kabir < @ ad-engine . com >
rewrite: ruleset 199 input: kabir < @ ad-engine . com >
rewrite: ruleset 199 returns: kabir < @ ad-engine .com
rewrite: ruleset 98 input: kabir @ nitec .com
rewrite: ruleset 98 returns: kabir @ nitec .com
rewrite: ruleset 198 input: kabir @ nitec: kabir @ nitec .com
rewrite: ruleset 198 returns: $$ local $: kabir @ nitec .com
rewrite: ruleset 0 returns: $$ local $: kabir @ nitec .com
```

正如你所看到的，`kabir@nitec.com` 地址是通过本地邮件传输器投递的。考虑另一个例子。假设你有以下 `/etc/mail/domaintable` 映射：

```
ad-engine.com nitec.com
```

因此，任何发往 `ad-engine.com` 的邮件都应该重路由到 `nitec.com`。这里是一个测试：

# ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)

Enter `<ruleset> <address>`

```
> 3.0 kabir@nitec.com.
rewrite: ruleset 3 input: kabir @ nitec . com
rewrite: ruleset 96 input: kabir < @ nitec . com >
rewrite: ruleset 96 returns: kabir < @ ad-engine . com >
rewrite: ruleset 3 returns: kabir < @ ad-engine . com >
rewrite: ruleset 0 input: kabir < @ ad-engine . com >
rewrite: ruleset 199 input: kabir < @ ad-engine . com >
rewrite: ruleset 199 returns: kabir < @ ad-engine .com
rewrite: ruleset 98 input: kabir @ nitec .com
rewrite: ruleset 98 returns: kabir @ nitec .com
rewrite: ruleset 198 input: kabir @ nitec: kabir @ nitec .com
rewrite: ruleset 198 returns: $$ local $: kabir @ nitec .com
rewrite: ruleset 0 returns: $$ local $: kabir @ nitec .com
```

正如你所看到的，`kabir@nitec.com` 地址是通过本地邮件传输器投递的。考虑另一个例子。假设你有以下 `/etc/mail/domaintable` 映射：

```
ad-engine.com nitec.com
```

因此，任何发往 `ad-engine.com` 的邮件都应该重路由到 `nitec.com`。这里是一个测试：

# ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)

Enter `<ruleset> <address>`
