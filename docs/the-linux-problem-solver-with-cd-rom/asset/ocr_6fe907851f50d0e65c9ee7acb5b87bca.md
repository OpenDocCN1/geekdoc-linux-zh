While looking at scripts and examples on the system and in introductory books, you have probably noticed that they use an array of methods to get literal characters: single quotes, double quotes, and backslashes. Because there are so many ways to get literal characters, Unix shells sometimes cause utter confusion. Worse still, some shells have inconsistent schemes, and they're all somewhat incompatible. One factor in the choice of bash in this book is its relatively clean syntax.

To write effective scripts and commands, you need to understand how a shell parses its input and runs a command. When you type a command, you are specifying a number of arguments. Even the program you intend to run is an argument. After processing the arguments, the shell puts each argument into its own slot and runs a system call on all of the slots to execute the command. The argument slots' numbers start at zero in this system call—therefore, the actual first argument (in this case, the command), is often called the zeroth argument.

If you enter a command such as

```
$ echo "I'm a command" * $PATH
```

the zeroth argument is echo. The first argument is the string I'm a command (including the spaces). The rest of the arguments depend on the contents of the current working directory and what the environment variable PATH is set to.

When you type a command, your shell first parses quoted arguments and expands variables and patterns. Then it fills the argument slots with whatever the expansions yielded. Problems tend to occur when you forget that the shell expands some character in an argument before putting it into an argument slot.

Any * out on its own expands to a list of files in the current directory that do not begin with a dot (.) before the execution of the command. If the current directory holds no files, a literal * is passed as the argument; no error messages appear. This holds for all pattern matching. For example, foo* expands to all files in the current directory that start with foo except when none match, in which case it doesn't expand at all. This kind of expansion is known as globbing.

Any unquoted string beginning with $ expands to a shell or environment variable.

The confusion with quotes comes in when you want to prevent the shell from expanding special characters. There are three types of quotes: the double quote ("); the single quote (') or tick; and the back quote (`), or backtick. Their meanings are:

+   ' Literal. Anything inside single quotes does not expand; the shell passes it straight to the command.

+   " Somewhat literal. There is no globbing, so a character such as * is sent to the command, but shell and environment variables (beginning with $) are expanded.