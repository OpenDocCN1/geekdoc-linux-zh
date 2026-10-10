
# 第3章：使用图像

![](img/81f56bf497dbf7f7582072400d12cb42_63_0.png)

使用 PNG 图片的缺点是软件和浏览器支持的问题。最新版本的 Netscape Navigator 和 Internet Explorer 支持 PNG，但旧版本可能无法很好处理或根本无法处理 PNG。PNG 的某些功能（例如透明度）在某些浏览器中可能不可用。如果你针对的是 Netscape 或 Internet Explorer 3 或更早版本，可能最好坚持 JPEG。如果你确定受众是使用较新浏览器的用户，可以放心地使用 PNG。

同样，如果你使用的是早期版本的 Adobe Photoshop 或图像处理程序，可能不支持以 PNG 格式保存图形。

PNG 兼具两者的优点：一种无损图像格式，尺寸较小，提供透明度，并支持索引色、灰度和真彩色图像（见图 3.2）。

要测试你的浏览器，请将其指向此 URL：`http://www.w3.org/Graphics/PNG/inline_alpha.html`。

现在你已经知道了了自己的选择，你将查看如何使用 DocBook 标记在文档中包含图像。

## 图像类型

![](img/81f56bf497dbf7f7582072400d12cb42_64_0.png)

图 3.2 完全兼容浏览器中的 PNG 图像示例

## 为 Web 标记图像

DocBook 中可以使用许多不同的元素来包含图像，但其中许多元素现在已弃用。

DocBook 在开发过程中，OASIS 技术委员会偶尔会认为某些事情的实现方式比目前更好，或者新技术表明需要以不同的方式进行处理。委员会会对 DocBook DTD 进行更改以反映这一点。

然而，政策是避免在短时间内对 DTD 发生剧烈变化。对于要消除的元素，将保持支持，但不被鼓励使用。这使得 DocBook 主要版本之间的不兼容性降到最低。

虽然你仍然可以使用弃用的元素（例如当你从别人那里获得了一份旧的 DocBook 文档时），我在本书中避免使用它们，以尽量减少混淆并避免养成坏习惯。

> 弃用的元素仍然有效，但正在被淘汰，取而代之的是新元素或简单地被消除。

![](img/81f56bf497dbf7f7582072400d12cb42_64_1.png)

在这里用于在文档中包含图形的三个元素是 `MediaObject`、`ImageObject` 和 `ImageData`。与 HTML 不同，插入一个 `img` 元素并此结束是不够的。`MediaObject` 元素不仅限于图形，还可能包含 `AudioObject` 元素和/或 `VideoObject` 元素。

`MediaObject` 元素还可以包含 `TextObject` 元素及其子元素 `Phrase` 元素，但不能单独使用。`TextObject` 和 `Phrase` 的组合必须与 `ImageObject`、`AudioObject` 或 `VideoObject` 元素结合使用。`TextObject` 不应与 `Caption` 元素混淆，`Caption` 用于为图像添加标准说明，而不是用于替代图像的备用文本。

现在，你只关注结合 `TextObject` 和 `Phrase` 对使用 `ImageObject` 元素来为 Web 生成输出。

在典型的 Web 页面中，你将看到这种标记来显示带有原生文本的图像，以防浏览器不支持图像或图像被关闭：

```
<img src="image.jpg" alt="This is an image">
```

这产生了图 3.3 所示的输出。

如果在纯文本浏览器（如 Lynx）中查看，你将看到图 3.4 所示输出。

要在 HTML 中渲染此输出，你必须在 DocBook 标记中包含所有必要信息，如图 3.5 所示：

```
<mediaobject>
<imageobject>
<imagedata fileref="image.jpg">
</imageobject>
<textobject>
<phrase> is an image. 如果你能查看图像，你会看到一个很棒图像！</phrase>
</textobject>
</mediaobject>
```

![](img/81f56bf497dbf7f7582072400d12cb42_66_0.png)

图 3.3 带有备用文本的图像

![](img/81f56bf497dbf7f7582072400d12cb42_66_1.png)

图 3.4 在 Lynx 中显示的备用文本

![](img/81f56bf497dbf7f7582072400d12cb42_67_0.png)

图 3.5 显示图像和备用文本的 DocBook 标记

注意 `ImageData` 元素是一个空元素，因此在 XML 标记中，必须在标记末尾包含斜杠以表示空元素，例如：

```
<imagedata href="image.jpg"/>
```

> 记住，空元素是不需要关闭标签的元素。`ImageData` 元素是一个空元素，因此在 XML 标记中，必须在标记末尾包含斜杠以表示空元素，例如：
>
> ```
> <imagedata href="image.jpg"/>
> ```
