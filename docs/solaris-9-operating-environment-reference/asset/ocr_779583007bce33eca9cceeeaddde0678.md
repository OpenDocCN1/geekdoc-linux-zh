# 342

# exstr

message retrieval function gettxt(). The msgfile and msgnum fields are used to construct the first argument to gettxt(). The second argument to gettxt() is printed if the message retrieval fails at runtime. This argument is the null string, unless you use the -d option.

The exstr command cannot replace strings in all instances. For example, a static initialized character string cannot be replaced by a function call. A second example is that a string could be in the form of an escape sequence that could not be translated. To not break code, you must examine the files created by invoking exstr and delete lines containing strings not replaceable by function calls. In some cases, the code may require modifications so that strings are extracted and replaced by calls to the message retrieval function.

# Options

Extract a list of strings from the named C-language source files, with positional information. This list is produced on standard output in the following format:

```
file:line:position:msgfile:msgnum:string
file The name of a C-language source file.
line Line number in the file.
position Character position in the line.
msgfile Null.
msgnum Null.
string The extracted text string.
```

Normally, you redirect this output into a file. Then, you edit this file to add the values you want to use for msgfile and msgnum

The file contains the text strings that replace string. A file with this name must be created and installed in the appropriate place by mkmsgs(1) command.

The next step is to use exstr -r to replace strings in file. 

Replace strings in a C-language source file with the message retrieval function gettxt().

Use with the -r option. If the message retrieval fails when gettxt() is invoked at runtime, the extracted string is printed. You use the capability provided by exstr on an application program that needs to run in an international environment and have messages print in more than one language. exstr replaces text strings with function calls that point at strings in a message database. The database depends on the runtime value of the LC_MESSAGES variable (see environ(5)).

# Examples

The following examples show use of exstr.