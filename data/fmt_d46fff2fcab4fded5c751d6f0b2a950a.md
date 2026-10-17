
```
    fi

  done

  /usr/sbin/sendmail {"$DAEMON" -yes } & echo \

  $[ -n$QUEUE" ] && echo -q$QUEUE

  RETVAL=$?

  echo

  [ $RETVAL -eq 0 ] && touch /var/lock/subsystem/sendmail

stop)

  # 停止守护进程。

  echo "Shutting down sendmail:"

  killproc sendmail

  RETVAL=$?

  echo

  [ $RETVAL -eq 0 ] && rm -f /var/lock/subsystem/sendmail

restart(reload)

  $0 stop

  $0 start

  ;;

status)

  RETVAL=$$

  ; status sendmail

  ;;

*)

  echo "Usage: sendmail [start|stop|restart][status]"

  exit 1

  ;;

esac

exit $RETVAL
```

© Copyright 1999-2000 Gerhard Maurani and Open Network Architecture ®

关于此书的意见和建议请邮件至 `gmourani@videotron.ca`

现在，让此脚本具有执行权限并更改其默认权限：
`[root@deep] # chmod 700 /etc/rc.d/init.d/sendmail`

使用以下命令为 Sendmail 创建符号 rc ：
`[root@deep] # chkconfig --add sendmail`

使用以下命令手动启动你的 Sendmail 服务器：
`[root@deep] # /etc/rc.d/init.d/sendmail start`
Starting sendmail.

# 工作后的清理

```bash
[root@deep] # cd /var/tmp

[root@deep] # rm -rf sendmail-version/ sendmail.version.tar.gz
```
