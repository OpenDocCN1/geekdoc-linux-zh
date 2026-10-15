3. Give the exact Python code that would allow you to step through the invocation of the three functions from Example 16.16, to generate its output results until you reach StopIteration. List the output generated at each step through the recursion.

# 16.3.13 Coroutines

In the previous section, we introduced generator functions, which use yield to give output results. Python generator functions can also “consume” results using a yield statement. In addition, two new methods applied to generator objects, send() and close(), create a framework for objects that consume and give values. Generator functions that define these objects are called coroutines. Coroutines consume values using a yield statement on the right side of an expression, as follows.

```
value = (yield)
```

With this syntax, execution pauses at this statement until the object’s send method is invoked with an argument:

```
coroutine.send(data)
```

Then, execution resumes, with value being assigned to the value of data. To signal the end of a computation, we shut down a coroutine using the close() method. This raises a GeneratorExit exception inside the coroutine, which we can catch with a try/except clause.

The next example illustrates these concepts. It is a coroutine that prints strings that match a provided template pattern:

# Example 16.17

```
>>>def grepper(template):
...     print ('Searching for ' + template)
...     try:
...         while True:
...             x = (yield)
...             if template in x:
...                 print x
...     except GeneratorExit:
...         print "Done"
...
>>> q = grepper("Pythonista")
>>> q.next()
Pythonista
>>> q.send("After doing this section, you will be known as a Pythonista")
After doing this section, you will be known as a Pythonista
>>> q.send("Not a very Pythonic answer")
```