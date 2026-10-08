
# mdb 839

[address] :::dump [-eqrstu] [-f] [-g bytes] [-w paragraphs]

Print a hexadecimal and ASCII memory dump of the 16-byte-aligned region of memory containing the address specified by dot. If a repeat count is specified for ::dump, this is interpreted as a number of bytes to dump rather than a number of iterations. The ::dump dcmd recognizes the following options.

-   -e Adjust for endianness. The -e option assumes 4-byte words. We can use the -g option to change the default word size.
-   -f Read data from the objectfile location corresponding to the given virtual address instead of the target's virtual address space. The -f option is enabled by default if the debugger is not currently attached to a live process, corefile, or crash dump.

-   -g bytes Display bytes in groups of bytes. The default group size is 4 bytes. The group size must be a power of 2 that divides the line width.

-   -p Interpret address as a physical address location in the target's address space instead of a virtual address.

-   -q Do not print an ASCII decoding of the data.

-   -r Number lines relative to the start address instead of with the explicit address of each line. This option implies the -u option.

-   -s Elide repeated lines.

-   -t Read and display only the contents of the specified addresses instead of reading and printing entire lines.

-   -u Unalign output instead of aligning the output at a paragraph boundary.

-   -w paragraphs Display paragraphs at 16-byte paragraphs per line. The default number of paragraphs is 1. The maximum accepted value for paragraphs is 16.

This dcmd is new in the Solaris 9 release and replaces the Solaris 8 ::dump dcmd.

```
:echo [string | value...]
```

Print the arguments separated by blanks and terminated by a newline standard output. Expressions enclosed in $ [ ] are evaluated to a value and printed in the default base.

```
:eval command
```

Evaluate and execute the specified string as a command. When the command contains metacharacters or white space, enclose it in double or single quotes.

# 840

# mdb

```
::events [ -av]
$ [ -av]
```

Display the list of software event specifiers. Each event specifier is assigned a unique ID number that you can use to delete or modify the event specifier at a later time. The debugger can also have its own internal events enabled for tracing. These events are displayed only when you specify the -a option. Specifying the -v option shows a more verbose display, including the reason for any specifier inactivity. In the Solaris 9 release, The following example shows some sample output.

```
::events
ID S TA HT LM Description Action
------------------------------------------------------
[ 1 ] - T 1 0  | stop on SIGINT 
[ 2 ] - T 0 0  | stop on SIGQUIT 
[ 3 ] - T 0 0  | stop on SIGILL 
[ 11 ] - T 0 0  | stop on SIGXCPU 
[ 11 ] - T 0 0  | stop on SIGXCPU 
[ 12 ] - T 0 0  | stop on SIGFSZ 
[ 13 ] - 2 0  | stop on libcprintf ::echo >
```

The following list explains the meaning of each column. You can display a summary of this information with ::help events.

The event specifier identifier. The specifier is in square brackets [] if the specifier is enabled, in parentheses () if the specifier is disabled, or in angle brackets <> if the target program is currently stopped on an event that matches the given specifier.

The event specifier state. The state is shown with one of the following symbols.

-   - The event specifier is idle. When no target program is running, all specifiers are idle. When the target program is running, a specifier can be idle if it cannot be evaluated (for example, a deferred breakpoint in a shared object that is not loaded).
-   - The event specifier is active. When the target is continued, events of this type are detected by the debugger.
-   - The event specifier is armed. This state means that the target is currently running with instrumentation for this type of event. This state is visible only if the debugger is attached to a running program with the -o nostop option.
-   - The event specifier is not armed because of an operating system error. You can use the ::events -v option to display more information about the reason the instrumentation failed.

# mdb 841

-   TA The Temporary, Sticky, and Automatic event specifier properties.
One or more of the following symbols can be shown.

-   t The event specifier is temporary and is deleted the next time the target stops, regardless of whether it is matched.
-   T The event specifier is sticky and is not deleted by :delete all or z. You can delete the specifier by explicitly specifying the ID number to :delete.
-   d The event specifier is automatically disabled when the hit count is equal to the hit limit.
-   D The event specifier is automatically deleted when the hit count is equal to the hit limit.
-   S The target stops automatically when the hit count is equal to the hit limit.
-   HT The current hit count. This column displays the number of times the corresponding software event has occurred in the target since the creation of this event specifier.
-   LM The current hit limit. This column displays the limit on the hit count at which the autodisable, autodelete, or autostop behavior takes effect. You can configure these behaviors with the ::evset dcmd.

## Description

A description of the type of software event that is matched by the given specifier.

## Action

The callback string to execute when the corresponding software event occurs. This callback is executed as if it had been typed at the command prompt.

```
[id] :evset [+/-DestT] [-c cmd] [-n count] id...
```

Modify the properties of one or more software specifiers. The properties are set for each specifier identified by the optional expression preceding the dcmd and an optional list of arguments following the dcmd. The argument list is interpreted as a list of decimal integers unless you specify an explicit radix. New in the Solaris 9 Release.
::evset dcmd recognizes the following options.

```
-c cmd
```

Execute the specified cmd_string each time the corresponding software event occurs in the target program. You can display the current callback string with ::events.

# 842

# mdb

-   -d Disable the event specifier when the hit count reaches the hit limit. When you specify the +d form of the option, this behavior is disabled. Once you disable an event specifier, the debugger removes any corresponding instrumentation and corresponding software events until the specifier is subsequently reenabled. If the -n option is not present, the specifier is disabled immediately.
-   -D Delete the event specifier when the hit count reaches the hit limit. Specifying the +D form of the option disables this behavior. The -D option takes precedence over the -d option. You can configure the hit limit with the -n option.
-   -e Enable the event specifier. When you specify the +e form of the option, the specifier is disabled.
-   -count Set the current value of the hit limit to count. If no hit limit is currently set and the -n option does not accommodate -s or D, the hit limit is set to 1.
-   -s Stop the target program when the hit count reaches the hit limit. Specifying the +s form of the option disables this behavior. The -s behavior tells the debugger to act as if ::count were never following each execution of the specifier's callback, except for the execution, where n is the current value of the specifier limit. The -s option takes precedence over the -D and -d options.
-   -t Mark the event as temporary. Temporary specifiers are automatically deleted the next time the target stops, regardless of whether it stopped as the result of a software event corresponding to the given specifier. Specifying the +t form of the option removes the temporary marker. The -t option takes precedence over the -d option.
-   -T Mark the event as sticky. Sticky specifiers are not deleted by ::delete all or :z. You can delete them by specifying the corresponding specifier ID as an explicit argument to ::delete. Specifying the +T form of the option removes the sticky property. The default set of event specifiers are all initially sticky.

You can display a summary of this information with ::help evset.

```
::files $ Print a list of the known source files (symbols of type ST_FILE present in the target symbol tables).
```

```
[fl]:fltbp [+dDestT] [-c cmf] [-n count] flt...
```

Trace the specified machine faults. The faults are identified with an optional fault number (<sys/fault.h>) following the dcmd, or a list of fault names as -d, -D, -e, -s, -t, -C, and -n have the same meaning as they do for the ::evset dcmd. In the Solaris 9 release
