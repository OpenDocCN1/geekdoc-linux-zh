# Chapter 5 Can I Quote You on That?

Note that in this particular example, it makes no difference whether the value assigned to address is enclosed in single quotes or double quotes. The shell displays the secondary command prompt in either case to indicate it's waiting for the corresponding close quote.

After assigning the two-line address to address, the value of the variable is displayed by echo. Without the variable quoted the address is displayed on a single line. The reason is the same as caused

```
echo one    two    three  four
```

to be displayed

Because the shell removes spaces, tabs, and newlines (whitespace characters) from the command line and cuts it up into arguments before giving it to the requested command, the invocation

```
echo $address
```

causes the shell to remove the embedded newline character

| |
|---|
| 39 |
| East |
| 12th |
| Street |
| New |
| York |
| N. |
| Y. |
| 10003 |

![](bbox=[0.119, 0.545, 0.365, 0.663])

Figure 5.5 echo $address

When the command

```
echo "$address"
```

is used instead, the shell substitutes the value of address as before, except that the double quotes tell it to leave any embedded whitespace characters alone. In this case, the shell passes a single argument to echo—an argument that contains an embedded newline. echo then displays its single argument. Figure 5.6 illustrates this, with the newline character depicted by the sequence \n.