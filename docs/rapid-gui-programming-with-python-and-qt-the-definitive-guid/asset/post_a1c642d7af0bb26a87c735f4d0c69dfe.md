
We create a list called `__keys` and a dictionary called `__dict`. If the `OrderedDict` is initialized with another dictionary, we need to get that dictionary’s data. The simplest and most direct way of doing this is how we do it in the `else` suite. We convert the object to a dictionary (which costs nothing if it is already a dictionary), and take a shallow copy of it. Then you take a sorted list of the dictionary’s keys.

The approach used in the `else` suite works in all cases, but purely for efficiency, we have introduced a type test using `isinstance()`. This function returns `True` if its first argument is an instance of the class or classes (passed as a tuple) given as its second argument, or any of their base classes. So if we are initializing from another `OrderedDict` (or from an `OrderedDict` subclass) we can simply shallow-copy its dictionary, which costs the same as before, and shallow-copy its keys, which is cheaper because they are already sorted.

Since our dictionary is ordered, in addition to the normal dictionary methods we should also be able to access the value of a dictionary item at a particular index position in the dictionary. That is what the first two methods we are going to implement provide:

```python
def getAt(self, index):
    return self.__dict[self._keys[index]]

def setAt(self, index, value):
    self.__dict[self._keys[index]] = value
```

The `getAt()` method returns the *index* th item in the dictionary. It does this by accessing the dictionary using the key the list holds in the *index* th position. The `setAt()` method uses the same logic, except that it sets the value for the dictionary item that is at the *index* th position.

```python
def __getitem__(self, key):
    return self.__dict[key]
```

If we have a dictionary, `d`, and use the syntax `value = d[key]`, the `__getitem__()` special method is called. We simply pass the work on to the dictionary we are holding inside our `OrderedDict` class. If the key is not in `__dict` it will raise a `KeyError`, which is what we want, since we want `OrderedDict` to have the same behavior as a `dict`, except when key order is an issue.

```python
def __setitem__(self, key, value):
    if key not in self.__dict:
        bisect.insort_left(self._keys, key)
    self.__dict[key] = value
```

![](img/9bfe0a027fcc8793bb087287001100dd_108_0.png)

If the user assigns to a dictionary using the syntax `d[key] = value`, we again rely on the `__dict` to do the work. But if the key is not already in the `__dict`, it can't be in the list of keys either, so we must add it.

The `insort_left()` function takes a sorted sequence, such as a sorted list, and an item to insert. It locates the position in the sequence where the item should go to preserve the sequence's order, and inserts the item there. The `insort_left()` function, like all the bisect module's functions, uses a binary chop, so performance is excellent even on very long sequences.

Another approach would have been to simply append the new key and then call `sort()` on the list. Python's sorting functionality is highly optimized for partially sorted data, so performance might not be too bad, but we prefer the more efficient solution.

```python
def __delitem__(self, key):
    i = bisect.bisect_left(self._keys, key)
    del self._keys[i]
    del self._dict[key]
```

Deleting an item is quite simple. The `bisect_left()` function takes a sorted sequence, such as a sorted list, and an item. It returns the index position where the item is in the sequence (or where the item would have been if it was in the sequence). We assume the key is in the list, relying on an exception being raised if it isn't. We delete the key by index position from the keys list, and delete the (key, value) by key from the dictionary.

We could instead have deleted the key from the keys list with a single statement, `self._keys.remove(key)`, but that would have used a slow linear search.

```python
def get(self, key, value=None):
    return self._dict.get(key, value)
```

This method returns the value for the given key, unless the key is not present in the dictionary, in which case it returns the specified value (which defaults to `None`). Since key order is not involved, we can simply pass on the work.

```python
def setdefault(self, key, value):
    if key not in self._dict:
        bisect.insort_left(self._keys, key)
    return self._dict.setdefault(key, value)
```

This method is similar to `get()`, but with one important difference: If the key is not in the dictionary, it is inserted with the given value. And in the case of a key that isn't in the dictionary, we must, of course, insert it into our key list.

```python
def pop(self, key, value=None):
    if key not in self._dict:
        return value
    i = bisect.bisect_left(self._keys, key)
    del self._keys[i]
    return self._dict.pop(key, value)
```

This method is also similar to `get()`, except that it removes the item with the given key if it is in the dictionary. Naturally, if a key is removed from the dictionary, we must also remove it from the list of keys.

```python
def popitem(self):
    item = self._dict.popitem()
    i = bisect.bisect_left(self._keys, item[0])
    del self._keys[i]
    return item
```

This method removes and returns an arbitrary item, that is, a (key, value) tuple. We first remove the arbitrary item from the dictionary (since we don't know what it will be in advance), then remove its key from our list of keys, and finally return the item that was removed.

```python
def has_key(self, key):
    return key in self._dict

def __contains__(self, key):
    return key in self._dict
```

The `has_key()` method is supported for backward compatibility; nowadays programmers use `in`, which is implemented by the `__contains__()` special method.

```python
def __len__(self):
    return len(self._dict)
```

This returns how many items are in the dictionary. We could just as easily have returned `len(self._keys)`.

```python
def keys(self):
    return self._keys[:]
```

We return our dictionary's keys as a shallow copy of our key list, so they are in key order. A standard `dict` returns its keys in an arbitrary order.

```python
def values(self):
    return [self._dict[key] for key in self._keys]
```

We return the dictionary's values in key order. To do this we create a list of the values by iterating over the key list in a list comprehension. This could also be done using a for loop:

```python
result = []
for key in self._keys:
    result.append(self._dict[key])
return result
```

Writing one line of code rather than four obviously makes the list comprehension more appealing, although the syntax can take some getting used to.

```python
def items(self):
    return [(key, self._dict[key]) for key in self._keys]
```

We use a similar approach for returning items, as (key, value) tuples, and again we could use a conventional loop instead:

```python
result = []
for key in self._keys:
    result.append((key, self._dict[key]))
return result
```

By now, though, list comprehensions should start to become more familiar.

```python
def __iter__(self):
    return iter(self._keys)

def iterkeys(self):
    return iter(self._keys)
```

An iterator is a “callable object” (typically a function or method) that returns the “next” item each time it is called. (Such objects have a `next()` function which is what Python calls.)

An iterator for a sequence such as a string, list, or tuple, can be obtained by using the `iter()` function, which is what we do here. For dictionaries, when an iterator is requested, an iterator to the dictionary’s keys is returned, although for consistency, the `dict` API also provides an `iterkeys()` method, since it also provides `itervalues()` and `iteritems()` methods. If `iter()` is called on a dictionary, such as an `OrderedDict` instance, Python uses the `__iter__()` special method.

```python
def itervalues(self):
    for key in self._keys:
        yield self._dict[key]
```

If `itervalues()` is called, we must return a generator that returns the dictionary’s values. For a plain `dict`, the generator returns each value in an arbitrary order, but for the `OrderedDict` we want to return the values in key order.

Any function or method that contains a `yield` statement is a generator. The `yield` statement behaves like a `return` statement, except that after the `yield` has returned a value, when the generator is next called it will continue from the statement following the `yield` with all its previous state intact. So in this method, after each dictionary value is returned, the next iteration of the `for` loop takes place, until all the values have been returned.

```python
def iteritems(self):
    for key in self._keys:
        yield key, self._dict[key]
```
