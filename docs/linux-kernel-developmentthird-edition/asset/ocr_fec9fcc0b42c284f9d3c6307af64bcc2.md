* **FIXME:** We assume `dog == cat` which may not be true in the future
*/

The kernel has a facility for self-generating documentation. It is based on GNOME-doc, but slightly modified and renamed Kernel-doc. To create the standalone documentation in HTML format, run

```
make htmldocs
```

Or for postscript

```
make psdocs
```

You can use the system to document your functions by following a special format for your comments:

```
/**
 * find_treasure - find 'X marks the spot'
 * @map - treasure map
 * @time - time the treasure was hidden
 *
 * Must call while holding the pirate_ship_lock.
 */
void find_treasure(int map, struct timeval *time)
{
 /* ... */
}
```

For more information, see Documentation/kernel-doc-nano-HOWTO.txt.

# Typeofs

The Linux kernel developer community employs a strong dislike of the `typeofs` operator. Their rationale is

+   • `typeofs` hides the real type of data structures.
+   • Because the type is hidden, code is more prone to do bad things, such as pass a structure by value on the stack.
+   • `typeofs` is just being lazy.

Therefore, to avoid ridicule, avoid `typeofs`.

Of course, there are a few good uses of `typeofs`: hiding an architecture-specific implementation of a variable or providing forward compatibility when a type may change. Decide carefully whether the `typeofs` is truly needed or exists just to reduce the number of characters you need to type.