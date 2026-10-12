
| `allowScripts` | `skin` | `'true'` | 皮肤可以运行脚本；不要设置为 `'false'` |

| `baseURL` | `locale`, `skin` | `URL` | 实现的位置；不要使用 `chrome` 方案 |

| `localeVersion` | `locale` | 版本号 | 此实现的版本 |

| `package` | `locale`, `skin` | `URN` | 此实现所属的包 |

| `skinVersion` | `skin` | 版本号 | 此实现的版本 |

## 12.3 持久化窗口状态 (PERSISTING WINDOW STATE)

与覆盖系统和 `chrome` 注册表类似，但要简单得多的是 Mozilla 的 GUI 持久化系统。该系统允许在应用程序关闭后记住 Mozilla 窗口在桌面上的位置和取向。它也可以用于存储任何应用程序的任何种非关键信息。所有信息都存储在本地计算机上。

持久化系统由 RDF 文件、一个 XUL 属性以及 Mozilla 平台的某些处理组成。它记录了一个或多个属性 XUL 标签的状态（值）。有时这是自动完成的，需要应用程序程序员的提示。由于属性可以包含任意字符串，因此可以将信息填充其中以备后用。对于 XUL 程序员来说，这是使用 `cookie` 的替代方案，尽管网络信息是自动可用的。

持久化的 RDF 文件称为 `localstore.rdf`，存储在用户配置文件中。对于在该处持久化的属性，有两个事实：XUL 文档（主体 URL）正在持久化（谓词）特定标签中的某项内容（对象）。这仅发生在给定标签中所有持久化的属性上。在第二个事实中，（主体 URL）需要一个等于属性名称的谓词/属性，以及一个对应属性值的字面量。列表 12.11 显示了 `editor.xul` 文档中 `id=editorwindow` 且具有 `width` 属性的标签的这些事实。

### Listing 12.11 localstore.rdf 中持久化事实的示例。

```
<RDF:Description about="chrome://editor/content/editor.xul">
<NC:persist resource="chrome://editor/content/editor.xul" width="884"/>
</RDF:Description>
```

```
<RDF:Description about="chrome://editor/content/editor.xul" width="884"/>
```

没有属性是默认持久化的。某些属性是由平台持久化的。最终，属性是否持久化取决于应用程序的设计，而不是平台能力。每个属性的持久化值是当前持有的值。在 XUL 中未设置属性的情况下，值会被写入。

应用程序程序员添加到 XUL 的提示确保了属性被记住。这种提示通过此 XUL 属性给出：

`persist` 可以包含逗号或空格分隔的属性列表。除了自动保存的属性外，这保留了窗口的布局方向。

## 12.4 相关 AOM 和 XPCOM 对象

覆盖和注册表系统使用这些 XPCOM 功能实现：

```
@mozilla.org/chrome/chrome-registry;1 nsChromeRegistry
```

此接口上的少数方法允许对覆盖系统进行简单操作，但它们不允许程序员手动驱动覆盖系统。使用此接口的理由很少，除非你正在构建 DOM 检查器或自定义安装系统。

要在 JavaScript 中持久化属性，请使用此方法：

```
document.persist(tagid, attname);
```

这将持久 `id` 等于 `tagid` 的标签的 `attname` 属性的值。

## 12.5 动手操作：NoteTaker 工具栏

在这次简短的“动手操作”课程中，我们将 NoteTaker 工具栏从 XUL 片段转换为正确合并到 Mozilla 窗口的覆盖层。执行此操作的简单。

- 找到一个可将 NoteTaker 工具栏合并到经典浏览器窗口的 `id`。
- 找到一个可将工具 NoteTaker 菜单项合并到经典浏览器窗口的 `id`。
- 检查 `chrome` 内容查看其他可能需要合并 `id` 的内容。
- 更新 `chrome` 内容以包含 NoteTaker 项、合适的 `id` 以及 `<overlay>` 标签。
- 更新 `chrome` 注册表以记录覆盖层的存在。
- 删除现有的覆盖数据库并重启平台以查看结果。

要找到 `id`，我们需要经典浏览器应用程序的主 XUL 文档（即包含 `<window>` 标签的文档）。

# 叠加层（Overlays）与 Chrome 第12 章

浏览 `chrome` 目录，唯一可能包含浏览器应用程序的文件是 `comm.jar`，它是 Communicator（Netscape Communicator 套件）的缩写。这个 `.jar` 包含了大量分布在许多子目录中的 XUL 文件，但如果我们查看这些文件，很明显，其中许多是 `<dialog>`、`<page>` 或 `<overlay>` 文档。在 `content/navigator` 中，`.jar` 的大部分内容是 `navigator.xul` 文件，它具有这个实用的开头：

```
<window id="main-window"> >
```

我们通过直接加载这个 `navigator.xul` 文件来测试它是否是类浏览器（Class Browser）的起始点：

```
mozilla -chrome "chrome://navigator/content/navigator.xul"
```

如果我们这样做，就会发现该文件是浏览器应用程序的正确起始点。所需的 `id` 要么在该文件中，要么在合并到此文档的某个叠加层中。我们可以通过对最终合并的文档使用 DOM 检查器（Inspector）来寻找合适的 `id`，也可以直接检查源代码，这需要列出所有使用的叠加层。要获取这些叠加层的完整列表，请添加以下方法：

- 直接在 `navigator.xul` 中使用 `?xul-overlay-?` 标签声明的叠加层。
- 在平台目录下的 `chrome/overlayinfo/navigator/contents/overlays.rdf` 文件中为 `chrome://navigator/content/navigator.xul` 声明的叠加层。
- 对第一遍及后续扫描中发现的所有叠加层文件重复上述两点。

在我们的情况下，这种列表是不必要的，因为 `navigator-xul` 文件本身就包含了合适的 `id`。

对于 NoteTaker 工具栏项，我们找到了：

```
<toolbox id="navigator-toolbox" class="toolbox-top" defferattached="true">
```

对于 NoteTaker Tools 菜单项，我们找到了：

```
<menu id="tasksMenu">
<menupopup id="tasksPopup">
```

`<menupopup>` 标签是一个额外菜单项的站点。它可能不是新项目的理想位置，但我们只是在尝试让它运行起来。

在浏览我们的工具栏代码后，我们还看到 `<commandset>` 也需要合并进来。为了这一点，我们需要在 `navigator.xul` 中：

```
<commandset id="commands">
<script> // 内容会被立即解释，不需要合并。
```

## 12.5 动手实践：NoteTaker 工具栏

为了与现有的命名命名一致，我们将 `toolbar.xl` 重命名为 `browserOverlay.xl` 并更改了它的内容。该文件的最终结构如列表 12.12 所示。

### 列表 12.12 NoteTaker 工具栏的叠加层结构。

```
<xml version="1.0"?>
<!DOCTYPE xfile>
<overlay xmlns="http://www.mozilla.org/keymaster/gatekeeper/
      there:is.only.xul">
  <script src="controllers.js" />
  <script src="toolbar_action.js" />
  <commandset id="commands">
    existing commands go here ...
  </commandset>
  <menupopup id="taskPopup">
    <menuitem label="Edit Note" command="notetaker.toolbar.command.edit"//>
  </menupopup>
  <toolbox id="navigator-toolbox">
    <toolbar id="notetaker-toolbar">
      existing toolbar content goes here ...
    </toolbar>
  </toolbox>
</overlay>
```
