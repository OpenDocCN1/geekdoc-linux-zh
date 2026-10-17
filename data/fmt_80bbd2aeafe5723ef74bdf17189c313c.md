
```
<- current-page-url, keyword, ?keyword ->
- current-keyword-urn, related, ?keyword ->
```

模板查询必须在某处兼顾这两种情况。解决方案之一是对每种可能性使用一个 `<rule>`。在我们的情况下，`template` 属性是一个简单的解决方案。

![](img/319913ee37032862c03d285bfc49c7581_0.png)14.8 递归查询的 RDF 图。

我们幸运的是，对于任何 URI，要么具有 `related` 属性事实，要么具有 `keyword` 属性事实，但不同具备，这意味着我们可以同时使用多个容器谓词。我们将 `related` 和 `keyword` 属性列出。

为了查看，可以考虑查询过程。当查询发现树的顶层时，`keyword` 会找到解决方案，而 `related` 不会，因为这是事实在文件中的排列方式。当查询发现更深处的解决方案时，`related` 会找到，而 `keyword` 不会。这正是我们想要的。列表 14.24 显示了结果-模板。

### 列表 14.24 NoteTaker 编辑框的递归模板。

```
<tree id="dialog" flex="1">
  datasources="notetaker-rdf"
  rdf:type="http://saturn/courses/model2"
  containment="http://www.mozilla.org/notetaker-rdf#related http://www.mozilla.org/notetaker-rdf#keyword"
  hidecolspicker="true"

  <treecols>
    <treecol id="tree.all" header="true" primary="true" flex="1"/>
  </treecols>
  <template>
    <rule>
      <conditions>
        <content uri="?uri"/>
        <member container="?uri" child="?keyword"/>
      </conditions>
      <action>
        <children>
          <treeitem uri="?keyword">
            <trerow>
              <treecell label="?keyword"/>
            </trerow>
          </treeitem>
        </children>
      </action>
    </rule>
  </template>
</tree>
```

查询找到匹配 `containment` 属性的标签。由于这是一个递归查询，我们不能使用普通的 `<description>` 标签进行测试。我们必须使用明确指定递归查询的标签，在本例中为 `<tree>`。

因此，我们成功构建了递归查询。只需要添加图 14.8 中的辅助信息。这是通过 `<binding>` 标签实现的。我们在 `</condition>` 标签之后添加此内容：

```
<binding>
  <subject="?keyword">
  predicate="http://www.mozilla.org/notetaker-rdf#label"
  object="?text"/>
</binding>
```

由于 `<binding>` 标签对递归过程没有帮助，我们只是增强了它检索的信息。最后，我们必须更改 `<treecell>` 以报告绑定发现的标签，而不是关键词的 URN：

```
<treecell label="?text"/>
```

通过这些更改，我们完成了树的模板以及 NoteTaker 工具所需模板。尽管 `<listbox>` 和 `<tree>` 标签具有模板生成的内容，第 13 章 Listboxes and Trees 的事件处理程序仍然继续工作；它们可以像从 XUI 标签构建 DOM 结构一样轻松地浏览模板生成的内容。

我们对 `<tree>` 模板有一个问题。它没有像第 13 章 Listboxes and Trees 中的自定义视图那样显示相关键。这可以改进输出。

## 14.5 模板的协调与刷新

我们希望实现的最后一个功能是保持工具栏更新。这意味着做出以下更改：

- 1. 每当笔记更改时更新工具栏的 JavaScript 版本。
- 2. 提供一个更新工具栏的实用函数。
- 3. 更新新页面的文本框。
- 4. 工具栏上的删除按钮需要一个 `notetaker-delete` 命令。
- 5. 工具栏上的保存按钮需要一个 `notetaker-save` 命令。
- 6. `notetaker-open-dialog` 命令必须更新对话框上的下拉菜单。

为了实现这一点，我们必须将现有笔记对象实现为完整的 JavaScript 对象并定义其方法 `clear()` 和 `resolve()`。`clear()` 移除当前笔记数据；`resolve()` 将提供的 URL 转换为现有笔记的 URL 并记录结果。对于本章来说，这些更改是微不足道的，但我们以后需要扩展它们。新对象的代码如列表 14.25。

### 列表 14.25 NoteTaker 笔记的基础型 JavaScript 对象。

```javascript
function Note() {
  // 构造函数
}

Note.prototype = {
  url: "",
  summary: "",
  chop_query : true, home_page : false,
  width: 100, height: 90, top: 80, left: 70,
  clear: function () {
    this.url = null;
  },
  resolve : function (url) {
    this.url = url;
  }
};
```

其次，我们实现一个 `refresh_toolbar()` 函数来更新工具栏模板。该函数的部分内容我们将在后面的章节中修改。列表 14.26 显示了此函数。

### 列表 14.26 NoteTaker 工具栏的模板重建代码。

```javascript
function refresh_toolbar() {
  var menu = window.document.getElementById('notetaker-toolbar.keywords');
  menu.firstChild.child.rebuild();

  var box = window.document.getElementById('notetaker-toolbar.summary');
  box.parentNode.setAttribute('ref', note.url);
  box.parentNode.child.rebuild();
}
```

`rebuild()` 方法会导致模板生成的内容被移除并重建。对于下拉菜单，只有当底层的 RDF 文件发生变化时，内容才会改变。对于文本框，模板本身会被修改，因此每次重建时其查询结果都是不同的。

接下来，我们查看了定时检查。这些所有内容都是从 `content_poll()` 函数运行的，因此让我们重写它，使其随着显示的笔记更新工具栏。列表 14.27 显示了新版本。

### 列表 14.27 轮显示的 Web 页面并进行所有必要的更新。

```javascript
function content_poll() {
  var doc;
  try {
    if (!window.content) throw('fail');
    doc = window.content.document;
    if (!doc) throw('fail');
    if (doc.getElementsByTagName('body').length == 0) throw('fail');
    if (doc.location.href == "_blank") throw('fail');
  } catch (e) {
    note.clear();
    refresh_toolbar();
    return;
  }

  if (doc.visited) return;
  note.resolve(doc.location.href);
  display_note();
  refresh_toolbar();
  doc.visited = true;
}
```

如果不存在合适的 URL，则清除当前笔记和工具栏。否则，找到新的当前笔记并更新工具栏、笔记和当前页面。

我们无法完成剩余的任务 4 和 6，因为我们还不知道如何修改 RDF 文件——我们只知道如何读取它们。然而，我们可以完成被提名命令的模板更新部分。我们更新了 `action()`，在任何需要的地方调用 `refresh_toolbar()`。列表 14.28 显示了这段特定的代码。
