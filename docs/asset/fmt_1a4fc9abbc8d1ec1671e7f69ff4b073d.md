
- `reset()` (Navigator 3, IE 3)—重置表单元素
- `submit()` (Navigator 2, IE 3)—提交表单数据

其他方法：`click` (IE 4), `contains` (IE 4), `getAttribute` (IE 4), `handleEvent` (Navigator 4), `insertAdjacentHTML` (IE 4), `insertAdjacentText` (IE 4), `removeAttribute` (IE 4), `scrollIntoView` (IE 4), `setAttribute` (IE 4)

# 事件

`onclick` (IE 4), `onblclick` (IE 4), `ondragstart` (IE 4), `onfilter` (IE 4), `onhelp` (IE 4), `onkeydown` (IE 4), `onkeypress` (IE 4), `onkeyup` (IE 4), `onmousedown` (IE 4), `onmousemove` (IE 4), `mouseout` (IE 4), `mouseover` (IE 4), `onmouseup` (IE 4), `onmousewheel` (IE 6), `onReset` (Navigator 3, IE 4), `onselect` (IE 4), `onSubmit` (Navigator 2, IE 3)

# frame

- 首次支持：Navigator 2, IE 3

提供对 HTML frame 的访问。`frame` 等同于 `window` 对象。请参考 `window` 对象以获取 `frame` 的描述。在 JavaScript 1.1 中更新。

# FRAMESET

- 首次支持：IE 4

提供对 HTML FRAMESET 标签的访问。

# 属性

Navigator 和 IE 均支持：无

- 其他属性：`border` (IE 4), `borderColor` (IE 4), `className` (IE 4), `cols` (IE 4), `document` (IE 4), `frameBorder` (IE 4), `frameSpacing` (IE 4), `id` (IE 4), `isText` (IE 4), `lang` (IE 4), `language` (IE 4), `parentElement` (IE 4), `parentEdit` (IE 4), `rows` (IE 4), `sourceIndex` (IE 4), `style` (IE 4), `tagName` (IE 4), `title` (IE 4)

# 方法

Navigator 和 IE 均支持：无

- 其他方法：`click` (IE 4), `contains` (IE 4), `getAttribute` (IE 4), `insertAdjacentHTML` (IE 4), `insertAdjacentText` (IE 4), `removeAttribute` (IE 4), `setAttribute` (IE 4)

# 事件

`onbeforeload` (IE 4), `onload` (IE 4), `onresize` (IE 4), `onunload` (IE 4)

# function

- 首次支持：Navigator 3, IE 4

以对象的形式访问 JavaScript 函数。没有定义任何事件。在 JavaScript 1.2 和 1.3 中进行了更新。

# constructor

```
new Function ([arg1, arg2, ... argN]], functionBody)
```

创建一个接受参数 1 到 N 以及指定函数体（以字符串形式表示）的函数。

# 属性

Navigator 和 IE 均支持：

- `arguments` (Navigator 3, IE 4)—识别传递给函数的参数。在最新的 JavaScript 规范中已废弃，由 Arguments 对象取代。
- `arguments.length` (Navigator 3, IE 4)—识别传递给函数的参数数量。
- `caller` (Navigator 4, IE 4)—识别调用此函数的函数。
- `constructor` (Navigator 3, IE 4)—识别对象的构造函数。
- `prototype` (Navigator 3, IE 4)—提供为对象添加新属性的能力。

## 录 A

其他属性：`arguments.callee` (Navigator 4), `arguments.callee` (Navigator 3), `arity` (Navigator 4), `caller` (IE 4), `length` (Navigator 3)

## 方法

Navigator 和 IE 都支持：

- `toString()` (Navigator 3, IE 4)—返回表示函数源代码的字符串
- `valueOf()` (Navigator 3, IE 4)—返回表示函数源代码的字符串

其他方法：`apply` (Navigator 4.06), `call` (Navigator 4.06), `toSource` (Navigator 4.06)

## Global

首次支持于：Navigator 2, IE 4

在 ECMAScript 1 中被识别为全局对象。自 JavaScript 1.0 以来，Global 已通过顶层属性和方法在 Navigator 和 IE 中受到支持。自 JavaScript 1.0 以来定义了额外的属性和方法。在 JavaScript 1.3 中，Navigator 实现了 ECMA 合规性。它没有定义的事件处理器。

## 属性

Navigator 和 IE 都支持：

- `Infinity` (Navigator 4.06, IE 4)—表示无穷大
- `NaN` (Navigator 4.06, IE 4)—表示不是数字（Not-a-Number）的值

其他属性：`undefined` (Navigator 4.06)

## 方法

Navigator 和 IE 都支持：

- `escape(string)` (Navigator 2, IE 3)—返回字符串的 URL 编码
- `eval(string)` (Navigator 2, IE 3)—将字符串求值为 JavaScript 代码
- `isFinite(number)` (Navigator 4.06, IE 4)—返回一个布尔值，表示数字是否有限
- `isNaN(value)` (Navigator 2, IE 3)—返回一个布尔值，表示值是否不是数字
- `parseFloat(string)` (Navigator 2, IE 3)—将字符串转换为浮点数
- `parseInt(string[, radix])` (Navigator 2, IE 3)—将字符串转换为整数
- `unescape(string)` (Navigator 2, IE 3)—将 URL 编码的字符串转换为编码前的值

其他方法：`Number` (Navigator 4), `String` (Navigator 4), `taint` (Navigator 3), `untaint` (Navigator 3)

## H1, H2, H3, H4, H5, H6

首次支持于：IE 4

提供对 HTML H1 到 H6 标签的访问。注意：这些标签在最新的 HTML 规范中已废用。

## 属性

Navigator 和 IE 都支持：无

其他属性：`align` (IE 4), `className` (IE 4), `document` (IE 4), `id` (IE 4), `innerHTML` (IE 4), `innerText` (IE 4), `isText` (IE 4), `lang` (IE 4), `language` (IE 4), `offsetHeight` (IE 4), `offsetLeft` (IE 4), `Parent` (IE 4), `offsetTop` (IE 4), `offsetWidth` (IE 4), `outerHTML` (IE 4), `outerText` (IE 4), `parentElement` (IE 4), `parentTextEdit` (IE 4), `source-Index` (IE 4), `style` (IE 4), `tagName` (IE 4), `title` (IE 4)

## 方法

Navigator 和 IE 都支持：无

其他方法：`click` (IE 4), `contains` (IE 4), `getAttribute` (IE 4), `insertAdjacentHTML` (IE 4), `insertAdjacentText` (IE 4), `remove-Attribute` (IE 4), `scrollIntoView` (IE 4), `setAttribute` (IE 4)

## 事件
