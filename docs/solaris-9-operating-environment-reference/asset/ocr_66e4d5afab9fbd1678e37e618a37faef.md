# true, false

# true, false — Provide Truth Values

# Synopsis

```
/usr/bin/true
/usr/bin/false
```

# Description

true does nothing, successfully. false does nothing, unsuccessfully. They are typically used in a shell script sh as:

```
while true
  do
    command
  done
```

which executes command forever.

# Exit Status

+   - true
  0.
- false
  A non-zero value.

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNmcu |

# See Also

sh(1), attributes(5)

# truss — Trace System Calls and Signals

# Synopsis

```
/usr/bin/truss [-fcaeildD] [- [tVx] [!]syscall,...] [-s [!]signal,...]
-mM [!]fault,...] [-rw] [!]fd,...] [-uU] [!]lib,...[:]
[!]func,...] [-o outfile command | -p pid
```

# Description

The truss executes the specified command and produces a trace of a system calls it performs, the signals it receives, and the system faults it incurs. Each line of the trace output reports either the fault or signal name or the system call name with its arguments and return value(s). System call are displayed symbolically when possible, using definitions from relevant system headers; for any path-name pointer