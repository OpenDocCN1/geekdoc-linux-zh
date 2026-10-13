
# 检查子系统是否已经启动。

``` 
subsys=${i#/etc/rcrunlevel.d/K?} && \
  [ ! -f /var/lock/subsystem/$subsystem ] && continue
```

# 停止子系统。

```
if grep -q "(killproc action)" $i; then
  stop
else
  action "Stopping $subsystem" $i stop
fi
```
done
fi

```

# 现在运行启动脚本。

```
for i in /etc/rc$runlevel.d/*; do
  # 检查脚本是否存在。
  [ ! -f $i ] && continue

  # 不运行 [KS]*.(rpmsave,rpmorig) 脚本
  [ "${i}.rpmsave" != "$i" ] && continue
  [ "${i}.rpmorig" != "$i" ] && continue
  [ "${i}.rpmnew" != "$i" ] && continue

  # 检查子系统是否已经启动。
  subsys=$(ls $i/etc/rc$runlevel.d/???)
  [ -f /var/lock/subsystem/$subsystem ] || \
    [ -f /var/lock/subsystem/($subsystem).init ] && continue

  # 如果处于确认模式，则获取用户确认
  [ -n "$CONFIRM" ] && \
    confirm $subsys
  case $? in
    0)
      ;;
    2)
      CONFIRM=
      continue
      ;;
  esac

  # 启动子系统。
  if egrep "$(daemon action)" $i ; then
    if [ "$subsys" = "halt" -o "$subsys" = "reboot" ]; then
      unset LANG
      unset LC_ALL
      unset TEXTDOMAIN
      unset TEXTDOMAINDIR
      exec $i start
    else
      $i start
    fi
  else
    if [ "$subsys" = "halt" -o "$subsys" = "reboot" ]; then
      if [ "$subsys" = "single" -o "$subsys" = "local" ]; then
        if [ "$subsys" = "halt" -o "$subsys" = "reboot" ]; then
          unset LANG
          unset LC_ALL
          unset TEXTDOMAIN
          unset TEXTDOMAINDIR
          exec $i start
        else
          $i start
          action "Starting $subsys" $i
        fi
      fi
    fi
done
```

与 `initab` 文件一样，以 `#` 字符开头的行被视为注释。嗯，几乎如此。第一行表示将运行一个唯一的 `/bin/bash` 实例来执行该脚本。第一行非注释行处理过去、现在和未来的运行级别。变量 `argv` 取了第一个（也是唯一的）命令行参数（`$1`）的值。这代表了期望的运行级别。`set` 命令将 `runlevel` 命令的输出（在本节稍后会解释）放入 `$1` 和 `$2` 中，然后分发到 `previous`（上一个运行级别）和 `runlevel`（当前运行级别）变量。

下一行读取 `/etc/init.d/functions`，它包含了几个 shell 代码段（例如 `action`、`killproc` 和 `confirm` 子程序），为从 rc 脚本启动的每个进程提供一致的接口。

如果在启动时向引导加载器传递了 `confirm` 选项，服务器进程将在未经过系统控制台用户确认的情况下启动。这段代码块检查进程是否需要确认，并相应地设置 `CONFIRM` 变量。

在下一行中，如果第一部分评估为真 (`0`)（`$1` 的值不等于空字符串），则执行它。`runlevel` 变量被设置为存储在变量 `$1` 中的期望运行级别。

与下一行的方式相同，如果目录 `/var/run` 存在，则创建或覆盖 `/var/run/runlevel.dir`。该文件将包含即将执行的命令（例如 `/etc/rc3.d`）的目录名称。

如果在启动时向引导加载器传递了 `confirm` 选项，服务器进程将在未经过系统控制台用户确认的情况下启动。这段代码块检查进程是否需要确认，并相应地设置 `CONFIRM` 变量。

在下一行中，如果第一部分评估为真 (`0`)（`$1` 的值不等于空字符串），则执行它。`runlevel` 变量被设置为存储在变量 `$1` 中的期望运行级别。

与下一行的方式相同，如果目录 `/var/run` 存在，则创建或覆盖 `/var/run/runlevel.dir`。该文件将包含即将执行的命令（例如 `/etc/rc3.d`）的目录名称。

如果在启动时向引导加载器传递了 `confirm` 选项，服务器进程将在未经过系统控制台用户确认的情况下启动。这段代码块检查进程是否需要确认，并相应地设置 `CONFIRM` 变量。

在下一行中，如果第一部分评估为真 (`0`)（`$1` 的值不等于空字符串），则执行它。`runlevel` 变量被设置为存储在变量 `$1` 中的期望运行级别。

与下一行的方式相同，如果目录 `/var/run` 存在，则创建或覆盖 `/var/run/runlevel.dir`。该文件将包含即将执行的命令（例如 `/etc/rc3.d`）的目录名称。

如果在启动时向引导加载器传递了 `confirm` 选项，服务器进程将在未经过系统控制台用户确认的情况下启动。这段代码块检查进程是否需要确认，并相应地设置 `CONFIRM` 变量。

在下一行中，如果第一部分评估为真 (`0`)（`$1` 的值不等于空字符串），则执行它。`runlevel` 变量被设置为存储在变量 `$1` 中的期望运行级别。

与下一行的方式相同，如果目录 `/var/run` 存在，则创建或覆盖 `/var/run/runlevel.dir`。该文件将包含即将执行的命令（例如 `/etc/rc3.d`）的目录名称。

如果在启动时向引导加载器传递了 `confirm` 选项，服务器进程将在未经过系统控制台用户确认的情况下启动。这段代码块检查进程是否需要确认，并相应地设置 `CONFIRM` 变量。

在下一行中，如果第一部分评估为真 (`0`)（`$1` 的值不等于空字符串），则执行它。`runlevel` 变量被设置为存储在变量 `$1` 中的期望运行级别。

与下一行的方式相同，如果目录 `/var/run` 存在，则创建或覆盖 `/var/run/runlevel.dir`。该文件将包含即将执行的命令（例如 `/etc/rc3.d`）的目录名称。

如果在启动时向引导加载器传递了 `confirm` 选项，服务器进程将在未经过系统控制台用户确认的情况下启动。这段代码块检查进程是否需要确认，并相应地设置 `CONFIRM` 变量。

在下一行中，如果第一部分评估为真 (`0`)（`$1` 的值不等于空字符串），则执行它。`runlevel` 变量被设置为存储在变量 `$1` 中的期望运行级别。

与下一行的方式相同，如果目录 `/var/run` 存在，则创建或覆盖 `/var/run/runlevel.dir`。该文件将包含即将执行的命令（例如 `/etc/rc3.d`）的目录名称。

如果在启动时向引导加载器传递了 `confirm` 选项，服务器进程将在未经过系统控制台用户确认的情况下启动。这段代码块检查进程是否需要确认，并相应地设置 `CONFIRM` 变量。

在下一行中，如果第一部分评估为真 (`0`)（`$1` 的值不等于空字符串），则执行它。`runlevel` 变量被设置为存储在变量 `$1` 中的期望运行级别。

与下一行的方式相同，如果目录 `/var/run` 存在，则创建或覆盖 `/var/run/runlevel.dir`。该文件将包含即将执行的命令（例如 `/etc/rc3.d`）的目录名称。
