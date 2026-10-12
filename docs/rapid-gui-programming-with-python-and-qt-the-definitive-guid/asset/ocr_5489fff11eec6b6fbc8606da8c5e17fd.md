```
```text
copy_reg.pickle(QDate, _pickleQDate)
copy_reg.pickle(QString, _pickleQString)
```
```

The copy_reg module is used to specify how to read and write nonstandard data types. The information is provided by calling copy_reg.pickle() with two arguments. The first argument is the new-style class that we want to be able to pickle, and the second is a function. The function must take a single argument, an instance of the class we want to pickle, and should return a two-tuple, whose first element is the class and whose second element is a tuple of standard Python types that can be fed into the class's constructor to create an instance that has the same value as the instance passed in.

With this information the pickle module can store instances of our class by storing the class name as text and the arguments as a tuple of standard Python types. Then, when we want to unpickle (load) the data back, Python can use eval() to re-create our instances.

PyQt 4.3 includes support for pickling basic Qt data types, including QByteArray, QChar, QColor, QDate, QDateTime, QKeySequence, QLine, QLineF, QMatrix, QPoint, QPointF, QPolygon, QRect, QRectf, QSize, QSizeF, QString, QTime, and all PyQt enums. This means that we can “pickle” any of these types without having to write and register our own pickling functions.

```
```python
def savePickle(self):
    error = None
    fh = None
    try:
        fh = gzip.open(unicode(self.__fname), "wb")
        cPickle.dump(self.__movies, fh, 2)
    except (IOError, OSError), e:
        error = "Failed to save: %s" % e
    finally:
        if fh is not None:
            fh.close()
        if error is not None:
            return False, error
        self.__dirty = False
        return True, "Saved %d movie records to %s" % (
            len(self.__movies),
            QFileInfo(self.__fname).fileName())
```
```

We can easily save any Python data structure, including recursive data structures, as a pickle. We do this by opening a file in binary mode and using the dump() function. In this example, we have chosen to save our pickle compressed (which may reduce file size by around 50 percent), but we could have avoided using compression like this:

```
```python
fh = open(unicode(self.__fname), "wb")
```
```