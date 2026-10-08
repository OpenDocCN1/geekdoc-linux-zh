# rusage

# Description

The rusage command is similar to time(1). It runs the command, which you must specify; that is, command() is not optional as it is in the C shell timing facility. When the command is complete, rusage displays the real (wall clock), the system CPU, and the user CPU times that elapsed during execution of the command, plus other fields in the rusage structure, all on one long line. Times are reported in seconds and hundredths of a second.

# Examples

The following example shows the format of rusage output.

```
castle# rusage wc /kookaburra-1
      9 47 264 kookaburra-1
0.07 0.02 user 0.03 sys 0 pf 0 sw 0 rb 0 wb 0 vcx 0 icx 0 mx 0
ix 0 id 0
cast#
```

Each of the fields identified corresponds to an element of the rusage structure, described in getrusage(3C), as follows:

| real elapsed time |
| user ru_utime user used |
| sys ru_stime system time used |
| pf ru_majflit page faults requiring physical I/O |
| pr ru_minflt page faults requiring physical I/O |
| sw ru_nswap swaps |
| rb ru_inblock block input operations |
| wb ru_oublock block output operations |
| vcx ru_nvcsw voluntary context switches |
| icx ru_nivcsw involuntary context switches |
| mx ru_maxrss maximum resident set size |
| ix ru_idrss currently 0 |
| id ru_idrss integral resident set size |
| is ru_isrss currently 0 |

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type Attribute Value |
| Availability sunmcpu |

# See Also

csh(1), time(1), getrusage(3C), attributes(5)

# Bugs

When the command being timed is interrupted, the timing values displayed may be inaccurate.