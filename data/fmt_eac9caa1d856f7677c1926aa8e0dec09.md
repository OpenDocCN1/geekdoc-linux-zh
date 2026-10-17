
### `body`

**Description:** 表示非框架 XHTML 文档中包含要显示的内容

**Element Type:** 结构性（文档），非空

**Example:**

```html
<body>页面的所有内容都放在这里</body>
```

**Tips:** 支持非常广泛。此元素常用于演示，因为浏览器会为块引用设置留边距，但应避免这种用法。相反，应使用 CSS 为任何元素实现留边距和内边距。

### `br`

**Description:** 强制换行

**Element Type:** 块级，空

**Example:**

```html
为了换行我的行<br />
```

一个换行是可以的。

**Tips:** 在某些旧版浏览器中，空元素中紧跟在最后一个字符后面出现的尾斜杠可能会导致渲染问题。在元素的最后一个字符和尾斜杠之间放置一个空格可以解决此问题。

### `button`

**Description:** 允许在表单中包含基于图片的按钮

**Element Type:** 行内，非空

**Example:**

```html
<button type="submit" id="button" value="clicked">
<img src="images/submit.gif" width="50" height="30" alt="submit">
</button>
```

**Tips:** 此元素得到了广泛支持，Netscape 4.x 浏览器除外。

### `caption`

**Description:** 在表格中声明标题。它对于可访问性目的特别有用。

**Element Type:** 结构性（表格），非空

**Example:**

```html
<caption>这是表格的用途</caption>
```

**Tips:** 此元素被广泛支持，但在不同浏览器版本和类型中的渲染效果可能不同。

### `center`

**Description:** 用于在页面上居中显示文本或其他内容的表现性元素

**Element Type:** 块级，非空

**Example:**

```html
<center>此文字现在将在页面上居中显示</center>
```

**Tips:** 这是一个表现性元素，应该优先使用 CSS 而非使用它。

### `cite`

**Description:** 表示对另一个来源的引用或参考

**Element Type:** 行内，非空

**Example:**

他说 `<cite>别哭了亲爱的，那只是洒掉的牛奶！</cite>` 但她仍然在哭。

**Tips:** 此元素被广泛支持，应用于内联引用、引用和参考。大多数浏览器将用斜体样式化此元素，但通过 CSS，你可以根据喜好进行修改。

### `code`

**Description:** 表示代码示例

XHTML 1.0 注释参考 233

**Element Type:** 行内，非空

**Example:**

`<code><code></code></code>` 元素用于表示内联出现的代码项。

**Tips:** 支持非常广泛，此元素在大多数浏览器中通常使用等宽字体显示。

### `col`

**Description:** 定义并控制列组内某列的显示；有助于提高表格的可访问性。

**Element Type:** 行内，空

**Example:**

```html
<col span="2" align="right" />
```

**Tips:** 此元素在许多浏览器中不可靠，而且由于它常用于样式表现，现代实践建议使用结构良好的表格和 CSS 以获得更一致的结果。

### `colgroup`

**Description:** 表示表格中的列组

**Element Type:** 行内，非空

**Example:**

```html
<table>
<colgroup align="center" span="2"></colgroup>
<colgroup valign="bottom"></colgroup>
<tr>
<td>第一列，跨越两列，居中。</td>
<td>第二列，两列跨越的一部分，居中</td>
<td>第三列，对齐到底部</td>
</tr>
</table>
```

**Tips:** 此元素在许多浏览器中不可靠，主要用于出于表现原因对列进行分组。表现最好通过 CSS 处理以获得一致的结果。

### `dd`

**Description:** 创建定义列表描述

**Element Type:** 块级，非空

**Example:**

```html
<dl>
<dt>XHTML</dt>
<dd>可扩展超文本标记语言</dd>
</dl>
```

**Tips:** 此元素被广泛支持，但遗憾的是未被充分利用。

### `del`

**Description:** 表示被删除的文本，通常来自同一文档的先前版本，或正在编辑的文档

**Element Type:** 行内，非空

**Example:**

```html
<del>这段文字将被删除</del>
```

**Tips:** 在 Netscape 4.x 中不支持，此元素在支持的浏览器中通常带有删除线样式显示。

### `dfn`

**Description:** 在术语首次出现时描述它

**Element Type:** 行内，非空

**Example:**

```html
<dfn>XHTML</dfn> 可扩展超文本标记。
```

**Tips:** Netscape 4.x 不支持。

### `dir`

**Description:** 定义目录列表

**Element Type:** 块级，非空

**Example:**

```html
<dir>
<li>项目一</li>
<li>项目二</li>
<li>项目三</li>
</dir>
```

**Tips:** 广泛支持，但应使用 `ul` 来替代它。

### `div`

**Description:** 表示文档中的区域

**Element Type:** 块级，非空

**Example:**

```html
<div id="content">
此部分将包含主要内容。
</div>
```

**Tips:** 支持良好。使用 CSS 设置样式。

### `dl`

**Description:** 表示术语列表

**Element Type:** 块级，非空

**Example:**

```html
<dl>
<dt>XHTML</dt>
<dd>可扩展超文本标记语言</dd>
</dl>
```

**Tips:** 此元素被广泛支持。

### `dt`

**Description:** 表示要定义的术语

**Element Type:** 块级，非空

**Example:**

见 `d1`。

**Tips:** 此元素被广泛支持。

### `em`

**Description:** 一种结构性的非空行联元素，用于表示强调的文本

**Element Type:** 行内，非空

**Example:**

```html
<em>这段文字被标记为强调。</em>
```

**Tips:** 此元素被广泛支持。虽然浏览器通常用斜体显示强调文本，但这是一种约定。`em` 元素不是表现性的。

### `fieldset`

**Description:** 为相关的表单标签和控件提供分组方法。用于可访问性。

**Element Type:** 块级，非空

**Example:**

```html
<form>
<fieldset>
  <input type="text" id="firstname" value="firstname" />
  <input type="text" id="lastname" value="lastname" />
</fieldset>
</form>
```

**Tips:** 支持 Netscape 4.x，但除此之外，此元素在现代浏览器中得到了良好支持。大多数浏览器为 `fieldset` 的内容设置边界。

### `font`

**Description:** 允许文档作者向文档添加字体

**Element Type:** 行内，非空

**Example:**

```html
<font face="Arial" color="blue" size="2">这将显示为比默认更小的 Arial 蓝色文字</font>
```

**Tips:** 这是一个已弃的元素，尽管它在 XHTML 1.0 Transitional 中被允许，但应避免使用。

### `form`

**Description:** 表示表单

**Element Type:** 块级，非空

**Example:**

```html
<input type="text" id="firstname" value="firstname" />
<input type="text" id="lastname" value="lastname" />
</form>
```
