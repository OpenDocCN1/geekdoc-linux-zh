
`afterupdate` (IE 4), `onbeforeupdate` (IE 4), `blur` (IE 4), `onchange` (IE 4), `onavailable` (IE 4), `dataavailable` (IE 4), `complete` (IE 4), `onclick` (IE 4), `onerrorupdate` (IE 4), `onfocus` (IE 4), `help` (IE 4), `onkeydown` (IE 4), `onkeypress` (IE 4), `onkeyup` (IE 4), `onload` (IE 4), `onmousedown` (IE 4), `mousemove` (IE 4), `mouseout` (IE 4), `onmouseup` (IE 4), `onreadystatechange` (IE 4), `onresize` (IE 4), `onenter` (IE 4), `onexit` (IE 4)

![img/6e9914f217994f8949215b0c67ff538.png]

## Area

首次支持于：Navigator 3, IE 4

定义图像映射的区域。从 JavaScript 的角度来看，`Area` 在功能上等同于 `Link` 对象；它与 URL 关联，当用户点击由 `Area` 对象代表的图像映射区域时，该 URL 会加载。

### 属性

Navigator 和 IE 均支持：

- `hash` (Navigator 2, IE 3)—URL 中的锚点名称
- `host` (Navigator 2, IE 3)—代表 URL 主机的主机名或 IP 地址
- `href` (Navigator 2, IE 3)—整个 URL 的文本
- `pathname` (Navigator 2, IE 3)—URL 的路径名部分
- `port` (Navigator 2, IE 3)—URL 的端口值
- `protocol` (Navigator 2, IE 3)—URL 的协议类型
- `search` (Navigator 2, IE 3)—包含的任何查询字符串的值
- `target` (Navigator 2, IE 3)—URL 的属性值

其他属性：`alt` (IE 4), `className` (IE 4), `coords` (IE 4), `document` (IE 4), `isText` (IE 4), `lang` (IE 4), `language` (IE 4), `offsetHeight` (IE 4), `offsetLeft` (IE 4), `offsetParent` (IE 4), `offsetTop` (IE 4), `outerHTML` (IE 4), `outerText` (IE 4), `parentElement` (IE 4), `parentText` (IE 4), `sourceIndex` (IE 4), `style` (IE 4), `tagName` (IE 4), `title` (IE 4)

### 方法

Navigator 和 IE 均支持：无

其他方法：`blur` (IE 4), `click` (IE 4), `contains` (IE 4), `focus` (IE 4), `getAttribute` (IE 4), `insertAdjacentHTML` (IE 4), `insertAdjacentText` (IE 4), `removeAttribute` (IE 4), `scrollIntoView` (IE 4), `setAttribute` (IE 4)

### 事件

`onclick` (IE 4), `onclickclick` (IE 4), `dragstart` (IE 4), `help` (IE 4), `onkeydown` (IE 4), `onkeypress` (IE 4), `keyup` (IE 4), `onmousedown` (IE 4), `onmove` (IE 4), `mouseout` (IE 4), `mouseover` (IE 4), `onmouseup` (IE 4), `onwheel` (IE 6), `onselectstart` (IE 4), `onselectwheel` (IE 6)

## Array

首次支持于：Navigator 3, IE 4

代表一个 Java applet。`document` 对象的属性提供了与文档关联的 `Applet` 对象列表的访问。只有在 applet 的 `APPLET` 标签中提供了 `MAYSCRIPT` 属性时，JavaScript 才能访问该 applet。

### JavaScript 对象引用

例如，以下 `APPLET` 标签加载了一个可以通过 JavaScript 访问的 applet：

```
<APPLET CODE="myClass" MAYSCRIPT></APPLET>
```

由于以下 `APPLET` 标签不包含 `MAYSCRIPT` 属性，因此无法从 JavaScript 访问：

```
<APPLET CODE="myClass"></APPLET>
```

`Applet` 对象继承了它代表的 Java 对象的所有公共属性和方法。

### 属性

Navigator 和 IE 均支持：无

其他属性：`access` (IE 4), `align` (IE 4), `altHTML` (IE 4), `className` (IE 4), `code` (IE 4), `dataField` (IE 4), `dataSrc` (IE 4), `document` (IE 4), `height` (IE 4), `hspace` (IE 4), `id` (IE 4), `isText` (IE 4), `lang` (IE 4), `language` (IE 4), `name` (IE 4), `offsetHeight` (IE 4), `offsetLeft` (IE 4), `offsetParent` (IE 4), `offsetTop` (IE 4), `lineWidth` (IE 4), `outerHTML` (IE 4), `outerText` (IE 4), `parentElement` (IE 4), `parentText` (IE 4), `sourceIndex` (IE 4), `style` (IE 4), `tagName` (IE 4), `title` (IE 4), `vspace` (IE 4)

### 方法

Navigator 和 IE 均支持：无

其他方法：`blur` (IE 4), `click` (IE 4), `contains` (IE 4), `focus` (IE 4), `getAttribute` (IE 4), `insertAdjacentHTML` (IE 4), `insertAdjacentText` (IE 4), `removeAttribute` (IE 4), `scrollIntoView` (IE 4), `setAttribute` (IE 4)

### 事件

`afterupdate` (IE 4), `onbeforeupdate` (IE 4), `blur` (IE 4), `onchange` (IE 4), `onavailable` (IE 4), `dataavailable` (IE 4), `complete` (IE 4), `onclick` (IE 4), `onerrorupdate` (IE 4), `onfocus` (IE 4), `help` (IE 4), `onkeydown` (IE 4), `onkeypress` (IE 4), `onkeyup` (IE 4), `onload` (IE 4), `onmousedown` (IE 4), `mousemove` (IE 4), `mouseout` (IE 4), `onmouseup` (IE 4), `onreadystatechange` (IE 4), `onresize` (IE 4), `onenter` (IE 4), `onexit` (IE 4)

![img/6e9914f217994f8949215b0c67ff538.png]

# JavaScript 对象引用 515

Navigator 4), `pop` (IE 5.5+), `push` (IE 5.5+), `shift` (IE 5.5+), `unshift` (IE 5.5+), `splice` (IE 5.5+)

## 属性

首次支持于：IE 5

将 HTML 元素的属性封装为对象。没有定义的事件。

### 属性列表

Navigator 和 IE 都支持：无

其他属性：`attributes` (IE 6), `childNodes` (IE 6), `cloneNode` (IE 6), `expand` (IE 5), `firstChild` (IE 6), `name` (IE 6), `nextSibling` (IE 6), `nodeName` (IE 5), `nodeType` (IE 5), `nodeValue` (IE 5), `parentNode` (IE 6), `previousSibling` (IE 6), `specified` (IE 5)

### 方法

Navigator 和 IE 都支持：无
