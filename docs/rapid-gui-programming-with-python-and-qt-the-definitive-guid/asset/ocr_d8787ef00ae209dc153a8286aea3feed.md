# ## Experimenting with Functions in Files

Both frange() and a generator version, gfrange(), are in the file chap02/frange.py. If we want to try these or any other functions interactively, we can start up IDLE, and append the path where the file we want to use is located to the paths it searches; for example:

```
```python
>>> import sys
>>> sys.path.append("C:/pyqt/chap02")
```
```

Now the relevant module can be loaded into IDLE:

```
```python
>>> import frange
```
```

The file we wish to import from must have a .py extension, and we must not include the extension in the import statement. Now we can use frange() and gfrange() inside IDLE:

```
```python
>>> frange.frange(3, 5, 0.25)
[3, 3.25, 3.5, 3.75, 4.0, 4.25, 4.5, 4.75]
```
```

The first name frange is the module name, and within that module we wish to access the frange function, which is why we write frange.frange(). We did the same thing a moment ago, when we imported the sys module and accessed its path list using sys.path.

Although we prefer to use IDLE, it is also possible to directly use the Python interpreter when experimenting interactively. If we simply run the Python executable itself (python.exe, for example) in a console, we will get the familiar >>> prompt and be able to use the interpreter interactively.

```
```python
def simplify(text, space="\\t\\r\\n\\f", delete=""):
    result = []
    word = ""
    for char in text:
        if char in delete:
            continue
        elif char in space:
            if word:
                result.append(word)
                word = ""
        else:
            word += char
    if word:
        result.append(word)
    return " ".join(result)
```
```