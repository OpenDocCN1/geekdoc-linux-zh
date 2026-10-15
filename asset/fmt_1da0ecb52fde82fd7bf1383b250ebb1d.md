
`rndc` 使用 TCP 连接（端口 953）与 `named` 通信；为了进行身份验证，它使用加密密钥在通过网络将命令发送给 `named` 之前对其进行数字签名。默认配置文件 `/etc/rndc.conf` 必须指定要通信的服务器，以及在与其通信时对应的密钥（该密钥必须被 `named` 识别）。

目前 `named` 支持的身份验证机制是使用经过 HMAC-MD5 算法加密的密钥，并在 `rndc` 和 `named` 之间共享。生成密钥的最简单方法是使用 `dnssec-keygen` 工具。在以下示例中，你正在请求工具生成一个名为 `rndc` 的 128 位用户密钥：

```bash
$ dnssec-keygen -a hmac-md5 -b 128 -n user rndc
Krndc.+157+14529
```

该工具分别创建两个带有 `.key` 和 `.private` 扩展的文件。`.private` 文件中的 `Key:` 行告诉了 `rndc` 和 `named` 需要共享的密钥（`mkDd2F1HMFe1Jqx1/z4cfw=`）。当我们有了它后，就可以设置一个非常简单的 `/etc/rndc.conf`：

```
/etc/rndc.conf
-------
# 与名称服务器 "localhost" 通信时使用名为 "rndc" 的键
server localhost { 
    key               rndc;
}

# 这里是关于名为 "rndc" 的键的细节
key rndc {
    algorithm           HMAC-MD5;
    secret              "mkDd2F1HMFe1Jqx1/z4cfw=";
}

# 默认
options {
    default-server     localhost;
    default-key        rndc;
}
```

该文件需要包含三个部分：

- `server` 部分定义了一个名称服务器（localhost），并指定了与其通信时使用的键（rndc）。
- `key` 部分包含了一些关于键的细节，由 `dnssec-keygen` 生成。当我们设置 `named` 时，我们需要告诉它关于键的相同信息，以便它能够验证 `rndc` 发出的请求。
- `options` 部分设置了合理的默认值（因为文件可能会列出多个服务器和键）。

如果需要，`rndc(8)` 和 `rndc.conf(5)` 帮助页包含更多信息。

## named.conf

接下来你必须配置 `named` 本身。它的单一配置文件（`/etc/named.conf`）语法与 `rndc.conf` 非常相似：此部分仅描述了对于配置功能性名称服务器至关重要的一小部分配置指令。如需更详细的参考，请参阅 BIND 9 ARM（管理员参考手册）；它随 BIND 一起发布，Red Hat 7.3 将安装安装 `/usr/share/doc/bind-9.2.1/arm/` 下。

`named.conf` 文件中的 `options` 和 `named` 部分是绝对必要的。`options` 部分必须告诉 `named` 区域文件存放的位置，并且 `named` 必须知道在哪里找到根区域（`*`）。我们还设置了一个 `controls` 部分，允许接受来自 `rndc` 的经过验证命令。由于客户端（特别是 `nslookup`）依赖于解析名称服务器的 IP，我们还设置了 `0.0.127.in-addr.arpa` 反向区域。

我们从类似这样的配置文件开始：

```
/etc/named.conf
options {
    # 这里是存放区域文件的地方
    directory "/var/named";
}

# 允许运行在 localhost 上的 rndc 向我们发送命令
controls {
    inet 127.0.0.1 {
        allow { 127.0.0.1; }
        keys { rndc };
    }
}

# 与 rndc.conf 中指定的相同信息
key rndc {
    algorithm hmac-md5;
    secret "mKKd2FiHMFe1JQ1/z4cfw==";
}

# 关于根区域的信息
zone ".*" {
    type hint;
    file "root.hints";
}

# 许多软件依赖于能够解析 127.0.0.1
zone "0.0.127.in-addr.arpa" {
    type master;
    file "rev/127.0.0.0";
}
```

`options` 部分是我们指定 `named` 应该查找区域文件的目录的地方（如文件中其他部分命名的）。你将在本章随后的示例中学习如何使用其他选项。

接下来，我们指示 `named` 接受来自经过验证的 `rndc` 的命令。我们添加了一个 `key` 部分，与那个 `rndc.conf` 完全相同，以及一个 `controls` 部分，说明 `rndc` 将从 `localhost` 连接并使用指定的键。（你可以在 `allow` 列表中指定多个 IP 地址，或者像“安全”章节中描述的那样使用访问控制列表。）

`*` 区域告诉 `named` 关于 `root.hints` 文件中带有名称和地址的根服务器的信息。这些信息决定了最初查询哪一个根服务器（该决定通常会根据服务器的响应进行频繁修订）。虽然可以通过 FTP 获取提示文件，但推荐的、对网络友好的保持其同步的方法是使用 `dig`。我们向一个根名称服务器（哪一个都行）请求 `.` 的 NS 记录，并使用 `dig` 的输出：

```
/var/named/root.hints

# dig @j.root-servers.net > /var/named/root.hints
# cat /var/named/root.hints
| << dig 8.2 << @root-servers.net . ns
| (1 server found)
| ;; res options: init recurs defnam dnsrch
| ;; get answer:
| ;; >>HEADER<< opcode: QUERY, status: NOERROR, id: 6
| ;; flags: ra rr rd; QUERY: 1, ANSWER: 13, AUTHORITY: 0, ADDITIONAL: 13
| ;; QUERY SECTION: | ;; type = NS, class = IN

| ;; ANSWER SECTION:
| 60 IN NS H.ROOT-SERVERS.NET.
| 60 IN NS C.ROOT-SERVERS.NET.
| 60 IN NS G.ROOT-SERVERS.NET.
| 60 IN NS F.ROOT-SERVERS.NET.
| 60 IN NS B.ROOT-SERVERS.NET.
| 60 IN NS J.ROOT-SERVERS.NET.
| 60 IN NS K.ROOT-SERVERS.NET.
| 60 IN NS L.ROOT-SERVERS.NET.
| 60 IN NS M.ROOT-SERVERS.NET.
| 60 IN NS I.ROOT-SERVERS.NET.
| 60 IN NS E.ROOT-SERVERS.NET.
| 60 IN NS D.ROOT-SERVERS.NET.
| 60 IN NS A.ROOT-SERVERS.NET.
| ;; ADDITIONAL:
| 60 IN NS H.ROOT-SERVERS.NET.
| 60 IN NS C.ROOT-SERVERS.NET.
| 60 IN NS G.ROOT-SERVERS.NET.
| 60 IN NS F.ROOT-SERVERS.NET.
| 60 IN NS B.ROOT-SERVERS.NET.
| 60 IN NS J.ROOT-SERVERS.NET.
| 60 IN NS K.ROOT-SERVERS.NET.
| 60 IN NS L.ROOT-SERVERS.NET.
| 60 IN NS M.ROOT-SERVERS.NET.
| 60 IN NS I.ROOT-SERVERS.NET.
| 60 IN NS E.ROOT-SERVERS.NET.
| 60 IN NS D.ROOT-SERVERS.NET.
| 60 IN NS A.ROOT-SERVERS.NET.
```
