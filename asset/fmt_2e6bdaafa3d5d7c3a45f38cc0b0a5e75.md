
When you know the name of a particular host, and you want to find the IP address that corresponds to it, there are a few things you can do.

### METHOD #1

To get the IP address of a host, `ping` the host in question; this will output the IP address of the host in parentheses (see Recipe 34.6.1 [Determining Whether a Host is Online], page 685).

### METHOD #2

Use `host` to get the IP address of the host whose name you give as an argument.

⇒ To get the IP address of `linart.net`, type:

```
$ host linart.net [RET]
```

**NOTES:** Depending on how the remote host is set up, this method may not work.

### METHOD #3

Use `dig`, the “domain information groper” tool, to get the IP address of a host. Give a hostname as an argument to output information about that host, including its IP address, in a section labeled `ANSWER SECTION`.

⇒ To find the IP address of the host `linart.net`, type:

```
$ dig linart.net [RET]
...output messages...
;; ANSWER SECTION:
linart.net.      1D IN A       64.240.156.195
...output messages...
$
```

In this example, `dig` output the IP address of `64.240.156.195` as the IP address for the host `linart.net`.

## 34.6.4 Getting the Hostname of an IP Address

When you know the IP address of a system, you can determine its full network name, or FQDN (“fully qualified domain name”). There are a few methods for this.

### METHOD #1

Use `host` to get the hostname of the system whose IP address you give as an argument.

⇒ To get the hostname of `127.0.0.1`, type:

```
$ host 127.0.0.1 [RET]
```

NOTES: Depending on how the remote host is set up, this method may not work.

### METHOD #2

To find the hostname for a given IP address, use `dig` with the `-x` option. Give an IP address as an argument to output information about that address, including its hostname in a section labeled `ANSWER SECTION`.

⇒ To find the hostname that corresponds to the IP address `152.2.210.81`, type:

```
$ dig -x 152.2.210.81 [RET]
...output messages...
;; ANSWER SECTION:
81.210.2.152.in-addr.arpa. 1D IN PTR metalab.unc.edu.
...output messages...
$
```

In this example, `dig` output that the FQDN corresponding to the given IP address was `metalab.unc.edu`.

## 34.6.5 Listing the Owner of a Domain Name

An Internet domain name's domain record contains contact information for the organization or individual that has registered that domain. Use the `whois` command to view the domain records for the common `.com`, `.org`, `.net`, and `.edu` top-level domains.

With only a domain name as an argument, `whois` outputs the name of the "Whois Server" that has that particular domain record. To output the domain record, specify the Whois Server to use as an argument to the `-h` option.

⇒ Here are two ways to use this.

- To output the name of the Whois Server for `columbia.edu`, type:

    ```
    $ whois columbia.edu [RET]
    ```

- To view the domain record for `columbia.edu`, using the `whois.educause.net` Whois Server, type:

    ```
    $ whois -h whois.educause.net columbia.edu [RET]
    ```

NOTES: This command also outputs the names of the nameservers that handle the given domain—this is useful to get an idea of where a particular Web site is hosted.

## 34.7 Chatting with Other Users

There are several ways to interactively chat with other users on the Internet, regardless of their platforms or operating systems. The following recipes describe the most popular tools and methods for doing this.

## 34.7.1 向另一用户的终端发送消息

有几种方法可以做到这一点，具体取决于你是向特定用户发送还是向所有用户发送。

### METHOD #1

使用 `write` 向另一用户的终端写入消息。将你想要写入的用户名作为参数给出。此命令会写入你提供的消息，并在前面加上一个标题行，表明以下内容是你发来的消息，并给出当前系统时间。它还会响起用户终端的铃声。

⇒ 要向用户 `sleepy` 登录的终端发送消息“Wake up!”，请输入：

```
$ write sleepy
Wake up!
^D
$
```

另一用户可以通过运行 `write` 并给出你的用户名作为参数来回复你。传统上，用户会在 `write` 消息末尾加上 `-o`，这表示他所说的内容“结束”了，现在轮到对方说话了。当用户认为对话已完成时，他会在一行末尾加上“oo”，意思是“结束并退出”。

### METHOD #2

类似的命令 `wall` 会将文本消息写入本地系统上的所有其他用户。它接受一个文本文件作为参数并输出该文件的内容；如果没有参数，则输出你输入的内容，直到你在单独一行输入 `CTRL-/D` 为止。它会在消息前加上文本“Broadcast message from username”（其中 username 是你的用户名），后跟当前系统时间，并响起它广播到的所有终端的铃声。

⇒ 以下是两种使用方法。
