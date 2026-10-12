
此覆盖层有两个与主文档匹配的 `id` (`osite1`, `osite2`)。列表 12.9 的内容完全相同，但内容读取为 "Box E, Box F" 而不是 "Box C, Box D"，且 `id="osite2"` 的框多了一个属性 `orient="horizontal"`。

```
Listing 12.9 包含两个包含片段的第二个覆盖层。
```xml

<?xml version="1.0"?>

<overlay xmlns="http://www.mozilla.org/keymaster/gatekeeper/there.is.only">

```

```

```
<box id="ositel">
  <description>Box E</description>
</box>
<box id="osite2" orient="horizontal">
  <description>Box F</description>
</box>
</overlay>
```

12.1 显示了包含和不包含这两个覆盖层的主文档。

每个覆盖层的内容都追加到了主文档的内容中。每个覆盖层按顺序追加到每个目标中。第二个目标 `id` 的布局通过覆盖层提供的属性更改为水平方向。主文档使用 `<vbox>` 或覆盖层使用 `<box>` 并不重要。覆盖层中的标签名称并不重要，但使用匹配的名称可以减少混淆。

这个例子可以稍微复杂一些。主文档的某些内容可以从这样变为：

```
<box id="ositel">
  <description>Main Box A</description>
</box>
<box id="ositel">
  <description>Main Box A</description>
  <box id="inner"/>
</box>
```

变为这样：

其中一个覆盖层可以将此内容作为 `<overlay>` 标签的子元素：

```
<box id="inner">
  <description>Inner Content</description>
</box>
```

覆盖层出现在哪里并不重要——它甚至可以是这两次添加操作的结果，如图 12.2 所示。

新内容被追加在新的位置。它出现在第一个框中追加内容之前，因为它位于主文档现有的内容内部。它被追加到主文档 `<box>` 标签的内容中，而不是主文档 `<vbox>` 标签的内容中。

| Main Box A | Main Box A |

|---|---|

| Box A | Box E |

| Main Box B | Box D / Box F |

**图 12.1** 包含和不包含覆盖层内容的主文档。

## 12.1 覆盖层 (Overlays)

![](img/319913ee3703286e2c03d285fbfc49c7_450_0.png)

图 12.2 带有额外覆盖层内容的主文档。

这个向框添加额外内容的例子是非常简单的。在应用术语中，有很多 XUL 标签是容器标签，对添加额外内容卡片非常敏感。`<commandset>` 可能会获得额外的命令。`<menupopup>` 可能会获得额外的 `<menuitem>`。`<toolbar>` 可能获得额外的 `<toolbarbutton>`。

### 12.1.3 合并选项

基于 `id` 的内容合并系统可以稍微修改。覆盖层内容并不总是必须追加到主文档。XML 属性可以修改它的放置位置。以下属性提供了其他选项：

- `position` `insertbefore` `removeelement`:

`position` 除 `id` 属性外外使用。它接受一个数字作为值，并放置在具有源 `id` 的目标内部的一个或多个内容标签上。内容标签将被插入到目标 `id` 标签的该位置。`position-n=` 将该内容放在目标 `id` 标签的前两个内容项之后。覆盖层之间不会发生位置冲突，因为覆盖层是逐个添加的。

- `insertbefore` 和 `insertafter`: 用于替代覆盖层上的 `id`。它们将每个值作为 `id` 值。不是将源 `id` 的内容添加到主文档，而是将源 `id` 自身及其内容添加。这里有一个额外的 insert 标签。`insertbefore` 将该内容放在主文档中指定的 `id` 之后。在两种情况下，内容都是指定 `id` 的兄弟 DOM 节点。

- `removeelement`: 可以被设置为 `true` 并与 `id` 属性一起使用。覆盖层标签将被移除。当主文档中的此匹配标签设置了此属性时，指定覆盖层内容就没有意义。

列表 12.10 阐释了所有语法。

```xml
<?xml version="1.0"?>
<overlay xmlns="http://www.mozilla.org/keymaster/gatekeeper/there.is.only.xul">
```

列表 12.10 显示了合并选项的语法。

这些 URN 可以用 RDF 属性/值对进行装饰。换句话说，它们可以作为事实的主语。这些事实的谓词必须来自此命名空间：

```
http://www.mozilla.org/rdf/chrome#
```

可用的谓词如表 12.1所示。

## 表 12.1 Chrome 注册表顶层谓词

| 谓词名称 | 适用对象 | 值 | 目的 |

| --- | --- | --- | --- |

| accessKey | skin | 字符 | 经典浏览器中用于更改主题的菜单快捷键 |

| author | package, locale, skin | 任意文本 | 软件包的创建者 |

| baseURL | package | URL | 软件包的位置；不要使用 chrome: 方案 |

| disabled | package | "true" | 防止外部覆盖层；不要设置为 "false" |

| displayName | package | 任意文本 | 物品的可读名称 |

| hasOverlays | package | "true" | 存在 XUL 覆盖层；不要设置为 "false" |

| hasStylesheets | package | "true" | 存在 CSS2 覆盖层；不要设置为 "false" |

| name | package | 软件包名称 | 软件包名称应与目录名匹配 |

| name | skin | 任意文本 | 皮肤的名称；可以是任意文本 |

| image | skin | URL | 说明皮肤外观的图像；不要使用 chrome: 方案 |

| localeVersion | package | 版本号 | 软件包要求的最低版本 |

| locType | package, skin | Install, profile | 软件包或皮肤的安装位置 |

| packages | locale, skin | URN | 存放特定包实现的 <Seq>  |

| previewURL | | URL | 说明本地化外观的文档；不要使用 chrome: 方案 |

| selectedLocale | package | URN | 当前本地化；仅适用于全局包 |

## 12.2 Chrome 注册表 (Chrome Registry)

表 12.1 Chrome 注册表顶层谓词（续）

| 谓词名称 | 适用对象 | 值 | 目的 |

|---|---|---|--| 

| selectedSkin | package | URN | 当前的皮肤；仅适用于全局包 |

| skinVersion | package | 版本号 | 软件包要求的最低皮肤版本 |

除了这些本地化外，还有两组二级容器。可以通过每个本地化和皮肤 URN 的 `package` 谓词进行访问。这些附加容器说明了皮肤和本地化的特定包实现的存在。它们也是 `<Seq>` 容器，具有如下名称：

```
urn:mozilla:locale:(locale-name):packages
urn:mozilla:skin:(skin-name):packages
```

每个容器都包含一个本地化或皮肤的特定包实现列表。本地化实现的 URN 应当为：

```
urn:mozilla:locale:(locale-name):package-name
urn:mozilla:skin:(skin-name)/(skin-version):package-name
```

如果 navigator 包（经典浏览器）具有法语本地化（FR）的实现，则需要此 URN 来声明该本地化已实现并可用：

```
urn:mozilla:locale:FR:navigator
```

如此声明的每个特定皮肤或本地化资源也可以用 RDF 属性/值对进行装饰。可用的谓词如表 12.2 所示。

较新的 Mozilla 浏览器通过额外的谓词稍稍增强了表 12.1 和表 12.2。

## 表 12.2 Chrome 注册表实现谓词

| 谓词名称 | 适用对象 | 值 | 目的 |

|---|---|---|--|
