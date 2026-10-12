The CD-ROM contains this code plus an example (bare-bones) e-mail client and SMTP class. (Don’t get rid of your e-mail client yet—these classes are the absolute minimal functionality required.)

# COLLECTIONS, ARRAYS, AND LINKED-LISTS

The Qt toolkit provides some very flexible classes for maintaining collections, arrays, and linked lists of objects. These classes comprise nearly half the overall value of the toolkit in my opinion. You will have to exercise a bit of caution when selecting a specific class, as Troll often provides two flavors of a given class; one that operates on values and another that operates on references to values. Unlike most other Qt classes, the naming conventions are not always a good clue as to which classes are value- or reference-based. I have tried to make it a little more obvious in the descriptions that follow.

# QArray

QArray is a value-based template class that can maintain arrays of simple objects, where "simple" means that there is no constructor, destructor, or virtual functions.

# A Possible Instantiation

```
```
...
QArray<int> nums(10);
...
```
```

# Example Use

```
```
...
QArray<int> so(100);
for(int a=0;a<100;a++) so[a] = a;
...
```
```

QArray uses bit-level copy and compare operations. See the QVector class for reference-based implementations of an array.

# QAsciiCache

QAsciiCache is a template class that provides caching functionality based on character pointer keys. Keys are stored in least-recently used order. Note that this class is not appropriate for Unicode cache implementations. QCache provides a QString-based caching mechanism with full Unicode support, and since there is no performance difference between the two, QAsciiCache is only useful for legacy coding purposes.

# QAsciiCacheIterator

This class provides an iterator for QAsciiCache objects.