```
process_input(I,
    io:format("= `n`I", [N]),
 catch
    ... ->
        usage()
end;
main(_) ->
    usage().

usage() ->
    io:format("Usage: scriptName integer\n"),
    halt(1).

process_input({Ok, Data}) when is_tuple(Data) ->
    Name = element(1, Data),
    io:format("""", [Name]);

process_input({Error, _}) ->
    io:format("There is an error somewhere."),

```

![](bbox=[0.48, 0.16, 0.72, 0.35])

Left The use of the fibo() function found in fibo1.erl

After creating the script file, you should change its permissions:

```
$ chmod 755 afile.erl
$ ls -1 afile.erl
---rw-r--x  1 mtsouk staff  0 Nov 14 15:30
afille.erl
```

Next, you can execute afilo.erl as if it was a regular shell script:

```
$ ./afile.erl 123
Please give (Name) >> (“Mihalis”).
“Mihalis”: 123
```

# Calculating Fibonacci numbers

You will now learn how to calculate Fibonacci numbers in a different way than the one you saw in the previous issue of Linux User and Developer. The code of the fibo() function, which can be found in fibo1.erl, is the following:

```
fibo(0) when N > 0 -> fibVar(N, 0, 1).

f2ivar(0, F1, F2) -> F1.
f2ivar(N, F1, F2) -> fibVar(N-1, F2, F1 + F2).
```

You can see its performance using the timer() command in Figure 8. The implementation of fibo() in fibo1.erl uses another function that is named fibvar() and takes three arguments instead of just one. However, as fibvar() is only used internally, it does not need to be in the export() list of the module. The only function in the export() list is main().

![](bbox=[0.48, 0.54, 0.72, 0.7])

Left The use of the fibo() function found in fibo2.erl as well as its entire Erlang code

As you can see, you just have to embed your Erlang code into a text file in a specific way and read the command line arguments as a list using the list_to_integer() function. This is a very pretty way of creating small Erlang programs that do so specific but relatively small tasks. The next tutorial will talk about many interesting things including formatting output, lists, maps, records and message passing between Erlang processes. Until then, write as much Erlang code as you can!

# Infinite loops

The following Erlang code, when combined with a negative integer as an argument, generates a function that keeps running and never ends:

```
fibo(0) -> 0;
fibo(1) -> 1;
fibo(N) -> fibo(N-1) + fibo(N-2).
```

In other words, you should be very careful when defining the arguments that a function can accept, and put guards where necessary in order to avoid such bugs. A more appropriate and secure definition of fibo() would be the following:

```
fibo(N) when N > 0 -> fibVar(N).
fibvar(0) -> 0;
fibvar(1) -> 1;
fibvar(N) -> fibvar(N-1) + fibvar(N-2),
```

# More about Fibonacci numbers

Although the Erlang code of fibo2.erl is different from the code you saw in the previous issue, there is another way to calculate Fibonacci numbers in Erlang, which uses a list, as well as the implementation of the fibo() function, which uses a list, as well as its performance, can be seen in Figure 9. Just remember to compile the code the first user gets, which is the Erlang compiler. As you can see, not all Fibonacci implementations are equal!