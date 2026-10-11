Table 19.13 **Flags used with** join **(continued)**.

| Flag | Purpose | Values |
| :--- | :--- | :--- |
| -a | Includes lines that cannot be joined from the specified file | Path to file |
| -e | When a field is empty but can be joined, enters the specified value in its place | Value |
| --help | Displays help information | None |
| -i | Ignores case when comparing fields | None |
| -l | Sorts data | None |
| -o | Builds output according to specified format | A comma- or space-separated list with one of two values: *file.field* or **0** |
| -t | Uses the specified character as a field separator | Character |
| -v | Does not print matching lines from the specified file | Path to file |
| --version | Displays version information | None |


# ## The ispell Spelling Checker

Many people rely on spelling checkers to help catch their mistakes. In Linux, you do not have to use a word processor in order to access this handy tool. You can use the **ispell** program and its associated scripts to spellcheck any text document. How exactly you use this tool depends on the context. These issues are addressed in the Immediate Solutions sections “Checking Spelling With **ispell**,“ “Building **ispell** Dictionaries,” and “Reducing **ispell** Dictionary Sizes.”

# ## The tr Text Transposer

Sometimes, you need to alter a file or data stream, but not in incredibly complex ways. A good tool to accomplish these jobs is **tr**. You use this command in the following format:

```
tr flags file(s)
```

The **flags** available with **tr** are listed in Table 19.14.

The values you use to determine a match come in more than one form. These forms can be mixed and matched where appropriate. One type of value available is a set of metacharacters in the format of a backslash and then a character. Each of these items represents a special function, such as the end of a line—a newline, or \n. Table 19.15 lists the metacharacters available with **tr**.