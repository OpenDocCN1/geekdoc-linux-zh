Notice that this is the same result we would get from `head -n 5 states.txt`, we just used cat to illustrate how the pipe works. The general syntax of the pipe is `[program that produces output] | [program uses pipe output as input instead of a file]`.

A more common and useful example where we could use the pipe is answering the question: “How many US states end in a vowel?” We could use grep and regular expressions to list all of the state names that end with a vowel, then we could use wc to count all of the matching state names:

```
grep "[aeiou]$" states.txt | wc -l
```

## 32

The pipe can also be used multiple times in one command in order to take the output from one piped command and use it as the input to yet another program! For example we could use three pipes with ls, grep, and less so that we could scroll through the files in out current directory were created in February:

```
ls -al | grep "Feb" | less
```

```
-rw-r--r--  1 sean  staff  472 Feb 22 13:47 sta\\
tes.txt
```

Remember you can use the Q key to quit less and return to the prompt.