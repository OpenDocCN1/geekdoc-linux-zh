
Conversely, mutable objects, that is, parameters that are object references to mutable types like lists and dictionaries, can be changed inside functions. These parameter-passing behaviors are the same as in Java.\*

All Python functions return a value. This is done either explicitly by using a return or yield statement (covered next), or implicitly, in which case Python will return None for us. Unlike C++ or Java, we are not tied down to specifying one particular return type: We can return any type we want since what we return is an object reference that is bound to a variable of any type. Python functions always return a single value, but because that value can be a tuple or a list or any other collection, for all practical purposes, Python functions can return any number of values.

## Generator Functions

If we replace the code at the end of the frange() function as shown in the following code snippet, we will turn the function into a generator. Generators do not have return statements; instead, they have yield statements. If a generator runs out of values, that is, if control reaches the end of the function, instead of returning, Python automatically raises a StopIteration exception:

```python
# Build and return a list
result = []
while start < (stop - (inc / 2.0)):
    result.append(start)
    start += inc
return result

# Return each value on demand
while start < (stop - (inc / 2.0)):
    yield start
    start += inc
```

Now, if we call frange(5), we will get back a generator object, not a list. We can force the generator to give us a list by doing this: `list(frange(5))`. But a more common use of generators is in loops:

```python
for x in frange(10): 
    print x,
```

This will output "0.1.0.2.0.3.0.4.0.5.0.6.0.7.0.8.0.9.0" whichever version we use. But for long lists the generator version will be much more efficient, because rather than creating the whole list in memory like the list version, it creates only one item at a time.

The yield statement behaves like a return statement, but for one crucial difference: After yield has returned a value, when the generator is next called it will continue from the statement following the yield with all its previous state intact. So the first time the frange() generator is called, assuming, say frange(5), it returns 0.0; the second time it returns 1.0, and so on. After returning 9.0 the while expression evaluates to False and the function terminates.

> \*Mutable parameters in Python are similar to Pascal's var parameters and to C++'s non-const references.

Because the function is a generator (and this is the case purely because we have used `yield`), when it finishes it does not return a value, but instead raises a `StopIteration` exception. In the context of a `for` loop, the `for` gracefully handles this particular exception, taking it not as an error, but as an indication that the iteration has completed, so the `for` loop ends and the flow of control moves to the `for` loop’s `else` suite, or to the statement following the `for` loop’s suite, if there is no `else`. Similarly, if we coerce a generator into a list, the list constructor will automatically handle the `StopIteration` exception.

A generator is an object that has a `next()` function, so we can explore the behavior of our `frange()` generator interactively if we wish:

```python
>>> list(frange(1, 3, 0.75))
[1, 1.75, 2.5]
>>> gen = frange(1, 3, 0.75)
>>> gen.next()
1
>>> gen.next()
1.75
>>> gen.next()
2.5
>>> gen.next()
Traceback (most recent call last):
File <pyshell#126>, line 1, in <toplevel>
  gen.next()
StopIteration
```

We generated the whole three-item list using `list()`, and then we used the generator returned by `frange()` to produce each successive value in the same way that a `for` loop does.

## Using Keyword Arguments

Python’s argument-handling abilities are very versatile. So far we have provided parameters using positional syntax. For example, the first parameter we gave to our `frange()` function always went to `arg0`, the second to `arg1`, and the third to `arg2`. We have also used default arguments so that some arguments could be omitted. But what happens if we want to pass, say, the first and third arguments, but accept the default second argument? In the next example, we will see how we can achieve this.

Python provides a `strip()` method for stripping whitespace (or other unwanted characters) from the ends of a string, but it does not provide a function for cleaning up the whitespace inside a string; something that we often need to do when we get strings from users. Here is a function that strips whitespace from both ends of a string and replaces each sequence of internal whitespace with a single space:

## Experimenting with Functions in Files

Both frange() and a generator version, gfrange(), are in the file chap02/frange.py. If we want to try these or any other functions interactively, we can start up IDLE, and append the path where the file we want to use is located to the paths it searches; for example:

```python
>>> import sys
>>> sys.path.append("C:/pyqt/chap02")
```

Now the relevant module can be loaded into IDLE:

```python
>>> import frange
```

The file we wish to import from must have a .py extension, and we must not include the extension in the import statement. Now we can use frange() and gfrange() inside IDLE:

```python
>>> frange.frange(3, 5, 0.25)
[3, 3.25, 3.5, 3.75, 4.0, 4.25, 4.5, 4.75]
```

The first name frange is the module name, and within that module we wish to access the frange function, which is why we write frange.frange(). We did the same thing a moment ago, when we imported the sys module and accessed its path list using sys.path.

Although we prefer to use IDLE, it is also possible to directly use the Python interpreter when experimenting interactively. If we simply run the Python executable itself (python.exe, for example) in a console, we will get the familiar >>> prompt and be able to use the interpreter interactively.

```python
def simplify(text, space="\t\r\n\f", delete=""):
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

The function iterates over every character in the text string. If the character is in the delete string (which, by default, is empty), we ignore it. If it is a “space” (i.e., it is in the space string), we append the word we have been building up to our list of words, and set the next word to be empty. Otherwise, we append the character to the word we are building up. At the end, we tack on the last word to our list of words. Finally, we return the list of words as a single string with each word separated by a single space, using the string `join()` method.*

Now let us look at how we can use the function:

```python
simplify(" this   and\n that\t too")    # Returns "this and that too"
simplify("  Washington   D.C.\n",
         delete=".;:. ")                # Returns "Washington DC"
simplify(delete="aeiou", text="  disemvoweled ")    # Returns "dsmwvwld"
```

In the first case, we use the default arguments for the space and delete parameters. In the second case, we use Python’s keyword argument syntax to specify the third parameter while accepting the default for the second parameter. In the last case, we use keyword syntax for both of the arguments we want to use. Notice that if we use keyword syntax, the order of the keyword arguments is up to us—providing that if we also use positional arguments, these precede the keyword arguments, as the second call shows.

The code we have used for `simplify()` is not as Pythonic as it could be. For example, we should really store word as a list of characters rather than as a string, and we don’t need the space parameter since we could use the string object’s `isspace()` method instead. The file chap02/simplified.py contains the `simplify()` shown here and a similar function, `simplified()`, which uses the more Pythonic approach. And as noted earlier, although we usually don’t show the docstrings in the book, they are in the files.

Python’s argument passing is even more sophisticated than we have shown so far. In addition to named arguments, Python functions can be given signatures that accept a variable number of positional arguments and a variable number of keyword arguments. This is a much more versatile and powerful version of C++’s and Java’s variable argument lists, but it is rarely needed, so we will not cover it.

## Lambda Functions

So far, we’ve always defined functions using `def`, but Python provides a second way of creating functions:

```python
cube = lambda x: pow(x, 3)
```

The lambda keyword is used to create simple anonymous functions. Lambda functions cannot contain control structures (no branches or loops), nor do they have a `return` statement: The value returned is simply whatever the expression

![](img/9bfe0a027fcc8793bb087287001100dd_75_0.png)
