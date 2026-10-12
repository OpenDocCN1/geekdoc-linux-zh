# Table 1.6 *Selected Set Methods and Functions*

| Syntax | Description |
|---|---|
| `x in s` | Returns True if item *x* is in set *s* |
| `x not in s` | Returns True if item *x* is not in set *s* |
| `len(s)` | Returns the number of items in set *s* |
| `s.clear()` | Removes all the items from set *s* |
| `s.copy()` | Returns a shallow copy of set *s* |
| `s.add(x)` | Adds item *x* to set *s* if it is not already in *s* |
| `s.remove(x)` | Removes item *x* from set *s*, or raises a `KeyError` exception if *x* is not in *s* |
| `s.discard(x)` | Removes item *x* from set *s* if it is in *s* |
| `s.issubset(t)` or `s <= t` | Returns True if set *s* is a subset of set *t* |
| `s.issuperset(t)` or `s >= t` | Returns True if set *s* is a superset of set *t* |
| `s.union(t)` or `s \| t` | Returns a new set that has all the items from set *s* and from set *t* |
| `s.intersection(t)` or `s & t` | Returns a new set that has each item that is both in set *s* and in set *t* |
| `s.difference(t)` or `s - t` | Returns a new set that has every item that is in set *s* that is not in set *t* |
| `s.symmetric_difference(t)` or `s ^ t` | Returns a new set that has items in either *s* or *t* but not in both |
| `s.issubset(t)` or `s <= t` | Returns True if set *s* is a subset of set *t* |
| `s.issuperset(t)` or `s >= t` | Returns True if set *s* is a superset of set *t* |

# Table 1.7 *Selected Sequence-Related Built-ins*

| Syntax | Description |
|---|---|
| `all(q)` | Returns True if all items in *q* are True; *q* is an *iterable*—for example, a sequence such as a string or a list | Python 2.5 |
| `any(q)` | Returns True if any item in *q* is True | Python 2.5 |
| `x in q` | Returns True if item *x* is in sequence *q*; also works for dictionaries |
| `x not in q` | Returns True if item *x* is not in sequence *q*; also works for dictionaries |
| `len(q)` | Returns the number of items in sequence *q*; also works for dictionaries |
| `max(q)` | Returns the maximum item of sequence *q* |
| `min(q)` | Returns the minimum item of sequence *q* |
| `sum(q)` | Returns the sum of the items in sequence *q* |