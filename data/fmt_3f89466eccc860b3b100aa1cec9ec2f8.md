
```html
<tree id="dialog.reader" hideocolumnpicker="true" setype="single" flex="1">
  <treecol>
    <treecol id="tree.all" hideheader="true" flex="1" primary="true"/>
    <treechildren flex="1">
      <treitem container="true" open="true">
        <treerow><treecell label="checkpointed"></treerow>
        <treechildren>
          <treitem>
            <treerow><treecell label="breakdown"></treerow>
          </treitem>
          <treitem>
            <treerow><treecell label="first draft/"></treerow>
          </treitem>
          <treitem>
            <treerow><treecell label="final/"></treerow>
          </treitem>
        </treechildren>
      </treitem>
      <treitem container="true" open="true">
        <treechildren>
          <treitem>
            <treerow><treecell label="reviewed"></treerow>
          </treitem>
          <treitem>
            <treerow><treecell label="guru"></treerow>
          </treitem>
          <treitem>
            <treerow><treecell label="rubbish"></treerow>
          </treitem>
        </treechildren>
      </treitem>
      <treitem container="true" open="true">
        <treechildren>
          <treitem>
            <treerow><treecell label="fun/"></treerow>
          </treitem>
          <treitem>
            <treerow><treecell label="cool/"></treerow>
          </treitem>
        </treechildren>
      </treitem>
  </treecol>
</tree>
```

此树中的关键字以层级结构的形式显示，但并不意味着它们是父键的子主题。人们很容易倾向于这样认为，但实际上它们是相关的概念。一个 Web 页面可以接收带有“guru”关键字的笔记，但如果用户决定“guru”意味着作者有名，而不是页面包含深思熟虑的信息，那么它可能就不会带有“reviewed”关键字。

像 `<tree>` 标签这样的层级显示适用于分层拆解材料，但也适用于其他问题。

我们正在使用它来展示形成简单网络的关系。我们不是将网络视为一个整体，而是从一组起点开始发现它的部分。这与第 14 章“模板”中的 RDF 查询相似，但这里使用的是熟悉的 XUL 和 JavaScript 技术。

### 13.5.2 事件处理器的系统化使用

这是该列表框的工作原理。用户输入新关键字。点击“添加”将输入的关键字放入右上角的列表中；点击“删除”将将其从列表中移除。点击列表中的某项会将该项复制到文本框中。如果选择了列表项，树中匹配的项将被选中并滚动到视图。如果点击了树中的项，它将被复制到树中。

所有这些动作都可以作为命令来实现。然而，这些动作中的某些相当微不足道。对每一个脚本片段都编写命令可能是大材小用。这些动作中听起来都不像“事务”、“指令”或“操作”。它们仅仅是 GUI 的调整。我们将使用事件来实现它们。

我们可以将这些事件处理器添加到单个 `<listbox>` 和 `<tree>` 内容标签中（`onclick= ...`），但我们希望支持自定义操作，这些操作类似于本地命令（参见通过 `performAction` 修复的树视图方法）。我们不这样做。对于我们的计划事件，我们需要：

```
“添加”按钮上的 onclick
“删除”按钮上的 onclick
<listbox> 上的 onselect
<tree> 上的 none
```

相比于 XUL 语法，我们将选择一个更有趣的选项。我们将使用 DOM 2 事件“EventTarget”接口，特别是 `addEventListener()` 方法。该方法适用于每个 DOM 对象，这意味着它适用于大多数 XUL 标签。通过脚本，我们将在编辑对话框首次加载时安装所有事件处理器。列表 13.8 显示了如何设置。

#### 列表 13.8. NoteTaker 关键字的事件处理器安装。

```javascript
var ids = {};

function init_handlers() {
  var handlers = [
    // id             处理函数
    ["dialog.add", "click", add_click],
    ["dialog.delete", "click", delete_click],
    ["dialog.keywords", "select", keywords_select],
    ["dialog.related", "select", related_select]
  ];
```

## 13.5 动手实践：NoteTaker：关键词面板

```javascript
var items = document.getElementsByTagName('treecell');
for (var i = 0; i < items.length; i++) {
  if (items[i].getAttribute('label') == textbox.value) {
    item = items[i].parentNode.parentNode;
    break;
  }
}

if (item) {
  selected = item;
  if (tree.view.indexOfItem(item) == -1) {
    while (item.tagName != 'tree') {
      if (item.getAttribute('container') != '') {
        item.setAttribute('open', 'true');
      }
      item = item.parentNode.parentNode;
    }
  }
}
// tree.currentIndex = tree.view.indexOfItem(selected);
// only selects the focus, not the selection.
i = tree.view.indexOfItem(selected);
tree.treeBoxObject.selection.select(i);
tree.treeBoxObject.ensureVisible(i);
```

此函数将当前选定列表项的标签复制到文本框中。这只需要一行代码。函数的其余部分是在树中搜索并高亮关键词（如果存在的话）。表 13.4 中描述的树接口仅适用于树的渲染行（包括由周围滚动框包含的行）。如果找到了关键词，视图接口将找到它。我们必须使用 DOM 来搜索整个树。找到适当的项目后，我们可以遍历树来管理树的显示。

在获取关键词时，我们在 `<listbox>` 处遇到了第二个棘手的问题。`currentItem` 这个 XBL 属性没有被正确维护；当列表框没有选定元素时，它的创建方式糟糕。尽管这并不显而易见，但如果我们不处理，就会向控制台抛出错误。这些错误的发生是因为我们的 `onclick` 处理程序恰好在列表框滚动时被调用。树 `()` 处理程序捕获了这种特殊情况并终止了处理程序，因为在这种情况下无事可做。
