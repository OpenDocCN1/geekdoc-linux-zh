
Based on the new contents of the `hello` file (`ls: cannot access 'nonexistent': No such file or directory`), what can you surmise about the function of `2>`? Here, `2` is a file descriptor for *standard error*.

# `Task 3:`

Sometimes, you want to redirect both output *and* error to the same place. In ye olden days, you would have to do something ugly like this: `ls foo > bar 2>&1`

However, modern versions of `Bash` have an easy-to-use shortcut: `ls foo && bar`

# `Task 4:`

We’ve talked about redirecting output, but what about input? To learn about that, run the following commands:

```
cat < hello
```

```
read foo <<< "foo"
echo $foo
```

```
cat << END-OF-FILE > goodbye
hello
goodbye
END-OF-FILE
cat goodbye
```

In short: `<` redirects input from a file name, `<<` starts a here document, and `<<<` redirects input from another command.

# `Task 5:`

Pipes (`|`) let you use the output of a command as the input to another command. In many situations (but not all), `|` and `<<<` are kind of a reverse of one another. For example, the output of...

```
echo "hello world" | grep e
```

... is identical to the output of...

```
grep e <<< "hello world"
```

Try to predict the output of the following command string before you run it (see `Answer 1` below):

```
grep non hello | cut -d: -f3
```
