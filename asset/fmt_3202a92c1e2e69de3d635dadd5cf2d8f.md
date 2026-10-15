
```javascript
this.d = {}; // 保护数字被字符串化

this.d.top = 40;
this.d.left = 40;
this.d.width = 100;
this.d.height = 100;

this.d.scale = att2var("scale", 2);
this.d.screenx = att2var("screenx", window.screen.width);
this.d.screeny = att2var("screeny", window.screen.height);
this.d.pageless = att2var("pageless", false);

this.d.page_offset = 0;
if (! d.page_offset ) {
  d.page_offset = (d.screenx - d.screeny/ratio)/scale/2;
}

this.setAttribute("style", "font-size:"+14/d.scale+"px;");
placeDesktop();
placeNote();
if (! d.pageless ) placeNote();
```

`getAEBA` 属性只是 `document.getElementByAttribute()` 这个长名称的简写引用。为了以后方便，我们记住了小部件重要的 DOM 元素。`d`（data）属性将我们的数值状态数据从 XBL 转换为字符串。`this.d` 的属性来自小部件的用户（应用程序 `<noteplaceholder>` 标签）。在计算完这些属性后，小部件的 `<content>` 部分的属性会进行调整，包括缩放显示的文本。`att2var()`、`placeDesktop()`、`placeNote()` 和 `placePage()` 函数都是在构造函数开始处声明的方法。它们显示在列表 15.19 中。

## 列表 15.19 用于 noteplaceholder XBL 绑定的私有 <constructor>-方法。

```javascript
var att2var = function (name, value) {
  var val = this.getAttribute(name);
  if (val == "*") return value;
  if (isNaN(val)) return value;
  return 0;
}

var arg2var = function (arg) {
  var err = "*Bad passed to noteplaceholder binding";
  if (arg == "*") throw err;
  if (isNaN(arg)) throw err;
  return arg;
}
```

```javascript
this.placeNote = function () {
note.setAttribute("top", d.top / d.scale);
note.setAttribute("left", d.page_offset + d.left / d.scale);
note.setAttribute("width", d.width / d.scale);
note.setAttribute("minheight", d.height / d.scale);
}

this.placeDesktop = function () {
desktop.setAttribute("width", d.width);
}

this.placePage = function () {
page.setAttribute("minheight", d.height);
}
```

## `<noteplaceholder>` 标签

```xml
<property name="screenx" readonly="true"
onget="return this.d.screenx"/>
<property name="screeny" readonly="true"
onget="return this.d.screeny"/>
<property name="pageless" readonly="true"
onget="return this.d.pageless"/>
```

`getCoords()` 函数用于转换坐标，使其与工具函数——`<constructor>`——共存，它不会对 widget 的用户暴露。`setFlowNode()` 方法则暴露给用户。在该方法通过 `getCoords()` 获取本地坐标后，它会根据位置和提供的现有节点重新计算节点的大小和顶角位置。注意，节点被定位以匹配位置。此方法本可以使用一些合理性检查（例如，宽度和高度不应为负数），但对于我们的目的来说已经足够了。

绑定规范的最后部分是 `<handler>` 部分。我们有两个处理程序，都针对左点击事件，但对应不同的鼠标按钮。对于主绑定，我们引入了另一个私有变量，这次命名为 `this.d.topclick`。如果该变量为 `true`，则主点击将设置节点左上角的位置；如果为 `false`，则设置右下角。我们在构造函数中将此变量初始化为 `true`。

对于次要绑定，我们使用勾股定理（“直角三角形两条边的平方和等于斜边的平方”）来检测距离点击点最近的节点对角线，并进行更新。结果代码显示在列表 15.22 中。

## 列表 15.22 用于 placeholder XBL 绑定的 <handler> 标签。

```xml
<handler event="click" button="0"><![CDATA[
this.setFlowNode(event, this.d.topclick);
this.d.topclick = this.d.topclick;
]]>
</handler>
<handler event="click" button="2"><![CDATA[
var coords = this.getCoords(event.clientX, event.clientY);
var dist1, dist2;
with (Math) {
dist1 = sqrt(pow(coords.x-d.left, 2) + pow(coords.y-d.top, 2));
dist2 = sqrt(pow(coords.x - (d.left + d.width), 2) + pow(coords.y - (d.top + d.height), 2));
}
this.setFlowNode(event, dist1 < dist2);
]]>
</handler>
</handlers>
```

使用 CDATA 区域可以避免在调试上浪费大量时间。处理程序函数复用了了暴露的 `setFlowNode()` 方法和私有的 `getCoords()` 方法，因此它们的逻辑非常简单。

完成`<handler>` 内容后，placeholder 绑定即宣告完成，总共大约 150 行代码。没有更多绑定需要，剩下的就是尝试运行它。

### 15.7.4 集成绑定

创建了 `notplaceholder` 绑定后，我们想要尝试它。事实上，接下来的几步是创建绑定测试框架的有效方法。这种测试框架在绑定开发期间和最终测试中都非常有用。要将绑定连接到标签，我们使用单一样式规则：

```css
notplacacer {
  moz-binding: url('notplacacer.xml#notplacacer');
}
```

我们目前将其放入此名为 `xulextras.css` 的文件中。该文件与 `notplaceholder` 其他部分位于同一目录下。此样式表通过新的 `<placeholder>` 标签增强了 XUL 标签的标准。在对新 widget 的测试中，我们希望看到以下情况：

- widget 适应在周围内容中。
- widget 对用户输入有正确响应，包括调整大小。
- widget 上的属性具有预期效果。
- 为 widget 提供的明确内容具有预期效果。

最后，我们构建了 15.23 测试 XUL 文档。

## 列表 15.23 用于 notplaceholder XBL 绑定的测试页。
