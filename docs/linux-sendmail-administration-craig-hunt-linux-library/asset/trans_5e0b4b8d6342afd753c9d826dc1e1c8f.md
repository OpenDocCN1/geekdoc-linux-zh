
输出文件。因此，在 `Build` 命令命令行中放置 `test.cf` 意味着使用 `test.mc` 来创建 `test.cf`。

尽管 `Build` 命令非常简单，但我从未用过它来构建 Sendmail 配置，你可能也不会这样做。我不使用它的原因是，用于构建 Sendmail 配置的 `m4` 命令也同样简单。对于普通的 Sendmail 管理员来说，`Build` 脚本并没有提供任何显著的优势。该脚本存在此目录中的真实目的是为了让维护 Sendmail 的人员能够方便地通过一个命令构建多个 `.cf` 文件。这对于源码维护者非常有帮助，因为正如我们所看到的，每当 Sendmail 升级到与 Sendmail 系统预期的版本号兼容的配置版本号时，都需要重新构建 Sendmail 配置文件。`Build` 有四个关键字参数，可以实现一个命令构建多个配置文件：

- generic: `generic` 关键字为通用的宏配置文件构建对应的 `.cf` 文件。这些是通常随 Sendmail 发行版一起附带唯一 `.cf` 文件。
- berkeley: `berkeley` 关键字构建在 Berkeley 使用的 16 个配置文件。由于 Berkeley 配置仅作为示例使用，这些配置的 `.cf` 文件大多没有构建。
- other: `other` 关键字构建 `Makefile` 中 `$OTHER` 变量列出的任何配置。在 Sendmail 8.11 中，该变量中只有一个配置，且它不是以 .cf 文件的形式交付的。
- all: `all` 关键字构建 `Makefile` 中 `$GENERIC`、`$BERKELEY` 和 `$OTHER` 变量定义的所有配置。

如果你需要构建多个配置，可以编辑 `Makefile`，更改 `$OTHER` 变量使其包含所有配置的名称，并使用 `Build` 一次创建你所有的配置。这是可行的，但不太可能。大多数 Sendmail 管理员并没有足够的配置来费费精力于此。我们不再再次提到 `Build`。在本书的其余部分中，将直接使用 `m4` 命令来构建 Sendmail 配置文件。

`cf/domain` 目录是你最可能添加配置文件的两个目录。其余四个目录都用于构建配置，但你使用的是其中已经存在的文件。你不太会在这些目录中添加或更改文件。

##  ostype 目录

每个宏配置文件必须包含一个 `OSTYPE` 命令，用于处理来自 `cf/ostype` 目录的宏源文件。该目录中的文件定义了特定操作 Sendmail操作特性。列表 4.4 显示了 `ostype` 目录的内容。

### 列表 4.4 cf/ostype 目录

```
[craig]$ ls -ostype
aix2.m4 bsd2di.0.m4 irix5.m4 sunos4.1.m4
aix3.m4 darwin.m4 irix6.m4 qnx.m4 svr4.m4
aix4.m4 dugux.m4 isc4.1.m4 riscos4.5.m4 ultrix4.m4
altos.m4 domains.m4 linux.m4 sco-uw-2.1.m4 uicware7.7
amahl-uts.m4 dynx3.2.m4 maxion.m4 sc03.2.m4 unknown.
aux.m4 gnu.m4 mklinux.m4 sinix.m4 uxpdps.m4
bsd3.m4 hpux10.m4 nextstep.m4 solaris2.m4
bsd4.m4 hpux11.m4 openbsd.m4 solaris2..m4
bsdi.m4 osfl.m4 solaris2.pres.m4
bsd1.0.m4 irix4.m4 powerux.m4 sunos3.5.m4
```

该目录包含了 40 多个不同操作系统的配置文件。Solaris、BSD、Linux——它们都在这里，并且可以通过名称轻松识别。事实上，`ostype` 目录中的操作系统定义远比 `/cf/cf` 目录中的通用宏配置文件要多得多。让我感到稍微惊讶的一点是，这里没有 `redhat.` 或 `slackware.`。不同的 Linux 发行版之间的差异至少和 `AI4` 一样大，但不同的 Linux 供应商并没有创建 `OSTYPE` 文件。但这并不重要。你可以从标准的 Linux `OSTYPE` 开始，并在你在 `/cf/cf` 目录中构建的宏配置文件进行所有的自定义。

## mail 目录

除了 `OSTYPE` 命令外，每个可用的服务器配置必须至少有一个 `MAILER` 命令。`MAILER` 命令处理来自 `/cf/mailer` 的源文件。`mail` 目录中的每个文件都包含一组 mailers 的定义。列表 4.5 显示了随 Sendmail 8.11 交付的 mailer 定义。

### 列表 4.5 cf/mailer 目录的内容

```
[craig]$ ls -mailer
cyrus.m4 local.m4 phquery.m4 procmail.m4 smtp.m4 uuc.m4
```

该目录包含了 11 组不同 mailers 的定义。在本文章节中，我们只使用了两个最基本的组：`local.m4` 和 `smtp.m4`。

每个宏配置文件必须包含一个 `OSTYPE` 命令，用于处理来自 `cf/ostype` 目录的宏源文件。该目录中的文件定义了特定操作 Sendmail操作特性。列表 4.4 显示了 `ostype` 目录的内容。

### 列表 4.4 cf/ostype 目录



该目录包含了 11 组不同 mailers 的定义。在本文章节中，我们只使用了两个最基本的组：`local.m4` 和 `smtp.m4`。

[/content] (注：由于提供的原文文本中存在大量重复和乱码片段，译文已根据“不要重复输出原文”的原则进行了去重和清理翻译)

**更正后的基于逻辑的翻译：**

[content]
##  ostype 目录

每个宏配置文件必须包含一个 `OSTYPE` 命令，用于处理来自 `cf/ostype` 目录的宏源文件。该目录中的文件定义了特定操作 Sendmail操作特性。列表 4.4 显示了 `ostype` 目录的内容。

### 列表 4.4 cf/ostype 目录

```
[craig]$ ls -ostype
aix2.m4 bsd2di.0.m4 irix5.m4 sunos4.1.m4
aix3.m4 darwin.m4 irix6.m4 qnx.m4 svr4.m4
aix4.m4 dugux.m4 isc4.1.m4 riscos4.5.m4 ultrix4.m4
altos.m4 domains.m4 linux.m4 sco-uw-2.1.m4 uicware7.7
amahl-uts.m4 dynx3.2.m4 maxion.m4 sc03.2.m4 unknown.
aux.m4 gnu.m4 mklinux.m4 sinix.m4 uxpdps.m4
bsd3.m4 hpux10.m4 nextstep.m4 solaris2.m4
bsd4.m4 hpux11.m4 openbsd.m4 solaris2..m4
bsdi.m4 osfl.m4 solaris2.pres.m4
bsd1.0.m4 irix4.m4 powerux.m4 sunos3.5.m4
```

该目录包含了 40 多个不同操作系统的配置文件。Solaris、BSD、Linux——它们都在这里，并且可以通过名称轻松识别。事实上，`ostype` 目录中的操作系统定义远比 `/cf/cf` 目录中的通用宏配置文件要多得多。让我感到稍微惊讶的一点是，这里没有 `redhat.` 或 `slackware.`。不同的 Linux 发行版之间的差异至少和 `AI4` 一样大，但不同的 Linux 供应商并没有创建 `OSTYPE` 文件。但这并不重要。你可以从标准的 Linux `OSTYPE` 开始，并在你在 `/cf/cf` 目录中构建的宏配置文件进行所有的自定义。

## mail 目录

除了 `OSTYPE` 命令外，每个可用的服务器配置必须至少有一个 `MAILER` 命令。`MAILER` 命令处理来自 `/cf/mailer` 的源文件。`mail` 目录中的每个文件都包含一组 mailers 的定义。列表 4.5 显示了随 Sendmail 8.11 交付的 mailer 定义。

### 列表 4.5 cf/mailer 目录的内容

```
[craig]$ ls -mailer
cyrus.m4 local.m4 phquery.m4 procmail.m4 smtp.m4 uuc.m4
```

该目录包含了 11 组不同 mailers 的定义。在本文章节中，我们只使用了两个最基本的组：`local.m4` 和 `smtp.m4`。
