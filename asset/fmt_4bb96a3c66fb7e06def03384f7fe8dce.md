
`set subj=unknown`

`fi`

`fi`

`set bad=$i.bad`

`mv $tmp $i $bad | Mail -s \`

`"""WWW ERR: ${subj}: $bad" $email`

# 可以生成页面: set blockip.csh

`/bin/rm $tmp`

监控系统还对其他组件进行自动测试，例如电子邮件、填写各种表单、进行测试交易等。要测试“GET”风格的表单，使用 Netscape 填写表单并执行。当结果显示时，Netscape 会显示 URL，这将是 CGI 程序的名称，随后是 `?` 和由 `&` 分隔的表单变量。你突出这些数据并将其放入调用 `tcpread` 的脚本中。如果你的内容随时间变化，你将需要使用 `perl`、`sed`、`grep` 和 `awk` 的组合来过滤掉变化，以获得成功的 `diff`。

以下是一个典型的 URL 格式：

`http://www.cavu.com/cgi-bin/sunset?loctype=ID&loc=JFK&date=today`

突出这段文本中主机之后的部分；它将成为你想传递给 `tcpread` 的第二个参数。你需要选择一个文件来存储输出作为参考。之前讨论的脚本将无法处理此，因为 `?` 和 `&` 字符对 shell 来说是特殊的。当你将此参数传递给 `tcpread` 时，需要对其加引号 `""`。同样，可以通过生成电子邮件并读取 `/var/spool/mail/testusr` 电子邮件文件来测试电子邮件。

你可以变得更复杂，监控响应你查询的流量。因为你知道应该产生什么样的网络流量，你可以检测是否有一个带有你测试信用卡号的电子邮件被发送到了某些未知网站。

- [1] Attrition 组织监控网站篡改情况。此表摘录自 `http://www.attrition.org/mirror/attrition/os.html`

## 第 4 部分：从入侵中恢复

在这里你将学习如何从入侵中恢复。虽然遵循第一部分中关于使系统安全的建议可以阻挡大多数黑客并防止大多数系统被破解，但没有任何系统是完全安全的，就像没有程序可以保证没有 bug 一样。使用检测黑客对系统进行修改的技术来定期检查你的系统（也许每月一次）是一个好主意。这将捕获那些偶尔入侵但没有造成可见破坏的黑客。一位安全专家每六个月从头重新安装他的系统，以确保没有黑客可能“潜伏”其中。

现在可怕的时刻到了，你意识到你的系统可能已经被入侵了！与其恐慌，或看着 CNN 的头条关于你网站宕机数小时的新闻，而你抓着头接听来自总统的愤怒电话，不如你遵循了你的计划。在短时间内，黑客进入你系统的路径被找到了，漏洞被堵住，你的网站恢复了正常。这可能被归结为一个故障，并且几乎不予加考虑。

## 目录树

```csh
umask 077

foreach i ( `cat m_dirs` )
echo $i
mkdir i
end

exit
```

编译 `tcpwatch` 程序并将其放在你的个人 `bin` 目录。它让窃取 Web 页面变得太容易，因此不应该公开可用。

```csh
make tcpwatch
mv tcpwatch $HOME/bin/
```

使用此名为 `capture` 的脚本创建参考文件。我们允许每个文件有 120 秒的超时；希望你的网站比这快。错误日志将存放在 `capture.log` 文件中。

```csh
#!/bin/csh -f

umask 077

touch capture.log

foreach i ( `cat m_files` )
echo $i
tcpread www.pentac.com /$i 120 > ! $i
if ($status != 0 ) then
echo == COULD NOT CAPTURE $i \
tee -a capture.log
endif
```

```csh
end
echo ===== errors
cat capture.log
```

接下来的名为 `wwwscan` 的脚本将扫描静态 Web 页面，如果任何页面不匹配，将发送电子邮件。动态页面可以使用 `perl`、`sed` 等进行缓存，允许动态部分存在差异。为了安全起见，将最重要的页面静态化可能是值得的，这样就可以进行匹配测试。可以修改脚本以解析你的数据，甚至通过 SSH 连接到相应的系统并切换到 SecBack（安全备份）Web 服务器或在维修期间将其关闭。这些关闭操作仅适用于某些网站，因为瞬时的网络延迟可能会触发超时，而不是由于差异，而这可以控制锚点。

```csh
#!/bin/csh -f

# Copyright 2001 Bob Toxen. 保留所有权利。
# 此程序可以在 GNU
# 通用许可许可证第 2 版条款下使用。
#
# 提供的服务无任何形式的保证。

set email-admin@pentacorp.com joe@homesys.com
set tmp=$$
set host=www.pentacorp.com

foreach i ( `cat m_files` )
  echo $i
  tcpread -o -f $i $host /$i >&! $tmp
  set x=$status
  if ( $x != 0 ) then
    if ( $x == 1 ) then
      set subj=$diff
    else
      if ( $x == 4 ) then
        set subj=timeout
      else
        set subj=unknown
    fi
  fi
  set bad=$i.bad
  mv $tmp $i $bad | Mail -s \
  """WWW ERR: ${subj}: $bad" $email
```

# 可以生成页面: set blockip.csh

`/bin/rm $tmp`
