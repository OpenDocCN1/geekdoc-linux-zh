
## Chapter 10: Patterns, Expansions, and Substitutions 433

common problems in very natural way. Subpatterns are patterns that you wrap with parentheses and precede with one of five character codes:

- `!!(...) The subpattern must occur zero times. (Must not occur).
- `?(...) The subpattern must occur exactly zero or once.`
- `(...) The subpattern may occur zero or more times.`
- `@(...) The subpattern must occur exactly once.`
- `+(...) The subpattern must occur once or more times.`

You will see that patterns are used with variables as well as with file names later in this chapter, but for now we'll continue to work with file names. However, you will need some longer file names than the ones used above to get an idea of how subpatterns work.

So remove all the files in your Lab10.1 directory and run the following commands to create a set of file names to work with:

```bash
for prefix in re
  do for root in read
    do for suffix in ing
      do > $prefix$root$suffix
    done
done
```

![](img/694fa9f0320e707804a4c650b96a09b4_452_0.png)

The third do command could have used the touch command instead of output redirection to accomplish the same thing, as follows:

```bash
touch $prefix$root$suffix
```

The touch command is slower to run and takes more characters to but will not destroy the contents of a file if it already exists.

## a) How many files did these commands create?

## Lab 10.1: Patterns

Run the following two commands:

```bash
print !(un*)
print !(un)*
```

b) What printed, and why?

Run the following commands:

```bash
print ?(re)read*
print +(re)read*
print @(re)read*
print *(re)read*
```

c) What printed, and why?

## LAB 10.1 ANSWERS

![](img/694fa9f0320e707804a4c650b96a09b4_453_0.png)

This section gives you some suggested answers to the questions in Lab 10.1, with discussion related to those answers. Your answers may vary, but the most important thing is whether or not your answer works. Use this discussion to analyze differences between your answers and those presented here.

If you have alternative answers to the questions in this exercise, you are encouraged to post your answers and to discuss them at the companion web site for this book, located at:
http://www.phptr.com/phptrinteractive/

## Chapter 10: Patterns, Expansions, and Substitutions 435

## 10.1.1. ANSWERS

## LAB 10.1

a) What is the difference in output between the ls and the print commands?

Answer: Your interaction should look like the following:

```bash
[10000]: mkdir Lab10.1
[10001]: cd Lab10.1
[10002]: touch a b c d e a.b b c.c d d.e
[10003]: ls *
a a.b b b.c e c.d d d.e e
[10004]: print *
a a.b b c c d d d.e e
[10005]:
```

Only the number of spaces between the file names is different. The ls command spaces the file names so they will line up in columns if there are too many names to fit on one line, but the print command prints each of its parameters separated by a single space.

![](img/694fa9f0320e707804a4c650b96a09b4_454_0.png)

> Be sure you understand that the shell, not the commands, is processing the asterisks. In both commands, the shell is expanding the asterisk to be a list of file names that match the pattern, "zero or more characters." The ls command verifies that each of the parameters passed to it is really the name of a file, then prints its name. The print command prints whatever of its parameters are.

```bash
ls abc *
print abc *
```

b) What do these two commands print?

Answer: Your interaction should look like the following:

```bash
[10005]: ls abc *
abc: no such file or directory
a a.b b b.c c c.d d d.e e
[10006]: print abc *
abc a.b b b.c c d d d.e e
[10007]:
```

## 436 Lab 10.1: Patterns

## LAB 10.1

This interaction shows that ls looks at each of its parameters to make sure they exist.

c) What does the output of this command differ from the output of this?
Answer: Your interaction should look like the following:

```bash
[10007]: print *
a.b b b.c c c.d d d.e e
[10008]: ls *
a.b b c c d d.. e
```

The ls command spaces the file names so they will line up in columns if there are too many names to fit on one line, but the print command prints each of its parameters separated by a single space.

The ls command verifies that each of the parameters passed to it is really the name of a file, then prints its name. The print command prints whatever of its parameters are.

```bash
ls abc *
print abc *
```

d) What would print if the print command's message was not in quotes?
Answer: Your interaction should look like the following:

```bash
[10009]: print *
a.b b b.c c c.d d d.e e
```

e) What is the value of the first time through the loop?
Answer: Your interaction should look like the following:

```bash
[10010]: print *
a.b b b.c c c.d d d.e e
```

f) How many lines of output were there?
Answer: There are nine lines.

## Chapter 10: Patterns, Expansions, and Substitutions 437

The ls command spaces the file names so they will line up in columns if there are too many names to fit on one line, but the print command prints each of its parameters separated by a single space.

The ls command verifies that each of the parameters passed to it is really the name of a file, then prints its name. The print command prints whatever of its parameters are.

```bash
ls abc *
print abc *
```
