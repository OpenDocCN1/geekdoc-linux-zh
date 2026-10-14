

用于连接远程 SSH 服务器的 SSH 客户端程序恰如其名，叫做 ssh。要连接到名为 remote-sys 的远程主机，我们会这样使用 ssh 客户端程序：

```
[me@linuxbox ~]$ ssh remote-sys
The authenticity of host 'remote-sys (192.168.1.4)' can't be established.
RSA key fingerprint is 41:ed:7a:df:23:19:bf:3c:a5:17:bc:61:b3:7f:d9:bb.
Are you sure you want to continue connecting (yes/no)?
```

第一次尝试连接时，会显示一条消息，指出无法验证远程主机的真实性。这是因为客户端程序以前从未见过该远程主机。要接受远程主机的凭证，请在提示时输入 yes。连接建立后，系统会提示用户输入密码：

```
Warning: Permanently added 'remote-sys,192.168.1.4' (RSA) to the list of known hosts.
me@remote-sys's password:
```

输入密码成功后，我们会收到来自远程系统的 shell 提示符：

```
Last login: Tue Aug 30 13:00:48 2011
[me@remote-sys ~]$
```

远程 shell 会话一直持续到用户在远程 shell 提示符下输入 exit 命令，从而关闭远程连接。此时，本地 shell 会话恢复，本地 shell 提示符重新出现。

也可以使用不同的用户名连接到远程系统。例如，如果本地用户 me 在远程系统上有一个名为 bob 的账户，用户 me 可以按如下方式登录远程系统上的 bob 账户：

```
[me@linuxbox ~]$ ssh bob@remote-sys
bob@remote-sys's password:
Last login: Tue Aug 30 13:03:21 2011
[bob@remote-sys ~]$
```

如前所述，ssh 会验证远程主机的真实性。如果远程主机未成功通过身份验证，则会出现以下消息：

```
[me@linuxbox ~]$ ssh remote-sys
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that the RSA host key has just been changed.
The fingerprint for the RSA key sent by the remote host is
41:ed:7a:fd:23:19:bf:3c:a5:17:7b:c1:63:b7:7f:d9:bb.
Please contact your system administrator.
Add correct host key in /home/me/.ssh/known_hosts to get rid of this message.
Offending key in /home/me/.ssh/known_hosts:1
RSA host key for remote-sys has changed and you have requested strict checking.
Host key verification failed.
```

此消息由两种可能情况之一引起。首先，攻击者可能正在尝试中间人攻击。这很少见，因为大家都知道 ssh 会提醒用户这一点。更可能的原因是远程系统以某种方式发生了变化；例如，其操作系统或 SSH 服务器已被重新安装。然而，出于安全和保障的考虑，不应轻易排除第一种可能性。当此消息出现时，务必与远程系统的管理员核实。

在确定消息是由于良性原因导致后，可以在客户端修复该问题。这是通过使用文本编辑器（例如 vim）从 ~/.ssh/known_hosts 文件中删除过时的密钥来完成的。在上面的示例消息中，我们看到：

```
Offending key in /home/me/.ssh/known_hosts:1
```

这意味着 known_hosts 文件的第 1 行包含有问题的密钥。从文件中删除该行，ssh 程序将能够接受来自远程系统的新身份验证凭证。

除了在远程系统上打开 shell 会话外，ssh 还允许我们在远程系统上执行单个命令。例如，我们可以在名为 remote-sys 的远程主机上执行 free 命令，并将结果显示在本地系统上：

```
[me@linuxbox ~]$ ssh remote-sys free
me@remote-sys's password:
             total       used       free     shared    buffers     cached
Mem:        775536     507184     268352          0     110068     154596
-/+ buffers/cache:           242520     533016
Swap:       1572856          0     1572856
[me@linuxbox ~]$
```

可以以更有趣的方式使用此技术，例如以下示例，我们在远程系统上执行 ls 并将输出重定向到本地系统上的文件：

```
[me@linuxbox ~]$ ssh remote-sys 'ls *' > dirlist.txt
me@remote-sys's password:
[me@linuxbox ~]$
```

注意使用了单引号。这样做是因为我们不希望在本地机器上执行路径名展开；而是希望在远程系统上执行。同样，如果我们希望输出

