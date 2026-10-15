
![](img/66f6e6c242a0e6a79aeee4012c6ff547_730_0.png)

# 收尾工作
第六部分

当你需要引用此节时，使用`<ref>tag:frobcation>`获取更多信息。

另见`<ref id="frobcation" name="Frobcation">`（如 HTML），读者将激活链接跳转到标记的章节。`name` 元素会插入章节名称，并适用于不支持超文本链接的文档。

自然，你还可以使用`<url>` 标签插入 URL 元素。此功能专门针对万维网，并支持标准的 HTML 文档、通过 FTP 获取的文件、`mailto:` 以及 URL 等。格式

你可以在`<url url="www.somdomain.com/frobcation.html" name="Frobcation">` 中了解更多关于 frobation 的信息。

此示例中的 `name` 元素将被渲染为指向 URL 的 HTML 超文本链接。为了支持 HTML，使用`<html>...` 格式，由于你想要... 元素，你也可以插入 URL 元素。对于不支持...链接的文档，`name` 元素会存在。实际上，使用`<html>...` 格式：

# 文档
第 38 章

| 行号 | 内容 |
| :--- | :--- |
| 55 | `<sect>ENVIRONMENT` |
| 56 | `<p>` |
| 57 | `<bf>&dollar;CF_BLEND</bf>` 将此变量设置为你偏好的混合比例。等同于 `<bf>coffee -b &dollar;CF_BLEND</bf>`。 |
| 58 | |
| 59 | | |
| 60 | `<sect>DIAGNOSTICS` |
| 61 | `<p>` |
| 62 | 无。此节仅用于说明目的。 |
| 63 | | |
| 64 | `<sect>SEE ALSO` |
| 65 | `<p>` |
| 66 | `<bf>creamer(1)</bf>`, `<bf>grind(1)</bf>`, `<bf>sweetener(1)</bf>` |
| 67 | | |
| 68 | `<sect>NOTES` |
| 69 | `<p>` |
| 70 | 如果有任何注释，将将在这里。 |
| 71 | | |
| 72 | `<sect>AUTHOR` |
| 73 | Kurt Wall `<kwall@xmission.com>` |
| 74 | | |
| 75 | `<sect>BUGS` |
| 76 | 如果全豆库为空，你必须离开椅子。向同一设备队列的多个连续请求可能会导致溢出。 |
| 77 | | |
| 78 | `</article>` |

在最后的摘录中，使用了`</article>` 标签来标记 SGML 解析器文档已结束。CD-ROM 包含了完整的 SGML 源文件 `coffee.sgml`，以及几个输出版本：HTML、LaTeX、LyX 和 RTF（富文本格式）。

## SGML-tools 标签

SGML-tools 并不限于上一个示例所示的标签。本节描述了内部交叉引用、URL 引用、两种列表以及索引生成。

创建指向文档其他部分的内部交叉引用非常费力。假设你有一个标题为“Frobication”的章节。要创建一个交叉引用——

```
<sect1>Frobication<label id="frobication">
```

![](img/66f6e6c242a0e6a79aeee4012c6ff547_730_0.png)

# 收尾工作
第六部分

当你需要引用此节时，使用`<ref>tag:frobcation>`获取更多信息。

另见`<ref id="frobcation" name="Frobcation">`（如 HTML），读者将激活链接跳转到标记的章节。`name` 元素会插入章节名称，并适用于不支持超文本链接的文档。

自然，你还可以使用`<url>` 标签插入 URL 元素。此功能专门针对万维网，并支持标准的 HTML 文档、通过 FTP 获取的文件、`mailto:` 以及 URL 等。格式

你可以在`<url url="www.somdomain.com/frobcation.html" name="Frobcation">` 中了解更多关于 frobation 的信息。

此示例中的 `name` 元素将被渲染为指向 URL 的 HTML 超文本链接。为了支持 HTML，使用`<html>...` 格式，由于你想要... 元素，你也可以插入 URL 元素。对于不支持...链接的文档，`name` 元素会存在。实际上，使用`<html>...` 格式：

# MIT 许可证 许可证

对于受 MIT 许可证保护的软件，其唯一条件是版权通知和免责声明不得更改或删除，并且必须出现在所有软件副本中。派生作品（部分基于受 MIT 许可证保护的应用程序）在未经作者事先许可的情况下，不得使用作者的名字来推销派生作品。

下面是 MIT 许可证的模板。在自己的项目中使用此模板时，请将 `<year>` 和 `<copyright holders>` 替换为相应文本。

## MIT 许可证

```
Copyright (c) <year> <copyright holders>

特此授予任何获得本软件及相关文档（下称“软件”）副本的人员免费许可对软件进行任何处理，包括但不限于使用、复制、修改、合并、发布、分发、许可和/或出售软件的权利，并允许以下条件：

在软件的所有副本或重大部分中，必须包含本版权声明和本免责声明。

根据本许可提供的软件“按原”提供，不提供任何形式的证言，无论是明示还是隐含的，包括但不限于对特定目的的适用性和无故障的保证。

在任何情况下，作者或版权持有者均 LIABLE FOR ANY CLAIM, DAMAGES 或 OTHER LIABILITY（包括, 但 NOT LIMITED TO DIRECT, INDIRECT, SPECIAL, INCIDENTAL 或 CONSEQUENTIAL DAMAGES）承担任何责任，无论是 IN AN ACTION OF CONTRACT, TORT, 或 OTHERWISE， ARISING OUT OF 或 IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE。
```

上述版权声明和本许可声明应包含在软件的所有副本或大部分部分中。

本软件按“现状”提供，不提供任何形式的保证，无论是明确还是暗示的，包括但不限于对适销性、针对特定用途的适用性以及不侵权的保证。在任何情况下，作者或版权持有者均不对任何索赔、损害或其他责任不承担责任，无论是由于合同诉讼、侵权诉讼或其他诉讼，而是由于本软件或对软件的使用或其他处理而引起的或与之相关的责任。

## BSD 风格许可

BSD 衍生许可比 MIT 类许可仅略微具有限制性。软件无论是以二进制形式还是源代码形式，均可不受限制地使用和分发，前提是满足以下条件：

- 原始版权声明和免责声明既不被修改也不被删除。
- 未经事先许可，不得使用原作者的名字来推广衍生作品。
- 任何针对衍生作品的广告材料必须包含对原作者的承认。

下方以模板形式包含了 BSD 风格许可副本。要从此模板生成您自己的许可，请将 `<owner>`、`<organization>` 和 `<year>` 替换为适当的值。

### BSD 许可

```
<owner>

<organization>

<year>
```
