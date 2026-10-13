
```
echo "c. OpenWin"; echo ""

echo -n Choice:"

set choice=

if [ $choice == "a" ]; then

  set path=$path $X11PATH

  setenv LD_LIBRARY_PATH ${X11LIBPATH}:$usr/lib:/usr/lib

  cp .xinitrc .xinitrc

  xinit

elsel [ $choice == "b" ]; then

  tcs

elif [ $choice == "c" ]; then

  setenv OPENHOME=/usr/openwin

  setenv OPENWIN=/usr/openwin/bin

  setenv LD_LIBRARY_PATH ${OPENHOME}:$usr/lib:/usr/local/lib

  set path=$OPENWIN $path

  cp .xinitrc-openwin .xinitrc

  cp open

else

  echo "请选择 a, b, 或 c。"

  goto ask

endif
```

# 退出 X11 或其他内容后跳转到这里

`goto exit`

```
else
# 如果我们不在控制台上，假设 X11 可以用，将登录
#记录在 .loginfile 中，设置终端的清除功能以配合我的
# 普通终端删除键，并继续连接
setenv LD_LIBRARY_PATH ${X11LIBPATH}:$usr/lib:/usr/local/lib
echo "remotlogin" -> $(date) >> .loginfile
```

```bash
echo "...远程登录..."; echo '
stty erase '?'
tcsh
goto exit2
```

```bash
exit:
# 执行一些小动作，比如在控制台上加载图像，记录
# 注销，并跳转到注销
echo "退出"
screenload -b i plumd $HOME/junk/AMG-ld5.ras
echo "logout ->" 'date' >> .logfile
done done
```

```bash
exit2:
# 相同，只是我们在远程，所以我们不弄
# 本地显示
echo "... 远程注销..."; echo
echo "remotelogout ->" 'date' >> .logfile
done
```

```bash
done:
# 输出一些内容，以便知道我们脚本执行到了这里，
# 然后退出
echo "离线"
logout
```

# 配置 csh

更多的 csh 文件。我将其作为系统级全局配置，补充用户的 `.cshrc`。

`/usr/local/extras/csh_extensions` 包含了所有用户可能需要的配置和路径。我使用它来配置通常通用的路径和环境变量，这样我就不需要为每个用户单独配置。`/usr/local/extras/csh_extensions` 包含了所有用户可能需要的配置和路径。我使用它来配置通常通用的路径和环境变量，这样我就不需要为每个用户单独配置。`/usr/local/extras/csh_extensions` 包含了所有用户可能需要的配置和路径。我使用它来配置通常通用的路径和环境变量，这样我就不需要为每个用户单独配置。`/usr/local/extras/csh_extensions` 包含了所有用户可能需要的配置和路径。我使用它来配置通常通用的路径和环境变量，这样我就不需要为每个用户单独配置。

通常通用的路径和环境变量，`path`

# 包含了所有用户可能需要的配置和路径

不需要为每个用户单独配置。`/usr/local/extras/csh_extensions` 包含了所有用户可能需要的配置和路径。我使用它来配置通常通用的路径和环境变量，这样我就不需要为每个用户单独配置。`/usr/local/extras/csh_extensions` 包含了所有用户可能需要的配置和路径。我使用它来配置通常通用的路径和环境变量，这样我就不需要为每个用户单独配置。`/usr/local/extras/csh_extensions` 包含了所有用户可能需要的配置和路径。我使用它来配置通常通用的路径和环境变量，这样我就不需要为每个用户单独配置。`/usr/local/extras/csh_extensions` 包含了所有用户可能需要的配置和路径。我使用它来配置通常通用的路径和环境变量，这样我就不需要为每个用户单独配置。

# 包含了所有用户可能需要的配置和路径

不需要为每个用户单独配置。`/usr/local/extras/csh_extensions` 包含了所有用户可能需要的配置和路径。我使用它来配置通常通用的路径和环境变量，这样我就不需要为每个用户单独配置。`/usr/local/extras/csh_extensions` 包含了所有用户可能需要的配置和路径。我使用它来配置通常通用的路径和环境变量，这样我就不需要为每个用户单独配置。`/usr/local/extras/csh_extensions` 包含了所有用户可能需要的配置和路径。我使用它来配置通常通用的路径和环境变量，这样我就不需要为每个用户单独配置。

# 包含了所有用户可能需要的配置和路径

不需要为每个用户单独配置。`/usr/local/extras/csh_extensions` 包含了所有用户可能需要的配置和路径。我使用它来配置通常通用的路径和环境变量，这样我就不需要为每个用户单独配置。`/usr/local/extras/csh_extensions` 包含了所有用户可能需要的配置和路径。我使用它来配置通常通用的路径和环境变量，这样我就不需要为每个用户单独配置。

# 包含了所有用户可能需要的配置和路径

不需要为每个用户单独配置。`/usr/local/extras/csh_extensions` 包含了所有用户可能需要的配置和路径。我使用它来配置通常通用的路径和环境变量，这样我就不需要为每个用户单独配置。

# 包含了所有用户可能需要的配置和路径

不需要为每个用户单独配置。`/usr/local/extras/csh_extensions` 包含了所有用户可能需要的配置和路径。我使用它来配置通常通用的路径和环境变量，这样我就不需要为每个用户单独配置。

# 包含了所有用户可能需要的配置和路径

不需要为每个用户单独配置。`/usr/local/extras/csh_extensions` 包含了所有用户可能需要的配置和路径。我使用它来配置通常通用的路径和环境变量，这样我就不需要为每个用户单独配置。

# 包含了所有用户可能需要的配置和路径

不需要为每个用户单独配置。`/usr/local/extras/csh_extensions` 包含了所有用户可能需要的配置和路径。我使用它来配置通常通用的路径和环境变量，这样我就不需要为每个用户单独配置。

# 包含了所有用户可能需要的配置和路径

不需要为每个用户单独配置。`/usr/local/extras/csh_extensions` 包含了所有用户可能需要的配置和路径。我使用它来配置通常通用的路径和环境变量，这样我就不需要为每个用户单独配置。

# 配置环境

将这些配置放在你的登录中。

# .xinitrc-X11

# 有用文件

```
#!/bin/sh
xrdb -merge $HOME/.X11defaults
timeout 5 off
```

# .xinitrc-openwin

# 配置环境

```bash
# 设置 LD_LIBRARY_PATH 以让程序可以找到共享库
set MANPATH:/usr/share/man

# 配置环境
将这些配置放在你的登录中。

# .xinitrc-X11

# 有用文件
```

# 防止邮件陷入无限循环并发送给自己。

# 邮件最终通过发送给表观用户 "test-outgoing" 来处理，

# 在此情况下，该用户由 /etc/aliases 中的一个条目处理。

:0

```bash
! "FROM DAEMON"
! *X-Loop: test@banana.biosci.ohio-state.edu
! *TO
! formail -f -k -r -b \
! -A "X-Loop: test@banana.biosci.ohio-state.edu \
! -I"Reply-To: test@banana.biosci.ohio-state.edu \
! -I "To: test@banana.biosci.ohio-state.edu \
! -I "From: "Subject"
! formail -u Subject" -I "References" \
! #SENDMAIL -o1 test-outgoing
```

# 真正的处理程序。/etc/aliases 中的一个条目将邮件

# 转发到 mboy-trans@banana.biosci.ohio-state.edu 的此账户。

# 该例程捕获邮件，防止其自我循环通信，

# 调整头信息并发送。
