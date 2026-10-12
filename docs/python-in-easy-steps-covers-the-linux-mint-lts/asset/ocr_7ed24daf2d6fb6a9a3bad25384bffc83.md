# Producing generators

When a Python function is called, it executes the statements it contains and may return any value specified to the **return** keyword. After the function ends, control returns to the caller and the state of the function is not retained. When the function is next called, it will process its statements from start to finish once more.

A Python generator, on the other hand, is a special function that returns a “generator object” to the caller rather than a data value. This, effectively, retains the state of the function when it was last called, so it will continue from that point when next called.

Generator functions are produced by definition just like regular functions, but contain a “yield” statement. This begins with the Python **yield** keyword and specifies the generator object to be returned to the caller. When the **yield** statement gets executed, the state of the generator object is frozen, and the current value in its “expression list” is retained. The generator object returned by the **yield** statement can be conveniently assigned to a variable. Python’s built-in **next()** function can then specify that variable name within its parentheses to continue execution of the function from the point at which it was frozen – exactly as if the yield statement were just another external call.

Repeatedly calling the generator object with the **next()** function continues execution of the function until it raises an exception. This can be avoided by enclosing the **yield** statement within an infinite loop so it will return successive values on each iteration. For example, to yield an incremented value on each call:

```
```python
def incrementer():
    i = 1
    while True:
        yield i
        i += 1

inc = incrementer()
print(next(inc))
print(next(inc))
print(next(inc))
```
```