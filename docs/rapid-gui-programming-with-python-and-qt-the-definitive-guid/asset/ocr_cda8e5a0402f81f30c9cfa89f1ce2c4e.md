When using **PyQt** we have access to an additional string type, **QString**. Unlike Python’s **str** and **unicode**, **QString** is mutable; this means that we can change **QStrings** in place, inserting and removing substrings, and changing individual characters. **QString** has a rather different API from that provided by **str** and **unicode**. Qt provides **QString** because **Qt** is written in C++, which does not yet have built-in Unicode support.

**QString** holds Unicode characters, but depending on which version of Python we are using, the internal representation may be different from Python’s Unicode representation; this doesn’t really matter, since **PyQt** can easily convert between **unicode** and **QString**. For example:

```
>>> from PyQt4.QtCore import *
>>> a = QString("apple")
>>> b = unicode("baker")
>>> print a + b
applebaker
>>> type(a + b)
<class 'PyQt4.QtCore.QString'>
```

Here we import all the classes from the **QtCore** module, made available to us through the **PyQt4** module. When we perform operations involving **QStrings** and Python strings, the resultant strings are always **QStrings** as the **type()** function reveals.

When using **PyQt**, **Qt** methods that take string arguments can be given **str**, **unicode**, or **QString** types, and **PyQt** will perform any necessary conversion automatically. **Qt** methods that return strings always return **QStrings**. In view of Python’s dynamic typing, we can easily become confused and not be sure whether we have a **QString** or a **Python** string. For this reason, it is wise to decide on a policy for string usage so that we always know where we stand.

The policy we use with **PyQt** is as follows:

+   - Use type **str** only when working with strictly 7-bit **ASCII** strings or with raw 8-bit data, that is, with raw bytes.
+   - For strings that will be used only by **PyQt** functions, for example, strings that are returned by one **PyQt** function only to be passed at some point to another **PyQt** function—do not convert such strings. Simply keep them as **QStrings**.
+   - In all other cases, use **unicode** strings, converting **QStrings** to **unicode** as soon as possible. In other words, as soon as a **QString** has been returned from a **Qt** function, always immediately convert it to type **unicode**.

This policy means that we avoid making incorrect assumptions about 8-bit string encodings (because we use **Unicode**). It also ensures that the strings we pass to **Python** functions have the methods that **Python** expects; **QStrings** have different methods from **str** and **unicode**, so passing them to **Python** functions