
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

Whenever the walker thread finishes indexing a file, it emits an `indexed()` signal with the filename; this signal is connected to the `form_indexed()` method shown earlier. We update the status label to show the name of the file that has just been indexed, and every 25 files we also update the file count, words indexed, and common words LCD widgets. We use a read lock to ensure that the shared data structures are safe to read from, and we do the minimum amount of work inside the context of the lock, updating the LCD widgets only after the lock has been released.

For every 10th file processed we update the common words list widget. Again we use a read lock, and we use `copy()` to ensure that we do not refer to the shared data once the lock has been released.

```python
def finished(self, completed):
    self.statusLabel.setText("Indexing complete" \
        if completed else "Stopped")
    self.finishedIndexing()
```

When the thread has been stopped or has finished, it emits a `finished()` signal, connected to this method and passing a Boolean to indicate whether it completed. We update the status label and call our `finishedIndexing()` method to update the user interface.

```python
def finishedIndexing(self):
    self.walker.wait()
    self.filesIndexedLCD.display(self.fileCount)
    self.wordsIndexedLCD.display(len(self.filenamesForWords))
    self.commonWordsLCD.display(len(self.commonWords))
    self.pathButton.setEnabled(True)
```

When the indexing has finished we call `QThread.wait()` to make sure that the thread's `run()` method has finished. Then we update the user interface based on the current values of the shared data structures. We don't need to protect access to the dictionary or the set because the walker thread is not running.

## Using a Context Manager for Unlocking

In this chapter, we use `try ... finally` blocks to ensure that locks are unlocked after use. Python 2.6 offers an alternative approach using the new `with` keyword, in conjunction with a context manager. Context managers are explained in [PEP 343](http://www.python.org/dev/peps/pep-0343); suffice it to say that we can make a context manager by creating a class that has two special methods: `__enter__()` and `__exit__()`. Then, instead of writing code like this:

```python
try:
    self.lock.lockForRead()
    found = word in self.commonWords
finally:
    self.lock.unlock()
```

we can write something much simpler and shorter:

```python
with ReadLocker(self.lock):
    found = word in self.commonWords
```

This works because the semantics of the object given to the `with` statement (at its simplest) are:

```python
ContextManager.__enter__()
try:
    # statements, e.g., found = word in self.commonWords
finally:
    ContextManager.__exit__()
```

The `ReadLocker` context manager class itself is also easy to implement, assuming it is passed a `QReadWriteLock` object:

```python
class ReadLocker:
    def __init__(self, lock):
        self.lock = lock

    def __enter__(self):
        self.lock.lockForRead()

    def __exit__(self, type, value, tb):
        self.lock.unlock()
```

In fact, since PyQt 4.1, `QReadLocker` and `QWriteLocker` can be used as context managers, so with Python 2.6 (or Python 2.5 with `from __future__ import with statement`), we don't need to use `try ... finally` to guarantee unlocking, and can instead write code like this:

```python
with QReadLocker(self.lock):
    found = word in self.commonWords
```

The files `pageindexer_26.py` and `walker_26.py` in `chap19` use this approach.

At any time during the indexing, the user can interact with the user interface with no freezing or performance degradation. In particular, they can enter text in the find line edit and press Enter to populate the files list widget with those files that contain the word they typed. If they press Enter more than once with a bit of time between presses, the list of files may change, because in the interval more files may have been indexed. The `find()` method is slightly long, so we will review it in two parts.

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

If the user enters a word to find, we clear the status label and the file list widget and look for the word in the set of common words. If the word was found, it is too common to be indexed, so we just give an informative message and return.

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

If the user's word is not in the set of common words, it might be in the index. We access the `filenamesForWords` default dictionary using a read lock, and copy the set of files that match the word. The set will be empty if no files have the word, but in either case, the set we have is a copy, so there is no risk of accessing shared data outside the context of a lock. If there are matching files we add them to the files list widget, sorted and using platform-native path separators.

The `sorted()` function returns its first argument (e.g., a list or set), in sorted order. It can be given a comparison function as the second argument, but here we have specified a "key". This has the effect of doing a DSU (decorate, sort, undecorate) sort that is the equivalent of:

```python
templist = [(fname.lower(), fname) for fname in files]
templist.sort()

files = [fname for key, fname in templist]
```

This is more efficient than using a comparison function because each item is lowercased just once rather than every time it is used in a comparison.

```python
def reject(self):
    if self.walker.isRunning():
        self.walker.stop()
        self.finishedIndexing()
    else:
        self.accept()
```

If the user presses Esc, the `reject()` method is called. If indexing is in progress, we call `stop()` on the thread and then call `finishedIndexing()`; the `finishedIndexing()` method calls `wait()`. Otherwise, indexing has either been stopped by a previous Esc key press or has finished; either way, we call `accept()` to terminate the application.

```python
def closeEvent(self, event=None):
    self.walker.stop()
    self.walker.wait()
```

When the application is terminated, either by the `accept()` call that occurs in the `reject()` method, or by other means, such as the user clicking the close X button, the close event is called. Here we make sure that indexing has been stopped and that the thread has finished so that a clean termination takes place.

All the indexing work has been done by the walker secondary thread. This thread has been controlled by the primary thread calling its methods (e.g., `start()` and `stop()`), and has notified the primary thread of its status (file indexed, indexing finished) through PyQt's signals and slots mechanism. The shared data has been accessed—for example, when the user has asked which files contain a particular word, or when the data has been updated by the walk-
