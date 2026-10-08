Two adjacent double percent signs (%%) separate each section of the grammar file. To make the file easier to read, put the %% on a line by themselves. A complete grammar file has the following structure.

```
declarations
%%
rules
%%
programs
```

The declarations section can be empty. If you omit the programs section, also omit the second set of %%. The smallest yacc grammar file has the following structure.

```
%%
rules
```

yacc ignores blanks, Tabs, and new characters in the grammar files. You can use these characters to make the file easier to read. You should not, however, use blanks, Tabs, or newlines in names or reserved symbols.

yacc uses the information in the grammar file to generate a parser that controls the input process. The parser calls an input subroutine (the lexical analyzer) to pick up the tokens from the input stream. The parser organizes the tokens, using the structure rules from the grammar file. When the parser recognizes one of the grammar rules, it executes the action from the user code supplied for that rule. Actions return values and use the values returned by other actions.

> Note — Because file names are fixed, only one yacc process can be active in a given directory at a given time.

# Options

+   - file-prefix file-prefixinstead y as the prefix for all output files. The y.tab.c code file, the y.tab.h header file (created when you specify -d), and the y.output description file (created when you specify -v) are changed to file-prefix.tab.c, file-prefix.tab.h, and file-prefix.output.

+   -d Generate the y.tab.h file with the #define statements that associate the yacc user-assigned token codes with the user-declared token names. This association enables source files other than y.tab.c to access the token codes.

+   -l Specify that the code produced in y.tab.c does not contain any #line constructs. Use this option only to fully debug the grammar and the associated actions.

+   -P parser Specify the parser of your choice instead of /usr/ccs/bin/yaccpar. For example, you can specify:

```
castle% yacc -P ~/myparser parser.y
```