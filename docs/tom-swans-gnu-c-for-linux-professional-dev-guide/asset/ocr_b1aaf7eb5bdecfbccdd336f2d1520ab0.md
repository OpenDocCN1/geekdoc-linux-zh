Even though the preceding code lacks only one teensy character, when you compile the program with the following command, the compiler reports a "parse error" (the line number might be different for you):

```
$ g++ atest.cpp
atest.cpp: In function 'int main()':
atest.cpp:4: parse error before '}'
```

Parsing is part of the process the compiler undertakes to translate C++ source code into executable code. The compiler parses the program's text into a symbolic form suitable to the compiler's tastes. When the compiler finds a mistake in the text, it can't go on because it no longer "comprehends" the program's expression. Errors in parsing confuse the compiler the way a missing word in a sentence might confuse you. Of course, you might be able to figure out an incomplete sentence's meaning. But the compiler isn't so intuitive, and it must have a complete program, or it refuses to go on.

In this case, the compiler found a closing brace before it finished parsing a statement. Notice that the error message indicates that the error located at some place before the unexpected character. The compiler doesn't explain what the mistake is or its precise location, but only that it found an unexpected character. The source of the error might be many lines back from where the compiler became confused, and this can make finding the cause of parsing errors difficult.

Tip
If you have trouble locating the cause of a parsing error, comment-out preceding statements one at a time and recompile. When you can compile the program successfully, the error is in the last statement that you converted into a comment.

# WARNING AND ERROR OPTIONS

Although GNU C++ warns about most kinds of common problems, by specifying selected options, you can control how picky the compiler is about parsing a program's source code. Increasing the compiler's warning level this way might help you find and fix subtle bugs. The technique is also helpful if you are just learning C++, when, of course, you are apt to make more mistakes.

To increase the level of warnings issued, use the -Wall option. Despite the "all" in that option's name, you can add even more warnings by specifying -W. For a full load of all possible warnings, combine the two options with a command such as

```
$ g++ -Wall -W atest.cpp
```

Be careful to type capital W in both cases. The following command turns off all warnings:
$ g++ -w welcome.cpp // ???
Don't ever do that! It tells the compiler not to report any warnings, and this command could cause you to miss a serious bug.