
## 50 Python commands

### 26 Ranges

You may need a list of numbers, maybe in a *for* loop. The command 'range()' can create an iterable list of integers. With one parameter, it goes from 0 to the given number. You can provide an optional start number, as well as a step size. Negative numbers count down.

### 27 Xranges

One problem with ranges is that all of the elements need to be calculated up front and stored in memory. The command 'xrange()' takes the same parameters and provides the same result, but only calculates the next element as it is needed.

### 28 Iterators

Iteration is a very Pythonic way of doing things. For objects which are not intrinsically iterable, you can use the command 'iter(object_name)' to essentially wrap your object and provide an iterable interface for use with other functions and operators.

### 29 Sorted lists

You can use the command 'sorted(list)' to sort the elements of a list. You can give it a custom comparison function, and for more complex elements can include a key function that pulls out a ranking property from each element for comparison.

![](img/e016e192a91ffc1a9e474690a590742f_19_0.png)

### 30 Summing items

Above, we saw the general reduction function reduce. A specific type of reduction operation, summation, is common enough to warrant the inclusion of a special case, the command 'sum(iterable, object)'. You can include a second parameter here that will provide a starting value.

![](img/e016e192a91ffc1a9e474690a590742f_19_1.png)

### 31 With modules

The 'with' command provides the ability to wrap a code block with methods defined by a context manager. This can help clean up code and make it easier to read when a given piece of code is supposed to be doing months later. A classic example of using 'with' is when dealing with files. You could use something like 'with open("myfile.txt", "r")' as f'. This will open the file and prepare it for reading. You can then read the file in the code block with 'data=f.read()'. The best part of doing this is that the file will automatically be closed when the code block is exited, regardless of the reason. So, even if the code block throws an exception, you don't need to worry about closing the file as part of your exception handler. If you have a more complicated 'with', for example, you can create a context manager class to help out.

### 32 Printing

The most direct way of getting output to the user is with the print command. This will send text out to the console window. If you are using version 2.X of Python, there are a couple of ways you can use the print command. The most common way had been simply call it as 'print "Some text"'. You can also use print with the same syntax that you would use for any other function. So, the above example would look like 'print("Some text")'. This is the only form available in version 3.X. If you use the function syntax, you can add extra parameters that give you finer control over this output. For example, you can give the parameter 'file=myfile.txt' and get the output from the print command being dumped into the given text file. It also will accept any object that has some string representation available.

> “A classic example of using 'with' is when dealing with files. The best part of doing this is that the file will automatically be closed when the code block is exited, regardless of the reason”

![](img/e016e192a91ffc1a9e474690a590742f_19_2.png)

### 33 Memoryview

Sometimes, you need to access the raw data of some object, usually as a buffer of bytes. You can copy this data and put it into a bytearray, for example. But this means that you will be using extra memory, and this might not be an option for large objects. The command 'memoryview(object_name)' wraps the object handed in to the command and provides an interface to the raw bytes. It gives access to these bytes an element at a time. In many cases, elements are the size of one byte. But, depending on the object details, you could end up with elements that are larger than that. You can find out the size of an element in bytes with the property 'itemsize'. Once you have your memory view created, you can access the individual elements as you would get elements from a list (item_view[1], for example).

### 34 Files

When dealing with files, you need to create a file object to interact with it. The file command takes a string with the file name and location and creates a file object instance. You can then call the file object methods like `open`, `read` and `close`, to get data out of the file. If you are doing file processing, you can also use the `readline` method. When opening a file, there is an explicit `open()` command to simplify the process. It takes a string with the file name, and an optional parameter that is a string which defines the mode. The default is to open the file as read-only (`r`). You can also open it for writing (`w`) and appending (`a`). After opening the file, a file object is returned so that you can further interact with it. You can then read it, write to it, and finally close it.

![](img/e016e192a91ffc1a9e474690a590742f_20_0.png)

### 35 Yielding

In many cases, a function may need to **yield** the control of execution to some other function. This is the case with generators. The preferred method for a generator is that it will only calculate the next value when it is requested through the method `next()`. The command `yield` saves the current state of the generator function and return execution control to the calling function. In this way, the saved state of the generator is reloaded and the generator picks up where it left off in order to calculate the next requested value. In this way, you need not have enough memory available to store the bare minimum to calculate the next needed value, rather than having to store all of the possible values in memory all at once.

### 36 Weak references

You sometimes need to have a reference to an object, but still be able to destroy it if needed. A **weak reference** is one which can be ignored by the garbage collector. If the only references left to an object are weak references, then the garbage collector is allowed to destroy that object and reclaim the space for other uses. This is useful in cases where you have caches or mappings of large datasets that don’t necessarily need to stay in memory. If an object that is weakly referenced ends up being destroyed and you try to access it, it will appear as a `None`. You can test for this condition and then reload the data if you decide that this is a necessary step.

![](img/e016e192a91ffc1a9e474690a590742f_20_1.png)

![](img/e016e192a91ffc1a9e474690a590742f_20_2.png)

![](img/e016e192a91ffc1a9e474690a590742f_20_3.png)

### 37 Pickling data

There are a few different ways of serialising memory when you need to checkpoint results to disk. One of these is called pickling. Pickle is actually a complete module, not just a single command. To store data on to the hard drive, you can use the `dump` method to write the data out. When you want to reload the same data at some other point in the future, you can use the `load` method to read the data in and unpickle it. One issue with pickle is its speed, or lack of it. There is a second module, `cPickle`, that provides the same basic functionality. But, since it is written in C, it can be as much as 1000 times faster. One thing to be aware of is that pickle does not store any class information for an object, but only its instance information. This means that when you unpickle the object, it may have different methods and attributes if the class definition has changed in the interim.

### 38 Shelving data

While pickling allows you save data and reload it, sometimes you need more structured object permanence in your Python session. With the `shelve` module, you can create an object store where essentially anything that can be pickled can be stored there. The backend of the storage on the drive can be handled by one of several systems, such as `dbm` or `gdbm`. Once you have opened a shelf, you can read and write to it using key-value pairs. When you do one, you need to be sure to explicitly close the shelf so that it is synchronised with the file storage. Because of the way the data may be stored in a backing database, it is best to not open the relevant files outside of the `shelve` module in Python. You can also open the shelf with `writeback` set to `True`. If so, you can explicitly call the `sync` method to write out cached changes.

### 39 Threads

You can do multiple threads of execution within Python. The `thread` command can create a new thread of execution for you. It follows the same techniques as those for POSIX threads. When you first create a thread, you need to hand in a function name, along with whatever parameters said function needs. One thing to keep in mind is that these threads behave just like POSIX threads. This means that almost everything is the responsibility of the programmer. You need to handle mutex locks (with the methods `acquire` and `release`), as well as create the original mutexeces with the method `allocate_lock`. When you are done, you need to `exit` the thread to ensure that it is properly cleaned up and no resources get left behind. You also have fine-grained control over the threads, being able to set things like the stack size for new threads.
