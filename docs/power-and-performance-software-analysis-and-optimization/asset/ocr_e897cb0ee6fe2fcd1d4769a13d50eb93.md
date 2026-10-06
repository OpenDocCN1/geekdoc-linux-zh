# CHAPTER 11 Other Helpful Tools

One of the major limitations of gprof is its lack of the ability to profile code located in dynamically linked libraries. A simple workaround is to statically link the executable to be profiled when compiling with the gprof instructions.

# 11.2 GCOV

The GNU code coverage tool, gcov, isn't much of a profiling tool. Instead, its primary tool is to measure the code coverage achieved by unit tests; however, the tool is worth mentioning since it provides one piece of information: the percentage of times each conditional branch was taken. This is especially useful outside, of routine error handling branches, programmers to be poor judges of which branches are frequently taken and which are skipped.

Similar to gprof, gcov also relies on the compiler to instrument the application's executable, but the compiler flag used is different. At the time of running, gcov is only well supported by GCC. Both ICC and LLVM provide their own coverage tools, which are incompatible; however, it may provide more information from them.

In order to enable coverage instrumentation with GCC, the application executable must be compiled and linked with the `--coverage` compiler flag. The instrumented executable is then run. The code inserted into the instrumented executable will generate two binary files for each source file, a `.gno` and `.gcda`. For instance, `foo.c` will have a corresponding `foo.gno` and `foo.gcda` file.

These files are converted into a text report by running `gcov()` with the desired source file as an argument. Rather than printing the results to `stdout`, a new text file will be created report, reporting the coverage for the source file passed as an argument. The name of this file is the source file name, a `.gcov` suffix appended. Continuing the previous example, `gcov foo.c` will generate a text file report in the file `foo.c.gcov`.

The report will include a full list of the listed file, along with annotations about the number of times each line was executed. In order to add the branching information, the `-b` option must be added to the `gcov(1)` command. For example:

```
$ gcc test.c -o test --coverage
./test
$ gcov -b test.c
```

Listing 11.3 provides a sample excerpt from one of these annotated source code. In this example, there are two branches of interest, one starting on line 1 and one starting on line 5. The annotations on the left side provide the number of times each statement was executed, along with the percentage of times that branch was taken, the fallthrough case; and the percentage of times where the branch was not taken. For example, looking at the branch statistics on lines 2 and 3, it is obvious that this branch is frequently taken. On the other hand, the