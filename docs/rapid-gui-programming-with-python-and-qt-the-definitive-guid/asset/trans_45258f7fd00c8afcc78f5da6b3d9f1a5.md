
## finally:
self.lock.unlock()
self.wordsIndexedLCD.display(indexedWordCount)
self.commonWordsLCD.display(commonWordCount)

elif self.fileCount % 10 == 0:
    self.commonWordsListWidget.clear()
    try:
        self.lock.lockForRead()
        words = self.commonWords.copy()
    finally:
        self.lock.unlock()
    self.commonWordsListWidget.addItems(sorted(words))

每当 walker 线程完成一个文件的索引时，它会发出一个带有文件名的 `indexed()` 信号；该信号连接到前面所示的 `form_indexed()` 方法。我们更新状态标签以显示刚刚完成索引的文件名，并且每处理 25 个文件时，我们也更新文件计数、已索引单词数以及常用单词 LCD 小部件。我们使用读锁来确保共享数据结构可以被安全地读取，并且我们在锁的上下文中执行最少的工作量，仅在锁释放后才更新 LCD 小部件。

每处理第 10 个文件时，我们更新常用单词列表小部件。同样，我们使用读锁，并使用 `copy()` 来确保在锁释放后不引用共享数据。

```python
def finished(self, completed):
    self.statusLabel.setText("Indexing complete" \
        if completed else "Stopped")
    self.finishedIndexing()
```

当线程被停止或完成时，它会发出 `finished()` 信号，该信号连接到此方法并传递一个布尔值以指示是否已完成。我们更新状态标签并调用 `finishedIndexing()` 方法来更新用户界面。

```python
def finishedIndexing(self):
    self.walker.wait()
    self.filesIndexedLCD.display(self.fileCount)
    self.wordsIndexedLCD.display(len(self.filenamesForWords))
    self.commonWordsLCD.display(len(self.commonWords))
    self.pathButton.setEnabled(True)
```

当索引完成时，我们调用 `QThread.wait()` 以确保线程的 `run()` 方法已结束。然后，我们基于共享数据结构的当前值更新用户界面。由于 walker 线程未运行，因此我们不需要保护对字典或集合的访问。

## 使用上下文管理器进行解锁

在本章中，我们使用 `try ... finally` 块来确保锁在使用后被解锁。Python 2.6 提供了一种替代方法，使用新的 `with` 关键字，结合上下文管理器。上下文管理器在 [PEP 343](http://www.python.org/dev/peps/pep-0343) 中进行了说明；简而言之，我们可以通过创建一个具有两个特殊方法的类来创建上下文管理器：`__enter__()` 和 `__exit__()`。然后，代替编写如下的代码：

```python
try:
    self.lock.lockForRead()
    found = word in self.commonWords
finally:
    self.lock.unlock()
```

我们可以编写更简单、更短的内容：

```python
with ReadLocker(self.lock):
    found = word in self.commonWords
```

这是因为传递给 `with` 语句的对象的语义（在最简单的情况下）如下：

```python
ContextManager.__enter__()
try:
    # 语句，例如 found = word in self.commonWords
finally:
    ContextManager.__exit__()
```

`ReadLocker` 上下文管理类本身也很容易实现，假设它接收一个 `QReadWriteLock` 对象：

```python
class ReadLocker:
    def __init__(self, lock):
        self.lock = lock

    def __enter__(self):
        self.lock.lockForRead()

    def __exit__(self, type, value, tb):
        self.lock.unlock()
```

事实上，从 PyQt 4.1 开始，`QReadLocker` 和 `QWriteLocker` 可以用作上下文管理器，因此在使用 Python 2.6（或使用 `from __future__ import with statement` 的 Python 2.5）时，我们不需要使用 `try ... finally` 来保证解锁，而是可以编写如下的代码：

```python
with QReadLocker(self.lock):
    found = word in self.commonWords
```

`chap19` 中的文件 `pageindexer_26.py` 和 `walker_26.py` 使用了这种方法。

在索引过程中的任何时刻，用户都可以与用户界面交互，而不会出现冻结或性能下降。特别是，他们可以在查找行编辑框中输入文本并按下 Enter 键，从而在文件列表小部件中填充包含所输入单词的那些文件。如果他们在每次按下 Enter 键之间稍作停顿并按了多次，文件列表可能会发生变化，因为在间隔期间可能已经索引了更多的文件。`find()` 方法稍微长一些，因此我们将分两部分回顾它。

```python
def find(self):
    word = unicode(self.findEdit.text())
    if not word:
        self.statusLabel.setText("Enter a word to find in files")
        return
    self.statusLabel.clear()
    self.filesListWidget.clear()
    word = word.lower()
    if " " in word:
        word = word.split()[0]
    try:
        self.lock.lockForRead()
        found = word in self.commonWords
    finally:
        self.lock.unlock()
    if found:
        self.statusLabel.setText(
            "Common words like '%s' are not indexed" % word)
        return
```

如果用户输入一个要查找的单词，我们清空状态标签和文件列表小部件，并在常用单词集合中查找该单词。如果找到了该单词，则它太常见而不会被索引，因此我们只给出一个信息性消息并返回。

```python
    try:
        self.lock.lockForRead()
        files = self.fileNamesForWords.get(word, set()).copy()
    finally:
        self.lock.unlock()
    if not files:
        self.statusLabel.setText(
            "No indexed file contains the word '%s'" % word)
        return
    files = [QDir.toNativeSeparators(name) for name in \
             sorted(files, key=unicode.lower)]
    self.filesListWidget.addItems(files)
    self.statusLabel.setText(
        "%d indexed files contain the word '%s'" % (
            len(files), word))
```

如果用户的单词不在常用单词集合中，它可能在索引中。我们使用读锁访问 `filenamesForWords` 默认字典，并复制与单词匹配的文件集合。如果没有文件包含该单词，集合将为空，但无论哪种情况，我们拥有的集合都是副本，因此不存在在锁上下文之外访问共享数据的风险。如果有匹配的文件，我们将它们添加到文件列表小部件中，排序并使用时本平台原生的路径分隔符。

`sorted()` 函数返回其第一个参数（例如列表或集合）的排序顺序。可以将比较函数作为第二个参数提供，但在这里我们指定了一个“key”。这会产生 DSU（装饰、排序、还原）排序效果，其等价于：

```python
templist = [(fname.lower(), fname) for fname in files]
templist.sort()

files = [fname for key, fname in templist]
```

这比使用比较函数更高效，因为每个项目只被小写化一次，而不是在每次用于比较时都进行小写化。

```python
def reject(self):
    if self.walker.isRunning():
        self.walker.stop()
        self.finishedIndexing()
    else:
        self.accept()
```

如果用户按下 Esc，则调用 `reject()` 方法。如果正在索引，我们在线程上调用 `stop()`，然后调用 `finishedIndexing()`；`finishedIndexing()` 方法调用 `wait()`。否则，索引要么已被之前的 Esc 键按下停止，要么已结束；无论哪种情况，我们都调用 `accept()` 来终止应用程序。

```python
def closeEvent(self, event=None):
    self.walker.stop()
    self.walker.wait()
```

当应用程序被终止时，无论是通过 `reject()` 方法中发生的 `accept()` 调用，还是通过其他方式（例如用户点击关闭 X 按钮），都会调用关闭事件。在这里，我们确保索引已停止且线程已结束，以确保干净地终止。

所有的索引工作都由 walker 辅助线程完成。该线程由主线程调用其方法（例如 `start()` 和 `stop()`）进行控制，并通过 PyQt 的信号和槽机制通知主线程其状态（文件已索引、索引完成）。共享数据被访问——例如，当用户询问哪些文件包含特定单词，或当数据被 walk-
