
然而，这些错误信息可能会产生误导。通常，属性上缺少引号或 dhtml 标签末尾缺少右括号，就会导致剩余的 dhtml 代码被忽略。在这种情况下，实际发生错误的标签并不是错误信息中指定的那个标签。例如，看这段错误的 dhtml 代码：

```html
<html-if name="today">
  Yesterday was <dhtml-var expr="(today-1).day()>
</dhtml-if>
```

在第 2 行中，`expr` 属性的末尾缺少了引号。然而，当你尝试保存此代码时，Zope 返回的错误是：

`No closing tag, for tag dhtml-if name="today", in line 1`

如你所见，第 3 行确实包含第 1 行 dhtml-if 的结束标签。问题在于，Zope 认为这一行是第 2 行 `expr` 属性值的一部分，因为在 `day()` 之后没有结束引号，所以 Zope 不再识别第 3 行视为 dhtml 标签。

## 16.2.2 调试模式

当在 Zope 中激活调试模式时（即使用默认的 Zope 启动脚本），你将在错误页面文本之后看到错误的回溯（traceback）。否则，回溯将显示在页面的 HTML 源代码中，你可以通过右键点击错误页面并选择“查看页面源代码”或“查看框架源代码”来查看。

回溯显示了从导致异常的模块（始终是回溯底部的文件）到控制 Zope 输出的模块的执行路径，以及在错误发生时在每个模块中执行的对象或表达式。（关于异常的更详细描述请见下文 16.3.1 节。）

在 DHTML 错误的情况下，最终模块始终是

```python
/usr/local/Zope-x.x.x/src/lib/python/DocumentTemplate/DT_String.py,
```

如图 16-1 所示。不幸的是，这使得回溯对于调试 DHTML 的用性降低。错误信息和回溯中显示的对象必须足以定位错误所在。

你可以通过安装 ZDebug 产品来极大增强 Zope 错误信息提供的信息。尽管在编写本文时它仍在开发中，但它仍然是一个非常有用的调试工具。可以从 http://www.zope.org/Members/hathazard/ZDebug 下载。

## 16.3 Zope 特有错误

表 16-2 中列出的错误信息是 Zope 特有的。

表 16-2：Zope 特有错误信息

| 错误 | 解释 |
| --- | --- |
| Bad Request | 输入了无效请求。 |
| CopyError | 无法复制对象。 |
| DateTimeError | 日期或时间格式存在错误。 |
| Forbidden | 此操作被禁止。 |
| HistorySelectionError | 在处理历史函数时发生错误。 |
| InError | 在处理 In 标签时发生错误。 |
| Invalid Object Name | 在模块中未找到对象。 |
| Invalid Permission | 权限无效。 |
| MailHostError | 发生了特定的邮件主机的错误。 |
| ModuleError | 无法访问该模块。 |
| ParseError | DTML 对象发生语法错误。 |
| SuperCannotOwn | 超级用户不能拥有对象。 |
| Time Error | 指定了无效的时间。 |
| Type Errors | 此类型已存在。 |
| Unauthorized | 尝试未经授权使用或访问对象。 |
| UndoError | 在撤销操作期间发生错误。 |
| ValidationError | 参数无效。 |
| VersionError | 在使用版本函数时发生错误。 |

## 16.3.1 Zope 错误信息

以下是实际操作中一些 Zope 错误信息的示例：

AttributeError

无法访问对象的属性。

```
Error Type : AttributeError
Error Value : 'string' object has no attribute x
```

解释：尝试在字符串中调用属性 `x`，但没有该名称的属性。如果属性存在但它是对象的私有属性且未通过 Zope 发布，也会发生此错误。

> 当你处理 Zope 时，AttributeError 和 SystemError 发生得更频繁，但它们实际上属于标准的 Python 错误。

## Bad Request

此类错误表示 HTTP 请求无效，例如：

Error Value: the id ___ contains characters illegal in URLs.

解释：指定的 id 包含 URL 中的非法字符。

Error Value: the id index html is invalid - it is already in use.

解释：尝试分配已存在的 id 名称（在此例中：index_html）。

## CopyError

你无法复制对象。这可能是因为你想要复制的对象不允许复制，或者你想要复制到的对象无法接受新对象。

The object ___ does not support this operation.

解释：所选对象不支持复制。

Cannot paste into this object.

解释：你无法将此对象粘贴到此文件夹对象中，因为它无法包含你剪板中的对象类型。

## DateTimeError:

指定的时区不存在，或指定的时间格式错误。

Unrecognized timezone

解释：使用的时区不被识别。

Unknown time zone in date

解释：指定的日期包含不存在或不支持的时间格式。

Invalid date

解释：指定的日期格式无效。

## Forbidden

某操作被禁止。这可能是因为用户没有适当的权限。

Zape Error
Error Type : Forbidden
Error Value : You are not authorized

## SelectionError

所选的操作无法执行（见 3.1.5 节历史管理）。

No historical revision was selected.
解释：未选择历史版本。

Only one historical revision can be copied to the present.
解释：只能复制一个历史版本到当前。

Only two historical revisions can be compared.
解释：只能比较两个历史版本。

## InError

处理 In 标签时出现问题。见 4.13.10 节，“In 标签”。

Error Value: Strings are not allowed as input to tag.
解释：不允许将字符串作为 tag 的输入。

## Invalid Object Name

在指定的模块中找不到对象或方法。例如，假设你创建一个外部方法，但编写的 Python 模块名称错误或当前不在扩展目录中。

指定的对象 `test_obj` 未在模块中找到。

## KeyError

当尝试使用 `[...]` 符号从命名空间访问对象时，如果找不到名称，就会发生此错误。此错误也发生在尝试查找字典或映射对象（如 Zope 文件夹或 REQUEST 对象）时。

命名空间未找到键。可能是输入错误或不存在。

检查错误信息中列出的变量的拼写。记住 Zope 和 Python 的名称是区分大小写的。

## MailHostError

通过 MailHost 对象发送电子邮件时发生错误。更多信息请见 4.3.12 节，“Sendmail 标签”。

No mailhost was not specified in tag

解释：Sendmail 标签中未指定邮件主机。

An unsupported encoding was specified in tag

解释：encode 参数设置了错误或不支持的值。

## Module Error

无法访问模块。

指定的模块 `TestModule` 未找到。
指定的模块 `TestModule` 无法打开。

解释：此错误发生在你尝试创建一个外部方法，但编写的 Python 模块名称错误或当前不在扩展目录中。

## ParseError

当你尝试保存包含错误的对象（DTML 方法或 DTML 文档）时，会发生解析错误。在解决任何解析错误之前，无法保存对象，例如：

unexpected end tag

解释：存在一个不需要或位置错误的结束标签。

+   解释：单个 if tag 对应了多个 else tag
No more than one else block is allowed

+   解释：if 块中使用了两个或多个 else tag。
The __ attribute was used but neither of start、end 或 size

