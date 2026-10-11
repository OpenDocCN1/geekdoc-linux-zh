# **Table 22.4** Commonly used debugging options available for gcc during the compilation phase (continued).

| Option | Purpose | Value | Example |
| --- | --- | --- | --- |
| -print-search-dirs | Prints the names of the directories that gcc will search during the compilation | None | -print-search-dirs |
| -Q | Prints progress information, such as statistics and a list of the functions as they are compiled | None | -Q |
| -save-temps | Saves all temporary intermediate files so that you can examine them | None | -save-temps |

7. If the code you are compiling is going to produce a large program, you probably want to utilize some of the optimization parameters available for the compiler phase. See Table 22.5 for a brief list of the optimization parameters to choose from. The program you are setting up to compile in this example is not going to be huge. Use the lowest level of optimization, giving you the following:

```
gcc -I~/ccode/headers -MD -Wimplicit-pg -O0
```

8. You may find that you need to tell gcc explicitly where to find various types of files. Table 22.6 outlines the choices you have available. For this example, you do not need any of these options.

9. You are finally finished with compiler options. I assume that you are not trying to insert assembly code in with the C code, so now we move directly to the linking phase. Choose the options you want to use from Table 22.7. For the example, you do not need any of these options.

# **Table 22.5** Commonly used optimization parameters available for gcc during the compilation phase.

| Option | Purpose | Value | Example |
| --- | --- | --- | --- |
| -O | Takes the extra time and compilation resources to optimize the code | None | -O |
| -O0 | Does not take the extra time and compilation resources to optimize the code | None | -O0 |
| -O2 | Optimizes the code more than would be done with just -O | None | -O2 |
| -O3 | Uses the highest level of optimization | None | -O3 |
| -Os | Optimizes for size instead of speed | None | -Os |