
```c
int PreeditStartCallback(ic, client_data, call_data);
```

- `ic` 指定输入上下文。
- `client_data` 指定额外的客户端数据。
- `call_data` 此回调未使用，且始终作为 `NULL` 传递。

当预编辑在指定的输入上开始时，回调带有 `NULL` 调用数据参数被调用。`PreeditStartCallback` 返回预编辑字符串允许的最大字节数，值 `-1` 表示无限制。

```c
void PreeditDoneCallback(ic, client_data, call_data);
```

- `ic` 指定输入上下文。
- `client_data` 指定额外的客户端数据。
- `call_data` 此回调未使用，且始终作为 `NULL` 传递。

当预编辑在指定的输入上停止时，回调带有 `NULL` 数据参数被调用。客户端可以释放由 `PreeditStartCallback` 分配的数据。

`PreeditStartCallback` 应初始化显示预编辑信息和处理 `PreeditDrawCallback` 调用所需的适当数据。一旦 `PreeditStartCallback` 被调用，在 `PreeditDoneCallback` 调用之前，它不会再次被调用。

## 预编辑绘图回调 (Preedit Draw Callback)

此回调被触发，用于在预编辑区域绘制并插入、删除或替换预编辑文本。预编辑文本可能包括未转换的文本（如日语假名）、已转换文本（如日语汉字）或这两种字符。该字符串是多字节或宽字符，其编码与输入上下文绑定的本地语言匹配。回调原型如下：

```c
void PreeditDrawCallback(ic, client_data, call_data);
```

## 区域与国际化文本函数

`client_data` 指定了额外的客户端数据。

`call_data` 指定了预编辑绘制信息。

回调函数通过 `call_data` 参数接收一个 `XIMPreeditDrawCallbackStruct` 结构。该结构体的 `text` 成员包含要绘制的文本。字符串绘制完成后，光标应移动到指定的位置。

`XIMPreeditDrawCallbackStruct` 结构体的定义如下：

```c
typedef struct _XIMPreeditDrawCallbackStruct {
    int *caret;         /* 预编辑字符串内的光标偏移 */
    int chg_first;      /* 开始更改的位置 */
    int chg_length;     /* 字符长度 */
    XIMText *text;
} XIMPreeditDrawCallbackStruct;
```

客户端必须通过引用缓冲区中的索引持续更新预编辑文本和回调参数。`call_data` 字段根据操作具有特定的含义，如下：

- 要删除文本，`call_data` 成员指定的文本字段为 `NULL`。要删除的文本是缓冲区中从 `chg_first` 位置（从 0 开始）开始、长度为 `chg_length` 的当前文本。
- 当文本非 `NULL` 时，表示在缓冲区中插入或替换文本。
- `chg_length` 标识当前预编辑缓冲区中受此调用影响的字符数量。正的 `chg_length` 表示从 `chg_first` 开始的 `chg_length` 个字符必须被删除，或必须被 `XIMText` 结构中指定长度的文本替换。
- `chg_length` 为 0 表示必须在 `chg_first` 指定的位置插入文本。`chg_first` 值为 0 指定缓冲区中的第一个字符。
- `chg_length` 和 `chg_first` 共同确定了对预编辑缓冲区所需的修改；从 `chg_first` 开始，将 `chg_length` 个字符替换为所提供的 `XIMText` 结构中的文本。例如，假设预编辑缓冲区包含字符串 "ABCDE"。

```text
Text:      A B C D E
           ^ ^ ^ ^ ^
CharPos:   0 1 2 3 4
```

图中的 `CharPos` 显示了字符相对于起始位置的位置。

- 如果 `chg_first` 的值为 1 且 `chg_length` 的值为 3，则表示从字符位置 1 开始替换 3 个字符为 `XIMText` 结构中的字符串。因此，BCD 将被结构中的值替换。
- 尽管 `chg_length` 和 `chg_first` 都是有符号整数，但它们的值永远不会为负。
- 光标标记标识了在预编辑缓冲区修改完成后，光标应该放置的字符位置之前。例如，如果 `caret` 为 0，光标位于缓冲区的开头。如果 `caret` 为 1，光标位于第一个和第二个字符之间。

```c
typedef struct _XIMText {
    unsigned short length;
    XIMFeedback * feedback;
    Bool encoding_is_wchar;
    union {
        char * multi_byte;
        wchar * wide_char;
    } string;
} XIMText;
```

传递的文本字符串实际上是一个定义如下的结构：

- `length` 成员是字符数长度。
- `encoding` 成员是一个值，指示文本字符串是按宽字符还是多字节格式编码的。文本字符串可以用多字节或宽字符的形式传递；由输入法控制数据传递的格式。客户端的回调程序必须能够处理这两种形式的数据。
- `string` 成员是文本字符串。
- `feedback` 成员指示字符串中每个字符的渲染类型。如果 `string` 为 `NULL`（表示仅更新现有预编辑缓冲区的高亮部分），则 `feedback` 指向应应用于现有预编辑缓冲区的长度高亮元素，从 `chg_first` 开始。

`feedback` 成员表示了回调函数在绘制文本时应该采用的渲染反馈类型。待绘制文本的渲染可以是通用方式（例如：主要的、次要的），也可以是特定方式（如反色、下划线）。当给出通用类型时，客户端可以自由选择渲染样式。然而，必须将主要（primary）和次要（secondary）映射到两种不同的渲染样式。

如果输入法想要控制预编辑字符串的显示，输入法可以通过特定方式使用 `feedback` 指示可见性提示。`XIMVisibleToForward`、`XIMVisibleToBackward` 和 `XIMVisibleToCenter` 掩码专门用于这些可见性提示。`XIMVisibleToForward` 提示文本最好从预编辑区域的光标位置向前沿主绘制方向显示。`XIMVisibleToBackward` 掩码表示预编辑最好相对于主绘制方向，从预编辑区域的光标位置向后显示。`XIMVisibleToCenter` 标记表示预编辑最好以预编辑区域的光标位置为中心显示。

`feedback` 成员还指定了如何执行对文本参数的渲染。其用法与编辑缓冲区中的周围字符相同；如果 `chg_first` 是高亮位置，客户端可以选择使用两种高亮中的某一种。如果 `feedback` 不为 `NULL`，则 `feedback` 指定了一个数组，定义了字符串中每个字符的渲染，该数组的长度即为

如果输入法想要指示它正在[高亮]...

```c
typedef unsigned long XIMFeedback;

#define XIMReverse             1
#define XIMUnderline          1<<1
#define XIMHighlight           1<<2
#define XIMPrimary            1<<3
#define XIMSecondary          1<<4
#define XIMTertiary           1<<5
#define XIMVisibleToForward   1<<6
#define XIMVisibleToBackward  1<<7
#define XIMVisibleToCenter    1<<8
```
