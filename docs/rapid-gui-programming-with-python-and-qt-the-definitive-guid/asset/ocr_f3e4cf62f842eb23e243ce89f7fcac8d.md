```
finally:
self.lock.unlock()
self.wordsIndexedLCD.display(indexedWordCount)
self.commonWordsLCD.display(commonWordCount)
elif self.fileCount % 10i == 0:
self.commonWordsListWidget.clear()
try:
self.lock.lockForRead()
words = self.commonWords.copy()
finally:
self.lock.unlock()
self.commonWordsListWidget.addItems(sorted(words))
```

Whenever the walker thread finishes indexing a file, it emits an indexed() signal with the filename; this signal is connected to the form_indexed() method shown earlier. We update the status label to show the name of the file that has just been indexed, and every 25 files we also update the file count, words indexed, and common words LCD widgets. We use a read lock to ensure that the shared data structures are safe to read from, and we do the minimum amount of work inside the context of the lock, updating the LCD widgets only after the lock has been released.

For every 101st file processed we update the common words list widget. Again we use a read lock, and we use set_copy() to ensure that we do not refer to the shared data once the lock has been released.

```
def finished(self, completed):
self.statusLabel.setText("Indexing complete" \
if completed else "Stopped")
self.finishedIndexing()
```

When the thread has been stopped or has finished, it emits a finished() signal, connected to this method and passing a Boolean to indicate whether it completed. We update the status label and call our finishedIndexing() method to update the user interface.

```
def finishedIndexing(self):
self.walker.wait()
self.filesIndexedLCD.display(self.fileCount)
self.wordsIndexedLCD.display(len(self.filenamesForWords))
self.commonWordsLCD.display(len(self.commonWords))
self.pathButton.setEnabled(True)
```

When the indexing has finished we call QThread.wait() to make sure that the thread's run() method has finished. Then we update the user interface based on the current values of the shared data structures. We don't need to protect access to the dictionary or the set because the walker thread is not running.