
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

# 第3章：使用图像

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

```
<imagedata href="image.jpg"/>
```

## 图像类型

![](img/81f56bf497dbf7f7582072400d12cb42_68_0.png)

## 图像类型

![](img/81f56bf497dbf7f7582072400d12cb42_68_0.png)

渲染 DocBook 将根据你尝试生成的输出类型，自动决定要查找什么类型的文件。

```
<mediaobject>
<imageobject>
<imagedata fileref="../images/image">
</imageobject>
<textobject>
<phrase>这是一张图像</phrase>
</textobject>
</mediaobject>
```

## 有用的工具

虽然创建 DocBook 标记只需要一个良好的文本编辑器，但你仍然需要一些额外的工具来制作或处理必须包含在最终文档中的任何图像。

本节介绍了一些更流行的开源工具，这些工具可以创建、处理或获取用于你文档的图像。这并不意味着

# 第 3 章：使用图像

可用开源和免费软件程序的详尽列表。这些是我认为非常有用的工具，它们涵盖了在 Linux 下处理图像的基础工作。无论你是制作自己的图像、使用数码相机拍照，还是用扫描仪扫描现有图像，这四个程序都足以满足你的需求。如果你是一个图形爱好者，你可能想访问 Freshmeat (`http://www.freshmeat.net/`) 并查看适用于 Linux 的广泛图形程序。

## 图像类型

![](img/81f56bf497dbf7f7582072400d12cb42_70_0.png)

图 3.7 包含多种类型图像的简单方法
