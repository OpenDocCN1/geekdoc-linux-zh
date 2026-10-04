

## A.2.2.3 tree 标签

### tree 标签的属性

| 名称 | 解释 |
|---|---|
| name | 参见表 4.1 中的 "name 属性"。 |
| expr | 参见表 4.1 中的 "Expr 属性"。 |
| branches | 用于查找子对象的方法名。默认值是 `tpValues`，这是一个查找类文件夹对象的方法。`objectValues` 方法查找另一个对象下的所有对象和子对象。该值必须是一个方法名。 |
| branches_expr | 一个用于求值以查找子对象的表达式。该属性的功能与 `branches` 属性相同，但它接收到的值是一个表达式而不是方法名。 |
| id | 用于确定对象 ld（逻辑标识）以计算树状态的方法或属性名。默认方法是 `tpld`。 |
| url | 用于确定对象 URL的方法或属性名。默认方法是 `tpURL`。 |
| leaves | 使用 "leaves" 来展开不包含子对象的对象的文档名称。 |
| header | 在任何分支展开上方显示的的文档名称。这允许你在层级结构中“标记”分支。 |
| footer | 每次显示的文档名称 |
| nowrap | 0 或 1。如果为 0，当分支内容太宽而无法适应浏览器窗口时，可以换行。默认值为 0。 |
| sort | 在插入文本之前对分支进行排序。该属性值为用于对元素元素的属性名。 |
| assume_children | 0 或 1。如果为 1，则自动假设所有对象都有子对象，因此当它们未展开时，前面总是会显示一个 "+" 号。只有在展开某一个项时，才会在子对象之间进行搜索。这对于避免耗时的搜索非常有用。 |
| single* | 0 或 1。如果为 1，则只能展开树的其中一个分支。当展开一个新分支时，每个已展开的分支都会被折叠。 |
| skip_unauthorized | 0 或 1。如果为 1，当尝试显示用户没有权限访问的子对象时，不会生成任何错误。 |

### tree 标签体中的变量

| 名称 | 解释 |
|---|---|
| tree-item-expand | 如果当前元素处于展开状态，则为 True。 |
| tree-item-url | 当前元素的相对 URL。 |
| tree-root-url | tree 标签所在的 DTML 文档的 URL。 |
| tree-level | 当前元素的深度。 |
| tree-colspan | 调用的树嵌套次数。 |
| tree-state | 树状态：输出为 id 列表和子 id 的子列表。 |

### sendmail 标签的属性

| 名称 | 功能 | 示例 |
|---|---|---|
| mailhost | 管理发送电子邮件所需数据的 Zope MailHost 对象。如果使用了此属性，则不需要 `smtost`。 | <sendmail mailhost="MailHost1"> |
| smtost | 将要使用的 SMTP 服务器的地址。如果使用了此属性，则不需要 `Mailhost` 属性。 | <sendmail smtost="mail.mycompany.com"> |
| port | 此属性仅能与 `smtost` 属性配合使用，且必须指定连接的端口号。如果使用了 `smtost` 但未使用 `port` 属性，则端口号默认设置为 25。 | port="20"> |
| mailto | 收件者地址。多个地址之间用逗号分隔。 | <sendmail mailto=MailHost1 |
| mailfrom | 发件者地址。 | mailfrom="abc@beehive.com" |
| subject | 消息主题。 | subject="Meeting today"> |

### MIME 标签和 Boundary 标签的属性

| 属性 | 功能 | 示例 |
|---|---|---|
| type | 表示数据的的类型和格式。默认值是 `application/octet-stream` | Type="image/bmp" |
| disposition | 设置后续数据的内容的呈现方式。如果 MIME 或或 boundary 标签中未指定 disposition，则内容的 MIME 头将不会插入消息中。 | disposition="attachment" |
| name | 指定要附加的文件对象的名称。如果在 MIME 标签中使用 `name` 属性，则该消息将作为附件发送，而不是标准文本。 | name="wordfile" |
| encode | 设置要发送文件的编码方法。默认值是 `base64`，适用于向大多数邮件客户端发送二进制文件。可用选项有：`base64`、`uuencode`、`x-uuencode`、`quote-printable`、`uue` 和 `7bit`。如果 `encode` 设置为 `7bit`，则不应用任何编码。这适用于 HTML 等文本文档格式。 | encode=uuencode |

## REQUEST 对象

### REQUEST

DTML 命令 `<dtml-var="REQUEST">` 在屏幕上生成如下输出。`REQUEST` 包含了在特定时刻 Zope 安装中变量空间里的现有 Zope 变量列表。

- form
- tree-s eZjTjF3jANPW/VYHUOALL1YE1A
- other
- AUTHENTICATION_PATH
- TraversalRequestNameStack []
    - tree-s eZjTjF3jANPW/VYHUOALL1YE1A
    - URL http://localhost:8080/My_Homepage
