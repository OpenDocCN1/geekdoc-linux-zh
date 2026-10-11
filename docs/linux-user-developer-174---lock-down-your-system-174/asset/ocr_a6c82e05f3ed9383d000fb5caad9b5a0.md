# Tutorial Erlang

![](bbox=[0.06, 0.16, 0.19, 0.27])

Mihalis Tsoukalos is a UNIX administrator, a programmer (UNIX & IOS), a DBA and a mathematician. He has been using Linux since 1993. You can reach him at @mactosouk(Twitter) and his website: mtsoukalos.eu

+   Resources
+   An installation of Erlang
+   A text editor such as Emacs or vi

# Program in Erlang:
Functions

Discover Erlang functions and basic Erlang data types as well as other interesting and helpful Erlang topics

![](bbox=[0.06, 0.74, 0.17, 0.91])

This tutorial is the second one in the series of tutorials about the Erlang programming language. The main subject of this tutorial is Erlang data types and functions.
As you might remember from the tutorial in the previous issue, all Erlang code comes in modules unless you are experimenting in the Erlang shell. As a result, all Erlang code comes in functions. Erlang has a pretty unusual way of defining functions, especially if you are used to programming languages such as C or Python, which will be explained here. Additionally, as Erlang is a functional programming language, it also supports anonymous functions, which are also going to be illustrated. You will also learn about atoms, lists, maps and tuples, so start reading!

# More About Erlang

Concurrency is a central part of Erlang. As a result, Erlang processes, which should not be confused with Linux processes, are lightweight. Put simply, Erlang processes are easy to create, much easier than Linux processes, as they require a very small amount of time and have a small memory overhead. Erlang processes do not communicate with each other using memory, which is a risky thing, but by using messages. Furthermore, as processes are independent, the memory space of each process can be garbage-collected individually. Last, the failure of a process cannot do any damage to other processes, therefore allowing them to continue their jobs.

# More About OTP

OTP is a central part of Erlang and the Erlang way of thinking, because it allows you to make your Erlang applications highly available. This section will talk a little bit more about OTP in order to get a better understanding of it.
OTP is unique among programming languages and allows teams to work and develop distributed, fault-tolerant, scalable and highly available systems.
Despite its name (Open Telecom Platform), OTP is domain independent, which means that you can program applications for many different areas.
OTP consists of three main parts. These are the Erlang language itself, various tools that come with Erlang, and the design rules, which are generic behaviours and abstract principles that allow you to focus on the logic of the system. The behaviours can be worker processes that do the dirty work, while supervisor processes monitor workers as well as other supervisors. In order to do this right, the developer should structure the processes appropriately.
That is enough information about OTP for this tutorial; you will learn even more details about OTP in forthcoming tutorials.

# Variables and Numbers

As expected, Erlang supports two kinds of numbers, integers and floats.
When defining floats, you should always have a number on the left of the decimal point, even if it is zero. If you forget to do so, you will get the following kind of error message: