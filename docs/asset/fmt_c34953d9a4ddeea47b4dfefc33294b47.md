
```python
    @pyqtSignature("")
    def on_replaceButton_clicked(self):
        regex = self.makeRegex()
        self.__text = regex.sub(unicode(self.replaceLineEdit.text()),
                                self.__text, 1)
```

这个方法很简单，因为它将准备工作交给 `makeRegex()` 方法。我们使用 `sub` 方法（“替换”）将查找文本的第一次出现替换为替换文本。替换文本可以是空的。这里的 `1` 是最大替换次数。

```python
    @pyqtSignature("")
    def on_replaceAllButton_clicked(self):
        regex = self.makeRegex()
        self.__text = regex.sub(unicode(self.replaceLineEdit.text()),
                                self.__text)
```

这个方法与前面的那个几乎相同。唯一的区别是我们没有指定最大替换次数，因此 `sub()` 将替换它找到的尽可能多的（非重叠）查找文本出现。

至此，我们已经实现了 `FindAndReplaceDlg`。该对话框方法的实现与我们之前所做的没有太大区别，除了我们使用装饰器和 `setupUi()` 来提供自动连接。

要在应用程序中使用该对话框，我们必须确保生成了 `ui_findandreplacedlg.py` 模块文件，并且必须导入我们刚写的 `findandreplacedlg` 模块。我们将在下一节中看到表单是如何创建和使用的。

## 测试对话框

由于任何 PyQt 小部件（包括任何对话框）都可以作为顶级窗口独立使用，因此实例化对话框并启动事件循环来测试它很容易。不过，我们通常需要做一些额外的工作。例如，我们可能需要设置一些初始数据，或者提供方法来接收对话框的信号，以便我们可以检查它们是否正常工作。

就查找和替换对话框而言，我们需要一些初始文本，并且需要检查连接是否正常工作，以及查找和替换方法是否有效。

因此，在 `findandreplacedlg.py` 文件的末尾，我们添加了一些额外代码。这段代码仅在文件独立运行时执行，因此它不会影响性能，也不会在对话框在应用程序中使用时干扰其使用。

```python
if __name__ == "__main__":
    import sys
    text = """US experience shows that, unlike traditional patents,
software patents do not encourage innovation and R&D, quite the
contrary. In particular they hurt small and medium-sized enterprises
and generally newcomers in the market. They will just weaken the market
and increase spending on patents and litigation, at the expense of
technological innovation and research. Especially dangerous are
attempts to abuse the patent system by preventing interoperability as a
means of avoiding competition with technological ability.
--- Extract quoted from Linus Torvalds and Alan Cox's letter
to the President of the European Parliament
http://www.oeffi.org/patentit/patentis_torvalds_cox.html"""

def found(where):
    print "Found at %d" % where

def nomore():
    print "No more found"

app = QApplication(sys.argv)
form = FindAndReplaceDlg(text)
form.connect(form, SIGNAL("found"), found)
form.connect(form, SIGNAL("notfound"), nomore)
form.show()
app.exec_()
print form.text()
```

我们首先导入 `sys` 模块，然后创建一段要处理的文本。接下来，我们为对话框的信号连接创建几个简单的函数。

我们以正常方式创建 `QApplication` 对象，然后创建对话框的一个实例，并传入我们的测试文本。我们将对话框的两个信号连接到我们的槽，并调用 `show()`。然后我们启动事件循环。当事件循环终止时，我们打印对话框的文本；如果用户替换了一些文本，这将与原始文本不同。

现在，该对话框可以从控制台运行并进行测试。

```
C:\pyqt\chap07>python findandreplacedlg.py
```

除非使用自动测试工具，否则为对话框添加测试功能通常很有帮助。编写它们不需要花费太多时间和精力，而且每次对话框逻辑发生变化时运行它们有助于将引入 bug 的可能性降到最低。

有时我们将复杂对象传递给对话框，这可能看起来使测试变得不可能。但得益于 Python 的鸭子类型，我们总是可以创建一个假类，模拟足够的行为以用于测试。例如，在第 12 章中，我们使用属性编辑器对话框。该对话框对“Node”对象进行操作，因此在测试代码中，我们创建一个 `FakeNode` 类，提供设置和获取 `node` 属性的方法，而对话框会用到这些方法。（相关文件是 `chap12/propertiesdlg.ui`，由此生成 `ui_propertiesdlg.py`，以及 `chap12/propertiesdlg.py`，其中实现了 `PropertiesDlg`。）

## 总结

Qt Designer 提供了一种快速简便的方式创建用户界面。使用可视化设计工具使得判断设计是否“有效”变得容易得多。Qt Designer 的另一个好处是，如果我们更改设计，只要我们没有添加、删除或重命名我们在代码中引用的任何小部件，我们的代码就不需要做任何更改。即使我们确实添加、重命名或删除了小部件，对代码的更改也可能很小，因为 Qt Designer 为我们处理了所有小部件的创建和布局。

使用 Qt Designer 的基本原则始终相同：我们将小部件拖放到表单上，先是容器（如框架、组合框和选项卡小部件），然后是普通小部件，并设置它们的属性。然后我们添加间隔符以占据空隙。接下来我们选择特定的小部件、间隔符和布局，并应用布局到它们，重复此过程直到所有布局完成。然后我们对表单本身进行布局。最后我们设置伙伴、选项卡顺序和信号-槽连接。

实现由 Qt Designer 创建用户界面的对话框与手动实现类似。最大的区别在于初始化器，其中我们只是调用 `setupUi()` 来创建和布局小部件，并创建信号-槽连接。我们实现的方法可以像以前一样完成（代码也没有不同），但通常我们使用 `on_widgetName_signalName` 命名约定，并配合 `@pyqtSignature` 装饰器以利用 `setupUi()` 自动创建连接的能力。

我们尚未涵盖的一个用例是使用“Widget”模板创建复合小部件（由两个或更多其他小部件组合布局而成的小部件）。在某些情况下，这些小部件设计可用于整个表单，在其他情况下，它们可作为表单组件使用——例如，提供选项卡小部件或小部件堆栈的页面。或者两个或更多复合小部件可以在表单中一起布局以创建更复杂的表单。这是通过 Qt Designer 和以正常方式生成 Python 模块来实现的。然后我们可以导入生成的模块，并在我们的表单类中调用每个自定义小部件的 `setupUi()` 方法来创建用户界面。

关于对话框有多“智能”、应该具有什么模式以及如何验证的问题，对于用 Qt Designer 创建的对话框与手动创建的对话框没有区别。唯一的例外是我们可以用 Qt Designer 设置小部件属性——例如，我们可以设置自增框的范围和初始值。当然，我们也可以在代码中做同样的事情，但对于只需要简单验证的小部件，在 Qt Designer 中完成通常更方便。

我们必须使用 `pyuic4` 从 Qt Designer `.ui` 文件生成 Python 模块，无论是直接运行 `pyuic4`，还是使用 `mkspec.py` 或 `Make PyQt`，后者在存在 `.qrc` 文件时也会为资源文件生成 Python 模块。
