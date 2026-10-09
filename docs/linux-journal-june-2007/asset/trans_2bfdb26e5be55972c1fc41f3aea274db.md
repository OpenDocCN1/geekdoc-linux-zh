
## 创建编程式扩展

为了熟悉附加组件工具并更好地理解创建编程式扩展的过程，让我们从头开始构建一个简单的虚拟文本生成器扩展。安装后，该扩展会在“工具 → 附加组件”菜单中添加“Lorem ipsum”命令。此命令会运行一个 OpenOffice.org Basic 宏，插入指定段落数的 Lorem ipsum 虚拟文本。以下说明假设您已具备有关如何在 OpenOffice.org 中创建和管理宏、模块及库的通用知识。附加组件工具使用的是旧术语“add-on”，您可以将其视为“扩展”的同义词。

首先，创建一个生成虚拟文本的宏。为保持整洁，创建一个名为 `LoremIpsumLib` 的独立库，其中包含 `LoremIpsumModule`。在此模块中，添加清单 1 中所示的宏。（请将“Lorem ipsum dolor sit amet…”字符串替换为一段虚拟文本）。

在启动附加组件工具之前，您需要做一些准备工作。首先，为所有工作文件创建一个单独的文件夹（例如 `loremipsum`）。如果您想为菜单项添加图标，请确保您拥有必要的图形文件。根据官方文档，您需要一组小尺寸（16x16）和大尺寸（26x26）的 BMP 格式图标。但是，您也可以使用 PNG 格式的 16x16 图标（您可以在 [www.famfamfam.com/lab/icons/silk](http://www.famfamfam.com/lab/icons/silk) 上找到一些高质量的图标）。接下来，将完整的 `LoremIpsumLib` 库复制到 `loremipsum` 文件夹中。为此，请导航到家目录下的 `/user/basic`，将 `LoremIpsumLib` 复制到 `loremipsum` 文件夹。现在，打开附加组件工具文档，并确保已启用宏执行。滚动到*创建配置文件*章节，按*创建 XML 文件*按钮以启动附加组件创建器。

### 清单 1. loremipsummacro.bxt

```basic
Option Explicit
Sub LoremipsumMacro()
  Dim ThisDoc As Object
  Dim Cursor As Object
  Dim ParNumber As Integer
  Dim InputMsg As String, InputTitle As String, InputReturn As String
  ThisDoc=ThisComponent
  InputMsg="Number of paragraphs"
  InputTitle="Lorem Ipsum Generator"
  InputReturn=InputBox (InputMsg, InputTitle)
  ParNumber=InputReturn
  Do While ParNumber>0
    Cursor=ThisDoc.text.createTextCursor
    Cursor.String="Lorem ipsum dolor sit amet…" & Chr(13)& Chr(13)
    ParNumber=ParNumber-1
  Loop
End Sub
```

![](img/526fd434dcfcf1b461b94c24ea170f36_90_0.png)

![](img/526fd434dcfcf1b461b94c24ea170f36_91_0.png)

**图 2. 使用附加组件创建器创建编程式扩展**

使用附加组件创建器创建扩展的过程大致可以分为三个阶段。首先，您定义常规设置，包括顶级菜单及其位置。然后，您指定菜单项，最后，您将创建的包压缩。在*基本信息*窗口中，指定主脚本文件的路径。按*浏览*按钮，并选择 `LoremIpsumLib` 文件夹内的脚本 `.xlb` 文件。您还必须在该*您的附加组件的唯一名称*字段中为您的扩展指定一个名称。只需将 `org.openoffice.Office.addon.example` 字符串中的示例部分替换为您想要的名称（例如 `org.openoffice.Office.addon.LoremIpsum`）。按*下一步*以选择在哪里添加顶级扩展菜单。这里有两个选择：您可以将菜单项添加到主菜单或工具菜单下。通常，如果您有一个仅包含几个命令的简单扩展，请将其置于工具菜单下。更复杂的扩展值得在主菜单中拥有自己的条目。由于 Lorem ipsum 生成器仅包含一个命令，因此将其安装在工具菜单下是有意义的。接下来，输入菜单标题，并按*添加此文本*按钮。如果您希望您的扩展仅对特定语言或国家可用，可以通过在*语言限制*部分指定相应设置来实现。当您对设置满意时，按*完成*。

下一步是将 `LoremIpsumMacro` 链接到创建的菜单项。为此，您必须指定库、模块以及宏本身。在我们的案例中，分别是 `LoremIpsumLib`、`LoremIpsumModule` 和 `LoremIpsumMacro`。一旦将宏链接到命令，您就可以为其添加图标。

### 清单 2. addonrc.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<oor:node xmlns:oor="http://openoffice.org/2001/registry"
xmlns:xs="http://www.w3.org/2001/XMLSchema" oor:name="Addons"
 oor:package="org.openoffice.Office">
 <node oor:name="Addon1">
  <node oor:name="AddonMenu">
   <node oor:name="org.openoffice.Office.addon.LoremIpsum"
    oor:op="replace">
    <prop oor:name="Context" oor:type="xs:string">
     <value/>
    </prop>
    <prop oor:name="Title" oor:type="xs:string">
     <value>Lorem ipsum</value>
    </prop>
    <prop oor:name="URL" oor:type="xs:string">
     <value>macro:///LoremIpsumLib.LoremIpsumModule.LoremIpsumMacro</value>
    </prop>
    <prop oor:name="Target" oor:type="xs:string">
     <value>self</value>
    </prop>
    <prop oor:name="ImageIdentifier" oor:type="xs:string">
     <value/>
    </prop>
   </node>
   <node oor:name="Images">
    <node
     oor:name="org.openoffice.Office.addon.LoremIpsum.img01"
     oor:op="replace">
     <prop oor:name="URL" oor:type="xs:string">
      <value>macro:///LoremIpsumLib.LoremIpsumModule.LoremIpsumMacro</value>
     </prop>
     <node oor:name="UserDefinedImages">
      <prop oor:name="ImageSmallURL">
       <value>%Origin%/LoremIpsumLib/Icon.png</value>
      </prop>
     </node>
    </node>
   </node>
  </node>
 </node>
</oor:node>
```

由于我们选择使用 PNG 格式的图标，请按下*其他图像类型*按钮，从图标定义下拉列表中选择*16x16 正常对比度*项，使用*浏览*图标选择图标，然后按*确定*以添加它。在添加图标时，您有两个选项：要么链接到一个将作为图像文件添加到扩展中的图标，要么将其集成到配置文件中（这仅适用于 BMP 格式的图标）。选择哪个选项主要取决于个人喜好，但链接图标而不是嵌入它们会产生更清洁、更易于阅读的配置文件。如果您稍后需要手动编辑该文件，这可能会有帮助。使用*完成*按钮以最终确定扩展，并按下*附加组件压缩*按钮以进行打包。现在您可以通过选择*工具 → 软件包管理器*来安装创建的扩展。重新启动 OpenOffice.org，您应该会在*工具 → 附加组件*菜单中看到*lorem ipsum*命令。

### 调整扩展

附加组件创建器巧妙地隐藏了过程的技术部分，如果您不想花时间手动完成这些基础工作，这是很好的做法。然而，如果您希望更好地了解扩展的工作机制——不仅是为了满足好奇心，也是为了能够在不每次都运行附加组件创建器的情况下对扩展进行故障排除和调整，那么这种方法就没那么有用。

如果您查看 zip 包内部，您会发现它包含熟悉的 `META-INF` 文件夹、包含宏文件的文件夹以及 `addon.xcu` 文件（清单 2）。后者是扩展的关键元素，因为它包含所有配置数据。`addon.xcu` 基于 XML，即使您只具备 XML 的基本知识，也只需查看其内容即可轻松理解其工作原理。

XML 文件包含若干节点，每个节点都有属性，而这些属性又具有值。例如，顶级节点 `<node oor:name="AddonMenu">` 具有多个属性，如 `<prop oor:name="Title" oor:type="xs:string">`，它们具有包含扩展菜单标题的值——`<value>Lorem ipsum</value>`。`<prop oor:name="URL" oor:type="xs:string">` 属性具有 `<value>macro:///LoremIpsumLib.LoremIpsumModule.LoremIpsumMacro</value>` 值，其中包含指向相应宏的链接。知道了这一点，您可以通过调整其 `addon.xcu` 文件来修改扩展。例如，如果您想更改菜单标题，只需编辑 `<value>Lorem ipsum</value>` 值如下：

```xml
<prop oor:name="Title" oor:type="xs:string">
  <value>Insert dummy text</value>
</prop>
```

在更复杂的宏中，您甚至可以通过克隆和修改配置文件的部分来添加新的菜单和命令。

![](img/526fd434dcfcf1b461b94c24ea170f36_92_0.png)

### 结语

既然您已经了解了基础知识，就可以开始构建自己的 OpenOffice.org 扩展了。如果您想与其他用户分享您的创作，您可以将它们添加到官方扩展存储库（`wiki.services.openoffice.org/wiki/Extensions_repository`）中。那里的大多数扩展都是基于 GPL 许可证发布的，因此您可以反编译它们以查看其工作原理并获得新的灵感。

> Mitpi Dormir 是一位自由撰稿人，其文章曾刊登在俄罗斯、英国和丹麦的计算机杂志上。他的文章涉及开源软件、Linux、Web 应用及其他计算机相关主题。

![](img/526fd434dcfcf1b461b94c24ea170f36_92_1.png)

