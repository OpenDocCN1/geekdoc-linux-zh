# 466

# gprof

though profiled, appear to be spontaneous (although for more obscure reasons). Any profiled children of signal catchers should have their times propagated properly unless the signal catcher was invoked during the execution of the profiling routine, in which case is all lost.

# Options

+   -a Suppose printing statically declared functions. If you specify this option, all relevant information about the static function (instance, time samples, calls to other functions, calls from other functions) belongs to the function loaded just before the static function in the a.out file.

+   -b Suppress descriptions of each field in the profile.

+   -c Discover the call graph of the program by a heuristic that examines the text space of the object file. Indicate static-only parents or children with call counts of 0.

+   -D Demangle C++ symbol names before printing them.

+   Produce a profile file gmon.sum that represents the difference of the profile information in all specified profile files. You can give the summary profile file to subsequent executions of gprof (also with -D) to summarize profile data across several runs of an a.out file. See also -s option.

As an example, suppose function A calls B n times in profile file gmon.sum, and m times in profile file gmon.out. With -D, create a new gmon.sum profile file showing the number of calls from A to B as n-m

+   -e function-name Suppress the graph profile entry for routine function-name and all its descendants (unless they have other ancestors that are not suppressed). You can specify more than one -e option. You can specify only one function-name with each -e option.

+   -E function-name Suppress printing the graph profile entry for routine function-name and its descendants (as -e), and also exclude the time spent in function-name and its descendants from the total and percentage time computations. You can specify more than one -E option. For example, the default is `-E mcount -E mcleanup`

+   -f function-name Print the graph profile entry only for routine function-name and its descendants. You can give more than one -f option. You can specify only one function-name for each -f option.