
该示例展示了构建 `sendmail.cf` 文件时使用的 `m4` 命令格式。`../m4/cf.m4` 是构建 `sendmail.cf` 文件所需的 `m4` 源码树的路径。如果该路径没有通过 `include` 命令包含在宏配置中，则必须在 `m4` 命令行指定。请注意，路径名是以 `../` 开头的相对路径。旧版本的 `m4` 实际上需要相对路径。更改到 `/cf` 目录并不是为了方便，而是使用正确源路径运行 `m4` 的必要部分。在 Linux 下构建的 GNU `m4` 程序可以接受此参数的绝对路径，这意味着宏配置文件可以存储在任何地方。Red Hat 在通过 RPM 安装 Sendmail 时利用了这一点。RPM 将 Red Hat 配置文件的副本存放在 `/etc/mail` 中，并在宏配置文件包含了指向 `cf.m4` 的绝对路径。

第二个命令行参数是新宏配置文件的文件名 `test.mc`。`m4` 读取源文件 `../m4/cf.m4` 和 `test.mc`，并输出测试文件。`m4` 命令生成的输出符合 `sendmail.cf` 文件的正确格式。

## 测试配置文件的兼容性

`test.cf` 是成为 `sendmail.cf` 文件的正确格式。在移动到 `/etc/mail/sendmail.cf` 之前，你应该确保它可以正常工作。如列表 4.9 所示，快速测试可以告诉你结果。

### 列表 4.9 测试兼容性

```
[]# sendmail -v -t -C /etc/sendmail.cf

Warning: .cf file is out of date: sendmail 8.11.0 supports

version 9, .cf file is version 8

^nD

No recipient addresses found in header

[]# sendmail -v -t -C ./test.cf

nD

No recipient addresses found in header
```

如列表 4.9 所示，新的 `test.cf` 配置解决了我们在编译新源码升级 Sendmail 时出现的兼容性问题。该测试没有证明其他任何，我不会假装这个简单的配置是最好的配置，但它实现了我们让 Sendmail 运行起来的目标。

## 安装新配置

一旦你决定使用新的配置文件，请将其移动到 Sendmail 期望查找配置的位置。Sendmail 8.11 的配置文件默认名为 `/etc/mail/sendmail.cf`。在大多数 Linux 系统上，配置文件为 `/etc/sendmail.cf`。将新文件放在你系统的相应位置。在本示例中，我们使用默认设置从源码编译了 Sendmail 8.11，因此我们需要将 `test.cf` 移动到 `/etc/mail/sendmail.cf`，我们在列表 4.10 中进行了操作。

### 列表 4.10 将新配置文件就位

```
[root] mv /etc/mail/sendmail.cf /etc/mail/sendmail.cf.hold

mv: /etc/mail/sendmail.cf: No such file or directory

[root] cp test.cf /etc/mail/sendmail.cf

[root] sendmail -v -

To: craig@wren.foobirds.org

From: craig

Subject: Test

Please ignore this test.

^^

craig@wren.foobirds.org: Connecting to wren.foobirds.org. via smtp-

220 wren.foobirds.org ESMP Sendmail 8.11.0/8.11.0;

Tue, 29 Aug 2000 20:42:44 -00

400

>>> EHLO From:<craig@ibis.foobirds.org>

250-wren.foobirds.org Hello root@almond.com [172.16.12.1]

pleased to meet you

>>> MAIL From:<craig@ibis.foobirds.org> SIZE=78

250 2.1.0 <craig@ibis.foobirds.org>... Sender ok

>>> RCPT To:<craig@wren.foobirds.org>...

250 2.1.5 <craig@wren.foobirds.org>... Recipient ok

>>> DATA

354 Enter mail, end with "." on a line by itself

2n02n0 eU0f0
```

# 第 4 章 创建基础 Sendmail 配置

可以使用以下 `m4` 命令对 `test.mc` 文件处理：

```
[root]# m4 test.mc > test2.cf
```
