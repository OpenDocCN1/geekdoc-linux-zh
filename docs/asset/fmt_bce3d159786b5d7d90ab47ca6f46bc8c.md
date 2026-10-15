
`char *XSetOCValues(oc);`

指定设置 XOC 值的变长参数列表。

如果没有发生错误，`XSetOCValues` 返回 `NULL`；否则返回第一个无法设置的参数名称。某个参数可能无法设置：

- 该参数是只读的。
- 参数名称不受识别。
- 发生了取决于实现的错误。

每个要设置的值必须是适当的数据，与参数要求的数据类型匹配。

`XSetOCValues` 可以产生 `BadAtom` 错误。

要获取 XOC 值，请使用 `XGetOCValues`。

`char *XGetOCValues(oc);`

`oc` 指定输出上下文。

... 指定获取 XOC 值的变长参数。

如果发生错误，`XGetOCValues` 函数返回 `NULL`；否则返回第一个无法获取的参数名称。由于以下原因，可能无法获取参数：

- 参数名称不被识别。
- 发生了取决于实现的错误。

名称后的每个参数必须指向存储值的位置。

# 输出上下文值

第一表描述了输出方法如何解释 XOC 值。第一列列出 XOC 值。第二列指示了理想情况下工作且为了兼容之前的版本提供的备选接口。第三列指示了每个 XOC 值的处理方式。

以下键适用于此表。

| 键 | 解释 |
| :--- | :--- |
| C | 此值必须通过 `XCreateOC` 设置。 |
| D | 此值可以使用 `XCreateOC` 设置。如果未设置，则提供默认值。 |
| G | 此值可以使用 `XGetOCValues` 读取。 |
| S | 此值必须通过 `XSetOCValues` 设置。 |

| XOC 值 | 备选接口 | 键 |
| :--- | :--- | :--- |
| BaseName | `XCreateFontSet` | C-G |
| MissingCharset | `XCreateFontSet` | G |
| DefaultString | `XCreateFontSet` | G |
| Orientation | - | D-S-G |
| ResourceName | - | S-G |
| ResourceClass | - | S-G |
| FontInfo | `XFontsOfFontSet` | G |
| OMAAutomatic | - | G |

# 基础字体名称

`XBaseFontName` 参数是基础字体名称列表，Xlib 使用它来加载区域（locale）所需的字体。基础字体名称是用逗号分隔的列表。字符串以空字符终止，并假设采用主机可移植字符编码（Host Portable Character Encoding）；否则，结果取决于实现。空格字符两侧紧邻空白会被忽略。

使用 XLFD 字体名称允许 Xlib 从单个不依赖于区域的基础字体名称中获取各种区域所需的字体。单个基础字体名称应命名一个字体族，其成员在这些区域所需的各种字符集中均有编码。

XLFD 基础字体名称可以显式地为区域指定字符集。这允许用户为区域请求的字符集指定精确的字体，从而完全控制选择。

如果基础字体名称不是 XLFD，Xlib 将尝试从字体的属性中获取 XLFD 名称。如果 Xlib 成功，`XGetOCValues` 函数将返回此 XLFD 名称，而不是客户端提供的名称。

此参数必须在创建时设置且不能更改。如果任何所需的字符集不存在字体，或者如果 Xlib 中的区域定义要求特定字符集存在字体但未找到该字符集的字体，则 `XCreate` 返回 `NULL`。

当查询 `XBaseFontName` XOC 值时，`XGetOCValues` 返回一个空终止的字符串，即 Xlib 用于加载区域所需字体的基础字体名称。该字符串由 Xlib 所有，客户端不应对其进行修改或释放。该字符串将通过对关联 XOC 调用 `XDestroyOC` 来释放。Xlib 不会修改字符串的内容。

# 缺失字符集

`XMissingCharSet` 参数返回字体缺失的必需字符集列表。参数的值是指指向 `XCharSetList` 结构的指针。

如果当前区域所需的所有字符集都存在字体，则参数值设置为 `NULL`；如果一个或多个必需字符集不存在字体，则字符列表设置为以空终止的字符集名称，且字符计数设置为缺失字符集的数量。这些字符集是区域编码的必需字符集，Xlib 可能映射。

缺失字符列表由 Xlib 所有，客户端不应对其进行修改或释放。它将通过对关联 XOC 调用 `XDestroyOC` 来释放。

# 默认字符串

当在具有缺失字符集的 XOC 上调用绘图或测量函数时，区域中的某些字符将不可绘制。`XDefaultString` 参数返回一个指针，表示用该 XOC 绘制的字符串。该字符串并不一定由当前区域的有效字符组成，也不一定用加载的字体绘制，但客户端可以绘制或测量包括该字符串的字符。

如果 `XDefaultString` 返回空字符串（`""`），则间距为零。该字符串由 Xlib 所有，客户端不应对其进行修改或释放。它将通过对关联 XOC 调用 `XDestroyOC` 来释放。Xlib 不会修改其内容。

## 方向

当 `XNOrientation` 参数的值为指定 `XOrientation` 参数的函数返回的值之一时，它指定文本的当前方向。参数值类型为 `XOrientation`。当设置 `XNORientation` 时，该值指定当前方向。当设置 `XOrientation_context` 时，文本方向根据取决于实现的方法确定（例如 ISO 6429 控制序列），且区域相关 Xlib 函数的初始文本方向假设为 `Orientation_LTR_TTB`。

`XNORientation` 值不会改变 Xlib 绘图函数的原始绘图方向。

## 资源名称与类

`XNResourceName` 和 `XNResourceClass` 参数是获取输出上下文资源的完整名称和类的字符串。在查找可能随输出上下文变化的资源时，这些值应作为名称和类的前缀。如果未设置这些值，资源将无法完全指定。

当查询 `XNResourceName` 或 `XNResourceClass` 值时，`XGetInputValue` 返回一个空终止字符串。该字符串由 Xlib 所有，客户端不应对其进行修改或释放。它将在对关联 XOC 调用 `XDestroyOC` 或通过 `XGetInputValue` 更改关联值时释放。

# 字体信息

`XNFontInfo` 参数指定了一个或多个 `XFontStruct` 结构列表以及用于给定输出上下文绘图的字体名称。参数的值是指指向 `XOMInfo` 类型结构体的指针。

```
typedef struct {
```

## 区域设置与国际化文本函数

```
int            num_font;

XFontStruct   **font_struct_list;

char            **font_name_list;

} XOMFontInfo;
```
