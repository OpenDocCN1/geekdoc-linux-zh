
# A Look at Lua

An overview of the compact yet powerful Lua programming language. **JOSEPH QUIGLEY**

**Lua is a free** and open-source multi-paradigm programming language released under the MIT license. Created in 1993 by Roberto Ierusalimschy, Luiz Henrique de Figueiredo and Waldemar Celes, Lua is a dynamically typed language. Extremely compact (only 150KB compiled), it is primarily used as a scripting language or an extension to another language (mainly *C/C++*).

## What Is Lua and How Is It Used?

Lua is implemented as a library and has no “main” program. It works only when embedded in a host client. The interpreter is a C program that uses the Lua library to offer a standalone Lua interpreter. Rather than provide a complex and rigid specification for a single paradigm, Lua is intended to be extended to fit different problem types.

Being small, Lua fits on many host platforms and has been ported and used in video games for both the PlayStation Portable and the Nintendo DS, and it is used in larger games, such as *Far Cry* and *World of Warcraft*. The Adobe Photoshop Lightroom photography program and the lighttpd Web server have incorporated Lua as well. Lua has a few advanced features, primarily coroutines, garbage collection, first-class functions and dynamic module loading. Because Lua is small, it includes only a few data types. It attempts to maintain a balance between power and small size.

## What’s Different about Lua?

Lua is comparably as easy as Python in terms of learning how to write code. Of the two, Lua is usually the better choice for embedded systems, simply because it’s smaller. Lua’s strength is in processing strings and tables. It handles logical equations more adeptly than Python. For a quick hack, a Lua programmer can process complicated data more quickly and easily than a Python programmer can (although a Ruby programmer can do so almost as quickly). But, for a large application that handles many chunks of complex data, a heavier language such as Ruby or Python may be a better choice.

There is no need to worry about different types of integers. You may have found that the different types of integers and numbers (such as floats, longs or doubles) can screw up the output of your program or even make it crash if you are absent-minded. Lua uses coercion for every integer and number type to convert it into a single type. You can add a float, long integer or a double to any other type of integer or number without a hitch in Lua. In contrast, doing this can cause programs written in Python 2.4 or older versions to crash. Lua is extremely forgiving syntactically. What if, for some reason, you are programming on an embedded device with a four-inch wide screen? You can reduce the amount of lines and other characters, which in turn enables easy reading of the code to make up for the small screen.

Small is beautiful. A programmer can embed Lua into several other languages, such as *C/C++* and Java, without bloating the host language, because Lua has a tiny API. Similar to Lisp’s single data structure, tables are the only data structuring mechanism that Lua has. This makes tables very powerful, because with a little work, they can emulate data structures in larger languages.

Object-oriented programming implementation is minimalistic. Lua uses tables and functions rather than classes.

In contrast to Python, Lua does not focus on 100% backward compatibility. Many newer releases of Lua break programs written in previous versions. Fortunately, the Lua developers always announce what the new versions of Lua will break.

Lua supports threading. Multiple Lua interpreters can coexist in the same process, and each one can run independently in its own thread. This often makes Lua desirable for multithreaded programs in embedded systems.

## Installing Lua

To compile and install Lua from the source code, grab a copy of Lua 5.1 from the Lua.org Web site, and untar, configure, make and install it:

```bash
tar -xvzf lua-5.1.1.tar.gz
cd lua-5.1.1
make
make install
```

(xyz is your platform name.)

Lua should now be installed and working. To test your install, type Lua on the command line. An interactive interpreter should appear.

## Syntax

Lua is a dynamically typed language whose syntax is very similar to that of Python and even more similar to Ruby. Line breaks do not play any role in Lua’s syntax, like that of Python or Ruby. Take, for example, the following ugly, but valid code:

```lua
foo = 89
bar = foo + 2
print(bar)
```

Because it is small, Lua has only eight basic data types:

- nil (similar to Python’s None)
- booleans
- numbers
- strings
- functions
- userdata (a type that allows arbitrary C data to be stored in Lua variables)
- threads
- tables

Lua supports only a few data structures, including arrays, lists and hash tables.

The table type implements an associative array that can be indexed with any value (similar to Python), except nil (similar to Python). Nil’s goal is to be different from any other value, as well as the default value for global variables. Nil also plays a much more important role in Lua than None does in Python. Although tables are the only data structuring mechanism in Lua (which may seem like a disadvantage), the table is just as powerful as Python's dictionary and list, and it's even as powerful as Ruby's hash. Tables are used to represent many different types of arrays, sets, trees and several other data structures. One handy feature of tables is to use strings as keys—for example:

```lua
x = { ['hello world!'] = "ciao world!" }
print(x["hello world!"])
```

When running this example, Lua outputs "ciao world!" and not "hello world!" as it might appear.

For a more in-depth look at Lua's tables go to lua-users.org/wiki/TablesTutorial.

### Variables and Identifiers

Because any value can represent a condition, booleans in Lua differ from those in many other languages. Both false and nil are considered false in Lua, but Lua considers everything else true (including zero and an empty string).

Unlike Python, global variables do not need to be declared. To create one, assign a value to it. To delete it, give it the nil value. A global variable exists only if it has a non-nil value. Exactly the opposite of Python, most variables in Lua are global by default, and you must declare the variable "local" to make it a local variable rather than assuming that all variables are local.

Because most CPUs perform floating-point arithmetic just as fast as integer arithmetic, numbers in Lua represent real, double-precision, floating-point numbers rather than common integers. Because Lua doesn't need integer types, it doesn't have them. This eliminates rounding errors, floating-point numbers and long integers.

Lua handles strings very adeptly and has been used for strings that are several megabytes long. It converts between strings and numbers; any numeric operation applied to a string converts the string to a number. This conversion principle applies only to numbers, as Lua converts numbers to strings when strings are expected. Even with automatic conversion, Lua still can differentiate between numbers and strings in cases like 90 == "90" (which always is false).

Identifiers starting with an underscore (such as _FOO) are not recommended for use in Lua, because many are reserved for special uses. As long as an identifier does not begin with a digit, the identifier can be made up of a combination of underscores, letters and digits.

You can basically rename anything in Lua, even to the point of making it non-callable. Take, for example, the following code:

```lua
x = io
x.read()
io = "Hello world!"
```

```lua
x = "Let's make io callable!"
x.read()
```

The second line gets keyboard input through the io module. Because io is essentially a variable with a function as a value, you can give it a different value so that it does not relate to the input/output functions anymore. When you try to get keyboard input from the io module again, Lua returns an error. The program is unable to call the input/output functions now that io's value has been reassigned. In order to use io again, you must restart the Lua program.

### Operators and Assignment

Lua concatenates strings with the `..` operator. Note that `print("Hello".."World!")` is valid, but `print("I've said "Hello World"...5..."or more times.")` is not. This is because Lua sees the periods as decimals after the integer. Otherwise, it won't return an error. The following code validly concatenates the strings and the integer:

```lua
print("I've said "Hello World" ... 5 ... "or more times.")
```

Lua uses many of the common operators that Python, Ruby and most every other language use. For the Python/Ruby logical not operator, Lua can either use it or use `==` for the negation of equality. Always

![](img/526fd434dcfcf1b461b94c24ea170f36_94_0.png)
