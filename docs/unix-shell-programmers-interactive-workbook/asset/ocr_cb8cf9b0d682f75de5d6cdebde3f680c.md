# Chapter 5: Parameters 235

+   3) Again assuming myfunc is defined in a file named ~/fun/myfunc, what happens the second time you run a myfunc command?
a) Nothing, because the shell knows it has already executed this file.
b) Nothing, because the shell knows it has already executed this function.
c) Nothing, because the shell knows it has already executed ~/bin/myfunc.
d) The shell executes ~/fun/myfunc then executes the newly defined function.
e) The shell executes the already-defined function, myfunc.

+   4) After running myfunc the first time, you can modify or delete ~/fun/myfunc and the shell will continue to use the definition it found the first time you ran it.
a) True
b) False

+   5) What is the difference between using "@" and "*" as a parameter to a command?
a) There is no difference because they are both in quotes.
b) The positional parameters will be passed as separate values using "@", but will be passed as a single value using "*".
c) The positional parameters will be passed as separate values using "*", but will be passed as a single value using "@".
d) "@" reverses the order of the parameters, but "*" does not.
e) "*" reverses the order of the parameters, but "@" does not.

+   6) What is the difference between $@ and $* as a parameter to a command?
a) There is no difference because neither is in quotes.
b) The positional parameters will be passed as separate values using $@, but will be passed as a single value using $.*
c) The positional parameters will be passed as separate values using $*, but will be passed as a single value using $@.
d) $@ reverses the order of the parameters, but $* does not.
e) $* reverses the order of the parameters, but $@ does not.