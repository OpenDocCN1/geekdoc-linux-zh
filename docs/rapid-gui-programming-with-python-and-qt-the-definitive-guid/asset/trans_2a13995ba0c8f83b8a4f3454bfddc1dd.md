
## 实现次级线程

页面索引器的次级线程实现在 `chap19/walker.py` 文件中的 `Walker` 类里。该类是 `QThread` 的子类，使用 `QMutex` 来保护其对自身私有数据的访问，并使用传入的 `QReadWriteLock` 来保护它与被主线程共享的数据的访问。

```python
class Walker(QThread):
    COMMON_WORDS_THRESHOLD = 250
    MIN_WORD_LEN = 3
    MAX_WORD_LEN = 25

    INVALID_FIRST_OR_LAST = frozenset("0123456789_ ")
    STRIPTHML_RE = re.compile(r"<[^>]*?>", re.IGNORECASE|re.MULTILINE)
    ENTITY_RE = re.compile(r"&(\w+?);|&\#\(d+?);", re.IGNORECASE)
    SPLIT_RE = re.compile(r"\W+", re.IGNORECASE|re.MULTILINE)
```

该类以一些静态变量开始，这些变量控制一个单词在多少个文件中出现后才被视为常用词，单词的最小和最大长度，以及单词不能以哪些字符开头或结尾。“剥离 HTML”正则表达式用于剥离 HTML 标签，实体正则表达式用于提取需要转换为 Unicode 字符的实体，而分割正则表达式用于将文件的文本分割成其组成的单词。一个更现实的应用程序可能会使用 HTML 解析器而不是正则表达式。

```python
def __init__(self, lock, parent=None):
    super(Walker, self).__init__(parent)
    self.lock = lock
    self.stopped = False
    self.mutex = QMutex()
    self.path = None
    self.completed = False
```

应用程序创建一个 walker 线程对象，但并不立即启动它。这个锁是主线程使用的同一个 `QReadWriteLock`——walker 线程使用它来保护对所有共享的 `filenamesForWords` 默认字典和 `commonWords` 集合的访问。`stopped` 变量用于在类内部判断线程是否已被请求停止（通过调用 `stop()` 方法）。`mutex` 用于保护 walker 线程自身对 `stopped` 变量的访问。这是必要的，因为当 `run()` 方法正在执行时，线程的其他方法（如 `stop()`）可能会被调用。`completed` 变量用于指示当线程停止时，索引是否已完成。

```python
def initialize(self, path, filenamesForWords, commonWords):
    self.stopped = False
    self.path = path
    self.filenamesForWords = filenamesForWords
    self.commonWords = commonWords
    self.completed = False
```

此方法设计用于在调用 `QThread.start()` 之前调用，以便为执行索引准备线程。当线程正在运行时不应调用此方法。（如果我们非常谨慎的话，可以在开头添加 `if not self.isStopped(): return`。）

虽然使用互斥锁和读写锁是无害的，但两者都不是必须的。当调用此方法时，walker 线程并未运行，因此对 `stopped` 进行赋值没有问题；而对于传入的字典和集合，我们只是获取它们的引用，并未以任何方式改变它们。

```python
def run(self):
    self.processFiles(self.path)
    self.stop()
    self.emit(SIGNAL("finished(bool)"), self.completed)
```

当调用者调用 `start()` 时，线程会依次调用 `run()` 方法——这是我们必须永远不要自己执行的操作。该方法只有三条语句，但 `processFiles()` 可能需要很长时间才能执行完，因为它涉及递归读取和索引路径下所有的 HTML 文件。不过这不是问题，因为处理是在 walker 线程自己的执行线程中进行的，所以用户界面保持响应状态，主线程可以调用 walker 线程的方法，并响应 walker 线程的信号，正如我们在前一节中看到的那样。最后，`run()` 方法发出一个 `finished()` 信号，带有一个布尔标志，指示索引是否完成；如果没有完成，说明用户一定通过用户界面停止了它。

```python
def stop(self):
    try:
        self.mutex.lock()
        self.stopped = True
    finally:
        self.mutex.unlock()
```

这会阻塞，直到获得锁为止，并且由于 `try ... finally` 块的存在，保证了最终互斥锁会被解锁。

如果我们使用的是 Python 2.6，或者带有适当 `from __future__` 语句的 Python 2.5，我们可以将这个方法重写为：

```python
def stop(self):
    with QMutexLocker(self.mutex):
        self.stopped = True
```

从 PyQt 4.1 开始，`QMutexLocker` 类可以用作上下文管理器。它会锁定作为参数传入的 `QMutex`（阻塞直到可以获得锁），并在控制流离开 `with` 作用域时解锁互斥锁（即使作用域是因异常而退出的）。

```python
def isStopped(self):
    try:
        self.mutex.lock()
        return self.stopped
    finally:
        self.mutex.unlock()
```

请注意，`return` 语句位于 `try ... finally` 块内部。当执行到 `return` 时，方法将尝试返回值，但会被强制进入 `finally` 块，之后方法将带着 `return` 语句的值返回。

如果我们使用的是 Python 2.6（或带有适当 `from __future__` 语句的 2.5），我们可能完全省略这个方法，并且在其他一些方法中，而不是写：

```python
if self.isStopped():
    return
```

我们可以这样写：

```python
with QMutexLocker(self.mutex):
    if self.stopped:
        return
```

这些方法中任何一个的开销不应该有显著差异，尽管使用带有 `QMutexLocker` 的 `with` 似乎是最干净、最清晰的方法。

`processFiles()` 方法相当长，因此我们将分三部分来回顾它。

```python
def processFiles(self, path):
    def unichrFromEntity(match):
        text = match.group(match.lastindex)
        if text.isdigit():
            return unichr(int(text))
        u = htmlentitydefs.name2codepoint.get(text)
        return unichr(u) if u is not None else ""
```

我们从嵌套函数定义开始。它与实体正则表达式（在第 552 页显示）配合使用。该表达式有两个匹配组，但在任何时刻只能有一个匹配。给定由正则表达式匹配到的匹配对象，该函数获取最后一个（也就是唯一的）匹配组，如果它全是数字，则返回对应码点的 Unicode 字符。否则，该函数返回与实体名称匹配的 Unicode 字符，如果该名称不在 `html entitydefs.name2codepoint` 字典中，则返回空字符串。

```python
for root, dirs, files in os.walk(path):
    if self.isStopped():
        return
    for name in [name for name in files \
                 if name.endswith((".htm", ".html"))]:
        fname = os.path.join(root, name)
        if self.isStopped():
            return

        words = set()
        fh = None
        try:
            fh = codecs.open(fname, "r", "UTF8", "ignore")
            text = fh.read()
        except (IOError, OSError), e:
            sys.stderr.write("Error: %s\n" % e)
            continue
        finally:
            if fh is not None:
                fh.close()
            if self.isStopped():
                return

        text = self.STRIPHTML_RE.sub("", text)
        text = self.ENTITY_RE.sub(unicodeFromEntity, text)
        text = text.lower()
```

`os.walk()` 方法从给定的路径开始递归遍历目录树。对于找到的每个目录，它返回一个三元组，包含根路径、子目录列表以及该目录中的文件列表。

我们遍历每个目录中带有 `.htm` 或 `.html` 后缀的文件。`unicode.endswith()` 和 `str.endswith()` 方法接受单个字符串或一个字符串元组作为匹配参数。对于每个匹配的文件，我们创建包含完整路径的文件名，并创建一个本地空集合，其中将包含在该文件中找到的唯一单词。

我们本应检查 HTML 文件使用的编码，但我们只是假设它们是 UTF-8 Unicode 或 ASCII（它是 UTF-8 的一个严格子集）。我们还传递了一个额外参数来指示应如何处理解码错误（即，它们应被忽略）。

一旦我们读取了文件的文本（作为一个大的字符串），我们剥离其 HTML 标签，将任何实体转换为它们的 Unicode 等效项，并将文本转换为小写

