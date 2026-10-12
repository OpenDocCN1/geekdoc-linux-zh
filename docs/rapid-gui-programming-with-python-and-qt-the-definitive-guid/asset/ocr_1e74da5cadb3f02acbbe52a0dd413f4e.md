seems to be no reason not to show it here. The class statement has a similar structure to a def statement, with the class keyword, followed by the name, except that in the parentheses we put the base classes rather than parameter names. We've used pass to indicate an empty suite, and we have chosen to inherit Exception. We could have inherited from one of Exception's subclasses instead; for example, ValueError.

In practice, though, raising an exception in this particular case may be overkill. We could take the view that the function will always be called with space or delete or both nonempty, and we can assert this belief rather than use an exception:

```
```
def simplify(text, space="\t\r\n\f", delete=""):
    assert space or delete
```
```

This will raise an AssertionError exception if both space and delete are empty, and probably expresses the logic of the function's preconditions better than the previous two attempts. If the exception is not caught (and an assertion should not be), the program will terminate and issue an error message saying that an AssertionError was the cause and providing a traceback that identifies the file and line where the assertion failed.

Another context where exception handling can be useful is breaking out of deeply nested loops. For example, imagine that we have a three-dimensional grid of values and we want to find the first occurrence of a particular target item. Here is the conventional approach:

```
```
found = False
for x in range(len(grid)):
    for y in range(len(grid[x])):
        for z in range(len(grid[x][y])):
            if grid[x][y][z] == target:
                found = True
                break

if found:
    break
if found:
    break
if found:
    print("Found at (%d, %d, %d)" % (x, y, z))
else:
    print("Not found")
```
```

This is 15 lines long. It is easy to understand, but tedious to type and rather inefficient. Now we will use an approach that uses exception handling:

```
```
class FoundException(Exception): pass

try:
```
```