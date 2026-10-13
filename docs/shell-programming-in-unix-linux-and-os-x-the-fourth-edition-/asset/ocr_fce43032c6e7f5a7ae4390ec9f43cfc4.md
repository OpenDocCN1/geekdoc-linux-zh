The technique of using echo in a pipeline to write data to the standard input of the subsequent command is simple but powerful, and is often used in shell programs.

The next example shows how cut can be used to extract the first character from the values stored in a variable called filename:

```
    $ filename=/users/steve/memos
    $ firstchar=$(echo $filename | cut -c1)
    $ echo $firstchar
    /
    $
```

sed is also often used to “edit” the value stored in a variable. Here it is used to extract the last character from each line of the file specified by the variable file:

```
    $ file=exec.o
    $ lastchar=$(echo $file | sed 's/.*\(.\)$/\1/')
    $ echo $lastchar
    o
    $
```

The sed command replaces all the characters on the line with the last one (remember that surrounding a pattern in parentheses causes it to be saved in a register[\e] in this case register 1, which is then referenced as \1). The result of the sed substitution is stored in the variable lastchar. The single quotes around the sed command are important because they prevent the shell from trying to interpret the backslashes. (Question: would double quotes also have worked?)

Finally, command substitutions can be nested. Suppose that you want to change every occurrence of the first character in a variable to something else. In a previous example, firstchar=$(echo $filename | cut -c1) gets the first character from filename, but how would we use this character to change every occurrence of that character in filename? A two-step process is one way:

```
    $ filename=/users/steve/memos
    $ firstchar=$(echo $filename | cut -c1)
    $ filename=$(echo $filename | tr "$firstchar" "^")    *translate to ^*
    $ echo $filename
    ^users^steve^memos
    $
```

But a single, nested command substitution can perform the same operation:

```
    $ filename=/users/steve/memos
    $ filename=$(echo $filename | tr "$(echo $filename | cut -c1)" "^")
    $ echo $filename
    ^users^steve^memos
    $
```

If you have trouble understanding this example, compare it to the previous one: Note how the firstchar variable in the earlier example is replaced by the nested command substitution; otherwise, the two examples are the same.