
```
cp states.txt states_copy.txt
```

To compute the MD5 hash of a file we can use the md5 command:

```
md5 states.txt
```

```
## MD5 (states.txt) = 8d7dd71ff51614e69339b03bd1cb86ac
```

```
md5 states_copy.txt
```

```
## MD5 (states_copy.txt) = 8d7dd71ff51614e69339b03bd1cb86ac
```

As we expected they’re the same! We can compute the SHA-1 hash using the shasum command:

```
shasum states.txt
```

```
## 588e9de7ffa97268b2448927df41760abd3369a9  states.txt
```

```
shasum states_copy.txt
```

```
## 588e9de7ffa97268b2448927df41760abd3369a9  states_copy.txt
```

Once again, both copies produce the same hash. Let’s make a change to one of the files, just to illustrate the fact that the hash changes if file contents are different:

```
head -n 5 states_copy.txt > states_copy.txt
shasum states_copy.txt
```

```
## b1c1c805f123f31795c77f78dd15c9f7ac5732d4  states_copy.txt
```

## Summary

- The md5 and shasum commands use different algorithms to create codes (called hashes or checksums) that are unique to the contents of a file.
- These hashes can be used to ensure that a file is genuine.

## Pipes

One of the most powerful features of the command line is skilled use of the pipe (|) which you can usually find above the backslash (\ ) on your keyboard. The pipe allows us to take the output of a command, which would normally be printed to the console, and use it as the input to another command. It’s like fitting an actual pipe between the end of one program and connecting it to the top of another program! Let’s take a look at a basic example. We know the cat command takes the contents of a text file and prints it to the console:

```
cd ~/Documents
cat canada.txt
```

```
## Nunavut
## Quebec
## Northwest Territories
## Ontario
## British Columbia
## Alberta
## Saskatchewan
## Manitoba
## Yukon
## Newfoundland and Labrador
## New Brunswick
## Nova Scotia
## Prince Edward Island
```

This output from cat canada.txt will go into our pipe, and we’ll attach the dispensing end of the pipe to head, which we use to look at the first few lines of a file:

```
cat canada.txt | head -n 5
```

```
Nunavut
Quebec
Northwest Territories
Ontario
British Columbia
```

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
-rw-r--r--  1 sean  staff  472 Feb 22 13:47 states.txt
```

Remember you can use the Q key to quit less and return to the prompt.

## Summary

- The pipe (`|`) takes the output of the program on its left side and directs the output to be the input for the program on its right side.

## Exercises

- 1. Use pipes to figure out how many US states contain the word “New.”
- 2. Examine your `~/.bash_history` to try to figure out how many unique commands you’ve ever used. (You may need to look up how to use the `uniq` and `sort` commands).

## Make

Once upon a time there were no web browsers, file browsers, start menus, or search bars. When somebody booted up a computer all they got was a shell prompt, and all of the work they did started from that prompt. Back then people still loved to share software, but there was always the problem of how software should be installed. The make program is the best attempt at solving this problem, and make’s elegance has carried it so far that it is still in wide use today. The guiding design goal of make is that in order to install some new piece of software one would:

- 1. Download all of the files required for installation into a directory.
- 2. `cd` into that directory.
