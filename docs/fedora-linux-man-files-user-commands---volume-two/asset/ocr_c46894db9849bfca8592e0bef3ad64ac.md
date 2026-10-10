# ## BUGS

The todo list presented by `—preserve-merges` `—interactive` does not represent the topology of the revision graph. Editing commits and rewording their commit messages should work fine, but attempts to reorder commits tend to produce counterintuitive results.
For example, an attempt to rearrange

```
```
1 --- 2 --- 3 --- 4 --- 5
```
```

to

```
```
1 --- 2 --- 4 --- 3 --- 5
```
```

by moving the “pick 4” line will result in the following history:

```
```
3 / 1 --- 2 --- 4 --- 5
```
```