
剩余文本。`re.sub()`（“替换”）方法将待处理的文本作为其第二个参数；其第一个参数要么是一个字面量字符串，用于替换每次匹配的内容，要么是一个要调用的函数。在函数的情况下，对于每次匹配，都会将一个匹配对象传递给该函数，并使用该函数的返回值（应当是一个字符串）作为替换字符串。

在几个地方，我们会检查 `stopped` 变量是否为 `True`，如果调用了 `stop()` 方法，该变量就会是 `True`。如果发生这种情况，我们不再进行进一步的索引，直接返回。如果检查的次数太少，用户在请求停止索引和线程实际停止之间可能会经历延迟。但另一方面，如果我们放置的检查越多，线程的运行速度就越慢。因此，多久检查一次，以及将检查放在哪里，可能需要经过一番尝试和错误才能弄对。

```
for word in self.SPLIT_RE.split(text):
    if self.MIN_WORD_LEN <= len(word) <= \
        self.MAX_WORD_LEN and \
        word[0] not in self.INVALID_FIRST_OR_LAST and \
        word[-1] not in self.INVALID_FIRST_OR_LAST:
        try:
            self.lock.lockForRead()
            new = word not in self.commonWords
        finally:
            self.lock.unlock()
        if new:
            words.add(word)
    if self.isStopped():
        return
for word in words:
    try:
        self.lock.lockForWrite()
        files = self.filenamesForWords[word]
        if len(files) > self.COMMON_WORDS_THRESHOLD:
            del self.filenamesForWords[word]
            self.commonWords.add(word)
        else:
            files.add(unicode(fname))
    finally:
        self.lock.unlock()
self.emit(SIGNAL("indexed(QString)"), fname)
self.completed = True
```

对于文件文本中的每个单词，如果它既不过长也不过短，且不以不可接受的字符开头，我们首先查看它是否位于常用词集合中；如果不在，则将其添加到本地的单词集合中。

一旦我们将文件的所有非常用单词都收集到 `words` 集合中，我们就遍历该集合。新单词会被添加到 `filenamesForWords` 默认字典中。如果该字典中针对某个单词的文件名集合过大，我们就删除该字典项并将该单词添加到常用词集合中；否则，我们将当前单词的文件名添加到该单词在字典中的集合中。当然，我们必须使用写锁来确保当这些对象正在被更新时，没有其他线程（例如主线程）可以访问该字典或常用词集合。

文件索引完成后，`indexed()` 信号会以文件名作为参数被发出。主线程连接了该信号，并在一个标签中显示文件名，以便用户可以看到刚刚索引了哪个文件。

一旦 `os.walk()` 循环结束，`completed` 变量就会被设置为 `True`，方法结束，控制权返回给调用者 `run()`。最后一条语句可能永远不会执行，因为如果用户停止索引（通过按 Esc 键，这会调用 `stop()`，将 `stopped` 设置为 `True`，这意味着 `isStopped()` 将返回 `True`），其中一个 `if isStopped():` 语句会导致 `processFiles()` 方法立即返回。在这种情况下，`completed` 变量（正确地）将为 `False`。

至此，我们完成了对 walker 线程的回顾。使用 `with` 语句和上下文管理器代替 `try...finally` 代码块，可以使代码更短、更易理解。通过比较 `pagedindexer.pyw` 与 `pagedindexer_26.pyw`，以及 `walker.pyw` 与 `walker_26.py` 可以看出这一点。对于服务于主线程的次要线程来说，拥有一个 `stop()` 方法和一个 `stopped` 变量非常常见，因此 `Walker` 类虽然在具体处理上具有特殊性，但在结构上却相当通用。

## 总结

使用 PyQt 的线程和网络类编写多线程服务器相对简单。对于非 GUI 服务器，可以使用 `QCoreApplication` 而不是 `QApplication`，或者完全避免使用 PyQt 类，转而依赖 Python 标准库的线程和网络类，或使用 Twisted。

理论上，将处理任务分配给次要线程并不困难，但在实践中，我们必须非常小心，确保任何可被多个线程访问的数据都使用了保护机制，例如 `QMutex`、`QReadWriteLock` 或 `QSemaphore`。在保护机制的上下文中，我们必须确保完成尽可能少的工作，以最小化其他线程可能被阻塞的时间。并且，在读取数据的情况下，尤其是当数据量不是很大的时候，最好将其复制一份，以避免在保护范围之外访问数据的风险。

主线程通过调用次要线程的方法与次要线程进行通信非常常见——例如，调用 `start()` 来启动它们，调用 `stop()` 来停止它们。次要线程可以通过发出主线程连接到的信号与主线程进行通信。主线程和次要线程还可以使用由 `QMutex`、`QReadWriteLock` 或 `QSemaphore` 保护的共享数据结构——一种常见的场景是主线程读取，而次要线程读写共享数据。线程可能需要保护对自身数据的访问——例如对次要线程的 `stopped` 变量的访问——因为它们可能有多个方法同时处于活动状态（例如，次要线程中的 `run()` 和 `stop()` 都活动）。

多线程程序比单线程程序更难编写和维护，因此，探索更简单的替代方案通常是有价值的，例如调用 `QApplication.processEvents()` 或使用 `QProcess` 调用外部进程。

## 练习

修改页面索引器应用程序，使其使用多个次要线程，而不仅仅是一个。通过确定次要线程的正确数量，可以使应用程序运行得比单个次要线程版本更快。虽然这个练习只需要编写或修改大约 100 行代码，但它相当微妙且具有挑战性。

解决方案采取的方法是，将 `os.walk()` 移到主线程中，并创建一个文件名列表。每当列表中有 1000 个文件时，就创建一个次要线程来处理这些文件。最后，再创建另一个次要线程来处理剩余的文件。由于我们可以将所有参数传递给构造函数，因此不需要 `Walker.initialize()` 方法。对 `Walker.run()` 和 `Walker.processFiles()` 的修改也非常小。大多数修改必须在 `pageindexer.py` 文件中进行。

`setPath()` 方法是收集文件名并创建处理它们的次要线程的地方。在解决方案中，我们使用了一个独立的方法来创建次要线程。由于可能存在许多次要线程，我们还添加了一个 `stopWalkers()` 方法，并修改了 `finished()`、`accept()`、`reject()` 和 `finishedIndexing()` 方法。由于用户界面中的某些控件可能会响应来自多个线程的信号而被访问，因此我们使用互斥锁来保护对这些控件的访问。

确保在线程不再需要时删除它们，以避免每次调用 `setPath()` 时都创建越来越多的线程。

新的 walker 模块版本应该比原始版本稍短，但新的页面索引器将比原始版本长约 90 行。解决方案提供在 `chap19/pageindexer_ans.py` 和 `chap19/walker_ans.py` 中。

## 这还不是终点

我们已经到达了本书的结尾，但远未到达 Python 或 PyQt 所能提供的一切的尽头。Python 的标准库非常大，由于我们将重点放在 PyQt 上，我们几乎只使用其中很小的一部分。还有许多其他库也作为 Python 和 PyQt 的附加组件可用，因此在许多情况下，我们可以通过组合现有组件进行编程，而不必自己从零开始构建所有内容。寻找附加组件的一个好去处是位于 http://pypi.python.org/pypi 的 Python 软件包索引。寻找技巧、提示和想法的一个好去处是位于 http://aspn.activestate.com/ASPN/Python/Cookbook 的 *Python Cookbook*。

我们对 PyQt 的讲解很全面，并且已经展示并描述了所有主要功能。但 PyQt 有数百个类，因此我们无法涵盖甚至提及所有类。例如，PyQt 包含比我们使用的更多的控件，包括 `QCalendarWidget`、`QGroupBox`、`QProgressBar` 和 `QToolTip`。还有许多有用的非控件类，例如 `QCompleter`（文本补全）、`QFileSystemWatcher`（用于观察文件系统中文件或目录的变化）和 `QSystemTrayIcon`（用于在系统托盘中放置带有弹出菜单的图标）。它还具有对可访问性和撤销/重做框架的支持。此外，PyQt 拥有一些特定于平台的功能，包括 Windows 上的 ActiveX 支持、X Window 系统上的会话管理，以及 Mac OS X 上的 sheets 和 drawers。这些都在广泛的在线文档中有描述。PyQt 还提供了其自己的示例集——那些覆盖你感兴趣的领域的示例非常值得一看。

这本书为使用 Python 和 PyQt 进行 GUI 编程打下了坚实的基础。它所展示的原则和做法应该使从随 PyQt 提供的文档和示例中学习新的 PyQt 类变得轻而易举，并使你能成功创建自己的类。使用 PyQt 进行编程既高效又令人愉快，它让我们可以自由地忽略不相关的细节。这意味着我们可以专注于构建外观精美且运行良好的优秀应用程序。
