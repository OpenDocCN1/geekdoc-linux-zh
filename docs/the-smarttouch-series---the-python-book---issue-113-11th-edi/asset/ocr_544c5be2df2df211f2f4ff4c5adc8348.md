# Python essentials

# Extend your Python

Find out how to digitally sign a release APK and upload it to an app store of your choice

With the Python interpreter, you aren't just limited to what is already available; you can extend the available functionality by defining your own Python objects, with their own methods and data, within your C code. These newly-created objects can then be called from within the Python interpreter. They are defined as static objects, with code like:

```
```c
static PyObject* my_func(PyObject *self,  PyObject *args) {
...
}
```
```

The new PyObject contains the executable code for the method to be used for your new object. You also need to create a method definition to be able to register the details with the Python interpreter. You do this by creating a PyMethodDef array:

```
```c
static PyMethodDef my_methods[] = {
  {"my_method", my_func, METH_VARARGS,
  "This is my method"},
  (NULL, NULL, 0, NULL)
};
```
```

Once you have finished these two parts, you are almost ready to start using your new module code. You need to initialise it with the function:

```
```c
PyObject_CallObject(my_func, NULL);
```
```

With this access, you should be able to do just about anything you wish in Python.

Up to now, we have been specifically looking at code interacting with the Python interpreter. But there are occasions where you want to allow the end user to have access to the interpreter. In these cases, you probably want to give your user access to a full Python console. You can do just such a thing with the function call Py\_Main(argc, argv), where you hand in the argc and argv that you have from the C side of your program. This is fine for a console-based program, but for a GUI program, you need to create some kind of terminal window to allow the user to interact with the Python interpreter. This console will automatically continue to run until the user explicitly quits from Python. The

```
```c
Py\_InitModule("my_module", my\_methods);
```
```

Now, you can import this new module in your Python code, just like any other module installed on your system. Within your Python code, you can write:

```
```python
import my\_module
my\_module.my\_method()
```
```

One thing to be aware of is that this level of control also gives you a huge level of responsibility. For example, you will need to start worrying about things like reference counts for objects. The garbage collector for the interpreter needs to know when an object is okay to delete, you need to increment the reference count each time something points to your newly created object. Every time a reference is removed, you need to decrement the counter.

You can also create multiple sub-interpreters within a single program. You can create a new sub-interpreter with the function Py\_NewInterpreter(). This way, you can have multiple Python threads running concurrently, and mostly independently. When you are done, you can shut them down with the function Py\_EndInterpreter(). There is no limit to what you can do with all of this power.

last thing you need to do is to clean up after the interpreter. You can do this with the function void Py\_Finalize(). The major issue with this function is that it destroys objects in a random order. If they depend on other objects, they may not be able to get cleaned up correctly. If you then try and re-initialise the interpreter again, it may fail due to an unclean finalisation step.

Now that you have your program written, you need to compile it. You need to include flags to tell the compiler where to find everything. Luckily, you can get these from Python itself. The flags needed for compiling are available with the command python-config --cflags. You also need to know where to find the libraries to link in, which are available with python-config --ldflags. After completing all of this you will have access to Python anywhere, even within another program.

# Code listing

```
```c
# A simple way to run Python code
#include <Python.h>

int main(int argc, char *argv[]
)
{
Py\_SetProgramName(argv[0]);
# Initialize the Python
interpreter
Py\_Initialize();
# Run your SimpleString "from time
import time,time\""\n"
PyRun\_SimpleString("from time
import time,time\"\"\n"
"'print 'Today is ',ctime(time())\"\n");
# Don't forget to clean up
Py\_Finalize();
return 0;
}
```
```

```
```c
# You can create an interactive
Python console
#include <Python.h>
int main(int argc, char *argv[]
)
{
Py\_Initialize();
Py\_Main(argc, argv);
Py\_Finalize();
}
```
```

```
```c
# You can even run a script file
#include <Python.h>
int main(int argc, char *argv[]
)
{
FILE *fp;
Py\_Initialize();
fp = fopen("my\_script.py", "r");
PyRun\_SimpleFile(fp, "my\_script.py");
Py\_Finalize();
fclose(fp);
}
```
```

# WHY PYTHON

It's the official language of the Raspberry Pi. Read the docs at python.org/doc