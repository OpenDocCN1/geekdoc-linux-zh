
# Tutorial Erlang

![](img/1f330653f83dcf0397f7d224ce8bbc16_45_0.png)

Mihalis Tsoukalos is a UNIX administrator, a programmer (UNIX & IOS), a DBA and a mathematician. He has been using Linux since 1993. You can reach him at @mactosouk (Twitter) and his website: mtsoukalos.eu

- Resources
- An installation of Erlang
- A text editor such as Emacs or vi

## Program in Erlang: Functions

Discover Erlang functions and basic Erlang data types as well as other interesting and helpful Erlang topics

![](img/1f330653f83dcf0397f7d224ce8bbc16_45_1.png)

This tutorial is the second one in the series of tutorials about the Erlang programming language. The main subject of this tutorial is Erlang data types and functions.

As you might remember from the tutorial in the previous issue, all Erlang code comes in modules unless you are experimenting in the Erlang shell. As a result, all Erlang code comes in functions. Erlang has a pretty unusual way of defining functions, especially if you are used to programming languages such as C or Python, which will be explained here. Additionally, as Erlang is a functional programming language, it also supports anonymous functions, which are also going to be illustrated. You will also learn about atoms, lists, maps and tuples, so start reading!

## More About Erlang

Concurrency is a central part of Erlang. As a result, Erlang processes, which should not be confused with Linux processes, are lightweight. Put simply, Erlang processes are easy to create, much easier than Linux processes, as they require a very small amount of time and have a small memory overhead. Erlang processes do not communicate with each other using memory, which is a risky thing, but by using messages. Furthermore, as processes are independent, the memory space of each process can be garbage-collected individually. Last, the failure of a process cannot do any damage to other processes, therefore allowing them to continue their jobs.

## More About OTP

OTP is a central part of Erlang and the Erlang way of thinking, because it allows you to make your Erlang applications highly available. This section will talk a little bit more about OTP in order to get a better understanding of it.

OTP is unique among programming languages and allows teams to work and develop distributed, fault-tolerant, scalable and highly available systems.

Despite its name (Open Telecom Platform), OTP is domain independent, which means that you can program applications for many different areas.

OTP consists of three main parts. These are the Erlang language itself, various tools that come with Erlang, and the design rules, which are generic behaviours and abstract principles that allow you to focus on the logic of the system. The behaviours can be worker processes that do the dirty work, while supervisor processes monitor workers as well as other supervisors. In order to do this right, the developer should structure the processes appropriately.

That is enough information about OTP for this tutorial; you will learn even more details about OTP in forthcoming tutorials.

## Variables and Numbers

As expected, Erlang supports two kinds of numbers, integers and floats.

When defining floats, you should always have a number on the left of the decimal point, even if it is zero. If you forget to do so, you will get the following kind of error message:

![](img/1f330653f83dcf0397f7d224ce8bbc16_46_0.png)

```
1) MyFloat = .987.
2 1: syntax error before: `'.
```

If the statement is correct, Erlang will reply by printing the float value:

```
1) MyFloat = 0.987.
   0.987
```

**Figure 1** shows an interaction with the Erlang shell where many variables are declared and used. You should pay special attention to the `b()` function that prints all defined variables and the `f()` function that clears all the bound variables when executed without any parameters or a specific variable when the variable is given as an argument.

## Erlang data types

Erlang supports many data types including atoms, maps, lists and funs. An atom is used for representing a constant value. Atoms have a global scope and start with lowercase letters:

```
1> linux.
linux
2> 12.
12
```

As you can see, the value of an atom is the atom itself! Although it looks strange to discuss the value of an atom or integer, the functional nature of Erlang requires that each expression has a value, which also applies to atoms and integers, despite the fact that they are naive expressions.

A fun is a functional object that also allows you to create anonymous functions, which you can pass as arguments to other functions as if they were variables, without having to use their names. **Figure 2** shows a part of the use Erlang reference about the `fun` keyword – a forthcoming tutorial will talk more about anonymous functions.

A map is a compound data type that can contain a variable number of key-value pairs. Each pair is called an element – the total number of elements is called the size of the map. The following shell command shows how to create a map:

```
1> MYPAY = #{country=>greece, city=>athens,
year=>2016, date=>nov,18}.
2 # {city => athens,country => greece, date =>
(nov,18},year => 2016}
```

As you can understand, there are many functions that allow you to manipulate maps – you can see some of them in **Figure 3**.

A list is another compound data type with a variable number of elements. You can define a new list in the Erlang shell as follows:

```
1> LIST1 = [a, b, c, {a,b}].
[ a, b,c,{a,b}]
```

Please also bear in mind that behind the scenes Erlang treats strings as lists, so everything that can work on a list can also be used for strings.

A unique process ID identifies each Erlang process. A PID has the following form and its own data type, which means that you cannot use a process ID as if it was a string:

```
1> self().
<<0.57.0>
```

![](img/1f330653f83dcf0397f7d224ce8bbc16_47_0.png)

![](img/1f330653f83dcf0397f7d224ce8bbc16_47_1.png)

![](img/1f330653f83dcf0397f7d224ce8bbc16_47_2.png)

**Right** The use of b() and f() functions as well as the declaration of numeric variables in Erlang

**Across** This is a small part of the Erlang reference about the **fun** keyword

The **self()** function returns the process ID of the calling process. Similarly, the **spawn()** function returns the process ID of the new process, which is used for sending messages to it:

```
1> c(hw).
   [ok,hw]
2> spawn(hw, helloWorld, []).
   hello_world!
   <0.65.0>
```

As you can see, spawn() takes three parameters, which are the name of the module the function belongs to, the name of the function, and the parameters of the function, which are passed as a list. If the function takes no parameters, you should pass an empty list. Figure 3 shows how to define and process maps and lists inside the Erlang shell.

## Tuples and guards

A **guard** will allow you to specify the kind of data a given function will accept. Although it might just look a little fuzzy at the moment, you will see Erlang code that uses guards later on in this tutorial. The **when** keyword indicates a guard. The condition of a guard is relatively simple and will allow you to do pattern matching based on the content of the argument and not just on its shape.

A tuple is a composite data type, which means that a tuple allows you to combine multiple items into a single data type and store them using a single variable. Most of the times Erlang tuples group two to five items. Moreover, the first atom of a tuple usually identifies the purpose or the category of the tuple. You can declare a tuple as follows:

```
> T1 = {linux, 1}.
   {linux,1}
```

The element() function allows you to access a given item of a tuple:

```
> element(1, T1).
   linux
```

As you can see, the first element of a tuple has an index number of 1. Similarly, the **setelement()** function allows you to change the value of an existing tuple item in order to create a new tuple:

```
> T2 = setelement(1, T1, unix).
   {unix,1}
```

Tuples are handy as they let you group data and are frequently used in Erlang as well as other programming languages.

## Erlang functions

A function in Erlang is a sequence of function clauses that are separated by semicolons and terminated using a period/full stop (.). A function clause has the following form:

```
> F = fun(X) -> 2*X end.
   #fun<erl_eval.5.232829458>
```

The previous code creates an anonymous function with one argument. The anonymous function is bound to a variable named F, which is also an atom. You can use it as follows:
