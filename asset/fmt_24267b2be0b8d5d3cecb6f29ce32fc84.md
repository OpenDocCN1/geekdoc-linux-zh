
其他属性：`accessKey` (IE 4), `aLink` (IE 4), `background` (IE 4), `bColor` (IE 4), `bgProperties` (IE 4), `bottomMargin` (IE 4), `className` (IE 4), `clientHeight` (IE 4), `clientLeft` (IE 4), `clientTop` (IE 4), `clientWidth` (IE 4), `document` (IE 4), `filter` (IE 4), `id` (IE 4), `innerHTML` (IE 4), `innerText` (IE 4), `isEdit` (IE 4), `lang` (IE 4), `language` (IE 4), `leftMargin` (IE 4), `link` (IE 4), `noWrap` (IE 4), `offsetHeight` (IE 4), `offsetLeft` (IE 4), `offsetParent` (IE 4), `offsetTop` (IE 4), `offsetWidth` (IE 4), `outerHTML` (IE 4), `outerText` (IE 4), `parentElement` (IE 4), `parentTextEdit` (IE 4), `recordNumber` (IE 4), `rightMargin` (IE 4), `scroll` (IE 4), `scrollHeight` (IE 4), `scrollLeft` (IE 4), `scrollTop` (IE 4), `scrollWidth` (IE 4), `sourceIndex` (IE 4), `style` (IE 4), `tabIndex` (IE 4), `tagName` (IE 4), `text` (IE 4), `title` (IE 4), `topMargin` (IE 4), `vLink` (IE 4)

# 方法

Navigator 和 IE 都支持：无

其他方法：`click` (IE 4), `contains` (IE 4), `createRange` (IE 4), `getAttribute` (IE 4), `insertAdjacentHTML` (IE 4), `insertAdjacentText` (IE 4), `removeAttribute` (IE 4), `setAttribute` (IE 4)

# 事件

`onafterupdate` (IE 4), `onbeforeunload` (IE 4), `onbeforeupdate` (IE 4), `onchange` (IE 4), `onclick` (IE 4), `ondataavailable` (IE 4), `onsetchanged` (IE 4), `onatasetcomplete` (IE 4), `ondblclick` (IE 4), `dragstart` (IE 4), `onerrorrorupdate` (IE 4), `onfilterchange` (IE 4), `onhelp` (IE 4), `onkeydown` (IE 4), `onkeypress` (IE 4), `onkeyup` (IE 4), `onload` (IE 4), `onmousedown` (IE 4), `onmousemove` (IE 4), `onmouseout` (IE 4), `onmouseover` (IE 4), `onmouseup` (IE 4), `onmouswheel` (IE 6), `onrowenter` (IE 4), `onrowexit` (IE 4), `onscroll` (IE 4), `onselectstart` (IE 4), `onunload` (IE 4)

# 布尔

首次支持：Navigator 3, IE 4

提供布尔真和假值的对象表示。重要的一点不要混淆布尔对象与布尔原始值：当用于替代布尔原始值时，布尔对象始终求值为真。布尔对象没有关联事件。它引入于 JavaScript 1.1，但在 JavaScript 1.3 中进行了修改以确保符合 ECMA 262 标准。它在 JScript 3 及更高版本中受支持。

## 构造函数

```
new Boolean(value)
```

构造函数使用的值创建一个对象：如果 `value` 为 `false`、`0`、`""`、`NaN`（非数字）、`null` 或 `undefined`，如果省略 `value`，则对象表示 `false`。对于任何其他值，将创建一个表示 `true` 的对象。

## 属性

Navigator 和 IE 都支持：

- `constructor` (Navigator 3, IE 4)—指向对象构造函数的引用
- `prototype` (Navigator 3, IE 4)—用于定义额外的属性

## 方法

Navigator 和 IE 都支持：

- `toString()` (Navigator 3, IE 4)—返回与 `toString()` 兼容的对象的字符串值
- `valueOf()` (Navigator 3, IE 4)—返回对象的原始值

其他方法：`toSource` (Navigator 4.06)

# BR

首次支持：IE 4

提供对 HTML 标签的访问。没有定义事件

## 属性

Navigator 和 IE 都支持：无

其他属性：`className` (IE 4), `clear` (IE 4), `document` (IE 4), `is` (IE 4), `isEdit` (IE 4), `language` (IE 4), `offset` (IE 4), `offsetLeft` (IE 4), `offsetParent` (IE 4), `offsetTop` (IE 4), `offsetWidth` (IE 4), `outerHTML` (IE 4), `outerText` (IE 4), `parentElement` (IE 4), `parentTextEdit` (IE 4), `sourceIndex` (IE 4), `style` (IE 4), `tagName` (IE 4), `title` (IE 4)

## 方法

Navigator 和 IE 都支持：无

其他方法：`contains` (IE 4), `getAttribute` (IE 4), `insertAdjacentHTML` (IE 4), `insertAdjacentText` (IE 4), `removeAttribute` (IE 4), `setAttribute` (IE 4)

# 按钮

首次支持：Navigator 2, IE 3

提供对 `form` 的访问。注意：包含 HTML 的按钮预计将被移除。

## 属性

Navigator 和 IE 都支持：

- `form` (Navigator 2, IE 3)—对表单的访问
- `name` (Navigator 2, IE 3)—按钮的名字
- `type` (Navigator 2, IE 3)—按钮的类型

其他属性：`accessKey` (IE 4), `className` (IE 4), `dataField` (IE 4), `dataFormats` (IE 4), `dataSrc` (IE 4), `disabled` (IE 4), `document` (IE 4), `id` (IE 4), `innerHTML` (IE 4), `innerText` (IE 4), `isTextEdit` (IE 4), `lang` (IE 4), `language` (IE 4), `offsetHeight` (IE 4), `offsetLeft` (IE 4), `offsetParent` (IE 4), `offsetTop` (IE 4), `offsetWidth` (IE 4), `outerHTML` (IE 4), `outerText` (IE 4), `parentElement` (IE 4), `textEdit` (IE 4), `sourceIndex` (IE 4), `style` (IE 4), `tagName` (IE 4), `title` (IE 4), `value` (IE 4)

## 方法

Navigator 和 IE 都支持：

- `blur()` (Navigator 2, IE 3)—移除按钮的焦点
- `click()` (Navigator 2, IE 3)—模拟点击按钮
- `focus()` (Navigator 2, IE 3)—使按钮聚焦

## 事件

`onblur` (IE 4), `onclick` (IE 4), `ondclick` (IE 4), `onfocus` (IE 4), `onhelp` (IE 4), `onkeydown` (IE 4), `onkeypress` (IE 4), `onkeyup` (IE 4), `onmousedown` (IE 4), `onmousemove` (IE 4), `onmouseout` (IE 4), `onmouseover` (IE 4), `onmouseup` (IE 4), `resize` (IE 4)

# UTTON

首次支持：IE 4

提供访问按钮的能力。注意：包含 HTML 的按钮预计将被移除。

## 属性

Navigator 和 IE 都支持：无
