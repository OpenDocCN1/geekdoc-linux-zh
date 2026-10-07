# Chapter 7: Basic Tests 339

that the comment $ indicates that the name of the script is s712b, so that that should be the name of the executable file.

d) What does the -i option do?

Answer: It tells `grep` to ignore the case of the characters as it looks for lines containing the given pattern.

By using this option, you can have "January" in the Months file match "january" or "January" (or "January," or however the user utilizes it) over the command line.

e) What does ^ \$ around "$1" do?

Answer:They "anchor" the pattern so that it must occur as the only characters on a line.

The caret (^) says that the command line argument must appear at the beginning of a line, and the dollar sign says the argument must appear at the end of a line. If it has to be at both the beginning and the end of a line, it must be the only type on the line, which is the structure of the Months file you wrote Chapter 2, "Command Syntax." If you didn't provide this "anchoring" information, the user could type part of the name of a month, for example, "marc," and grep would match it to the line containing "."

![](bbox=[0.015, 0.565, 0.115, 0.635])

> Be careful when you make up the pattern part of a grep command; it's easy to get unintended results.

The version of `grep` that you may have not support the -w option to match "words" or allow you to include the pattern inside angle brackets (< and >) to indicate that you want to match words. Be sure to quote the brackets so the shell doesn't interpret them as redirection symbols. These word options are very useful for searching files with multiple words on a line.

f) Why is it necessary to put ^1\$ inside quotes in the grep command?

Answer:They prevent embedded spaces in variable $1 from "breaking" the script.

Imagine what happens if the user types this command:

```
s712b "January February",
```