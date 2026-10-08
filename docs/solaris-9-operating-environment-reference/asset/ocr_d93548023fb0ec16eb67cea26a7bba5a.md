# 848

# mdb

```
[address] ::stack [count]
[address] $c [count]
```

Print a C stack backtrack. If the dmd is preceded by an explicit address, display a backtrack beginning at this virtual memory address.
Otherwise, display the stack of the representative thread. Specifying an optional count value as an argument displays no more than count arguments for each stack frame in the output.

```
::status
```

Print a summary of information related to the current target.

![](bbox=[0.085, 0.283, 0.135, 0.297])

```
:step [over | out] [SIG]
:s [SIG]
:u [SIG]
```

step the target program one instruction. If you specify an optional signal name or number (see signal(3HEAD)), the signal is immediately delivered to the target as part of resuming its execution. When you specify the over argument, ::step steps over subroutine calls. The ::step out argument is the same as the ::next dmd. When you specify the optional out argument, the target program continues until the representative thread returns from the current function. If no target program is currently running, ::step starts a new program running as if ::run and stops at the first instruction. The ::u dcmd dmd is the same as ::step out. New in the Solaris 9 release.

![](bbox=[0.085, 0.535, 0.135, 0.549])

```
[syscall] ::sysbp [+/-dbtest] [-io] [-c cmd] [-n count] syscall
```

Trace entry or exit from the specified calls preceding the dmd or a list of system call names or numbers (see <sys/syscall.h>) following the dmd. When you use the -i option (the default), the event specifiers trigger on entry into the kernel for each system call. When you specify the -o option, the event specifiers trigger on exit from the kernel. The -d,-e,-s,-t,-T,-C, and -n options have the same meaning as for the ::evsetd dcmd on page 833. New in the Solaris 9 release.

```
::typeset [+/- variable-name...
```

Set attributes for named variables. Specifying one or more variables defines them and sets them to the value of dot. Specifying the -t sets the user-defined tag associated with each variable. Specifying the +t option clears the tag. Specifying no variable names prints the list of variables and their values.

```
::unload module-name
```

Unload the specified dmd. You can print the list of active dmds with the ::dmods dcmd. Built-in modules cannot be unloaded. Modules that are busy (that is, provide dmds that are currently executing) cannot be unloaded.