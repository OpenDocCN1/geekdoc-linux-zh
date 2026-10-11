![](bbox=[0.08, 0.15, 0.46, 0.3])

![](bbox=[0.44, 0.15, 0.82, 0.3])

# Across

How to define a map and a list in Erlang shell, including functions that help you deal with maps and lists

# Left

The implementation of the process_tuple() function that illustrates how to process tuples

```
3> F(4).
8
4> F(4.5).
9.0
```

The number of the arguments of a function is called the arity of the function. It is the combination of the module name (m), the function name (f) and the arity (N) that uniquely identifies a function as m:f/N. As you might remember, you have to export a function in order to be able to use it outside of the module that it belongs to.

The next example shows how to pass functions as arguments to other functions! Type the following at the Erlang shell:

```
1> F=fun(X) -> 2*X end.
#fun(erl_eval.6.52032458)
2> Five = fun(N, Function) -> 5 * Function(N) end.
#fun(erl_eval.12.52032458)
3> Five(18,F).
100
4> F(18).
20
```

Here, you define two anonymous functions, named F() and Five(). The Five() function takes two arguments, which is an integer N and a function Function and multiplies the numeric result of Function(N) with the number 5!

# More about functions

Erlang supports much more complex functions than the ones you saw in the previous section. The following example will illustrate how to use a function to process a tuple. Please have in mind each tuple counts as a single function argument. A very common way to process tuples is by using pattern matching. Figure 4 shows the code of the process_tuple() function that processes tuples as found in tuples.erl. Executing tuples:main() generates the next output:

```
15> c(tuples).
[ok,tuples]
16> tuples:main().
Size: 6 First element: [1,2]
Size: 4 First element: a
Ok.
```

The last example will show a function that processes tuples

using guards and a case statement, which is a pretty common practice in Erlang. Figure 5 shows the relevant Erlang code as found in more_fun.erl. Using more_fun:check_temp() generates the following kind of output:

```
11> c(more_fun).
[ok,more_fun]
more_fun.erl:12: Warning: variable 'N' is unused
more_fun.erl:14: Warning: variable 'N' is unused
[ok,more_fun]
12> more_fun:check_temp({fahrenheit, 50}).
'Do not know about Fahrenheit!'
13> more_fun:check_temp({kelvin, 50}).
"Cannot tell about Kelvin!"
14> more_fun:check_temp({celcius, 50}).
'Way too hot!'
15> more_fun:check_temp({celcius, 10}).
"It is getting cold..."
```

As you can see, not all case statements must have a guard.

# More information about the Erlang shell

The q() function is the easiest way to exit the Erlang shell, but keep in mind that the q() function quits everything. Erlang is dying. If you are working locally then there is no problem, but if you are working on a remote system you'd better quit by typing Ctrl+C and then Q. The reason is that you may shut down the Erlang runtime on the remote machine when quitting using q()! The built-in line editor offer is a subset of Emacs.

In Figure 6 you will see some more advanced commands of the Erlang shell, including the declaration of a function, the use of the h() function to print the history list, and two alternative ways to exit the Erlang shell, the init:stop() function as well as the halt() function.

# Getting user input

Although Erlang is primarily used for server applications, it can also allow you to interact with users. This section will teach you how to get user input from Erlang, which is pretty handy when you are developing small interactive programs or other command-line utilities.

Although it is relatively easy to get user input from the Erlang shell, the tricky part is verifying that the input is valid in order to avoid exceptions: