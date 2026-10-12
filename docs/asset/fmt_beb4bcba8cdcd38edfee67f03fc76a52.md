
* `"Chinese"`, `"简体"`, `"简体*"`,

* 如果你有任何一个中文字体，这里应该能识别它：

* `"GB2312"`, `"gb"`, `"..."`,

* `"GB2312"`, `"gb2312.1980-0"`, `"song ti"`,

;

程序的后续部分包含了实现表格布局的数据结构声明和函数实现。从国际化（`I118N`）的角度来看，这些内容毫无趣味，在这里被省略了。

英语字体在几个子程序中使用。为了方便程序员，它是被硬编码并声明为全局变量的。这里还声明了一个从字符编码注册表和字体族构建 `XLFD` 的工具程序：

> /*
>
> 这些无聊的内容
>
> 全局变量是邪恶的，但我很懒。
>
> */

```
char *makeXLFD = "-*Helvetica-medium-r-*-24-*-100-100-*-iso8859-1;";
XFontStruct *englishFont = NULL;
```

> /*
>
> 工具类函数声明
>
> */

```
char *makeXLFD(char*, char*);
```

接下来是 `I118N` 相关的函数实现。`utfToNative` 如我们之前看到的，使用了 `iconv`。但有一个转折，由于 `iconv(3)` 设计用于用于处理外部流：

> /* LangRec 方法实现 */
>
> /*
>
> ```
> utfToNative()
> 更基础的 iconv 操作
> ```
>
> # 第 28 章
>
> ```
> unsigned UTNBFSZ 256
> char *utfToNbytes(const char *source, const char *icon_charset);
>
> char *buffer = malloc (UTNBFSZ);
> char *const retbuf = buffer;
>
> size_t ssz = strlen(source);
> size_t bsz = UTNBFSZ;
>
> iconv_t cd = iconv_open(icon_charset, "UTF-8");
>
> if (cd != (iconv_t)-1)
> && iconv(cd, source, &ssz, buffer, &bsz) != (size_t) (-1)
>     *buffer = 0;
> iconv_close(cd);
> ```
>
> 这里事情变得复杂了。日本工业标准 `JIS X 0208` 为日语定义了一组包含约 6000 个字符的基础字符集，以及一种与 `ISO 2022` 标准兼容的双字节编码。这使得日语等语言能够以一种本质的方式使用多字节编码：不同的字节表示不同的字符。双字节字符是日语，单字节字符是 `JIS X 0201` 的 `ASCII`（它是 `ISO 646` 的日语版本，与 `ASCII` 有三个字符不同）。`ISO 2022` 提供了两种方法将字符与全 `ASCII` 字符（后者是日语字符的一半）区分：要么使用高位来指示字符集（高位置1为日语），要么使用转义序列。高位通过 `EUC-JP` 编码实现，而转义序列方法通过 `ISO-2022-JP` 实现：`iconv(3)` 可以产生两者。
>
> 遗憾的是，`X11` 文本渲染函数无法处理其中任何一种。它们会忽略转义序列中的初始 `ESC` 字符，但会打印可打印字符。因此，`ISO-2022-JP` 不能直接传递给函数。另一方面，`EUC-JP` 是不可接受的，因为为 `X11` 提供的日语字体使用的编码期望每个字节都在 `0x21` 到 `0x7E` 范围内，而 `EUC-JP` 日语字符使用的字节在 `0xA1` 到 `0xFE` 范围内。
>
> 本程序使用 `iconv(3)` 输出亚洲语言的 `EUC` 编码，并掩盖高位以符合该代码所预期的格式。这是目前 `I18N` 程序面临的典型障碍类型。这些问题正在改进，但事实仍然是，即使对于一个良好国际化的应用程序，针对某些文化的本地化可能仍需要对代码进行“手术”。一旦你处理了这些，你就可以将这些代码放入工具箱供下一个项目使用。点在于，`I18N` 例程的实现必须暴露给程序员，这破坏了封装性并丢失了面向对象编程的一些优势。现在你可以使用 `Unicode` 作为一个很好的字体选择，因为许多语言使用相同的字符，但通常对美观有不同的想法。中文字符可能没有安装看起来像日语的字体，或者即使安装了，优先级也很低。在像这样的一个多语言应用程序中，这个问题是非常真实的。
>
> ```
> if (strcmp(iconv_charset, "EUC-JP") != 0)
>     for (buffer = retbuf; *buffer; ++buffer)
>         *buffer &= 127;
> return retbuf;
>
> printf(stderr, "iconv failed for %s\n", iconv_charset);
> iconv_close(cd);
> return NULL;
> ```
>
> */
>
> /* LangRec 方法实现 */
>
> `int langRecValidP(LangRec *lr)`
>
> (
>
> /* 是我太懒了还是怎么？ */
>
> `return 1;`
>
> )
>
> `char *englishName(LangRec *lr)`
>
> (
>
> `return lr->english;`
>
> )
>
> `char *nativeName(LangRec *lr)`
>
> (
>
> `return utfToNative(lr->native, lr->iconv_char);`
>
> )
>
> `char *nativeHello(LangRec *lr)`
>
> (
>
> `return utfToNative(lr->hello, lr->iconv_char);`
>
> )
>
> /* `m17n.c` 结束 */
