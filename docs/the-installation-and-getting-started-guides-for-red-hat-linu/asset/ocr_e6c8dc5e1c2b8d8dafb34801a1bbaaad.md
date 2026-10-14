# Using Redirection

Now that we have a handle on what standard input and standard output are, it's time to expand a little. Redirection means causing the shell to change what it considers standard input or where the standard output is going. We used cat before to demonstrate the idea behind standard input and standard output. Now, let's use cat to see how standard output can be redirected. To redirect standard output, we'll use the > symbol. Placing > after the cat command (or after any utility or application that writes to standard output) will direct its output to the filename following the symbol. Let's try it. In an xterm window type:

```
[billy@localhost billy] cat > sneakers.txt
buy some sneakers
then go to the coffee shop
then buy some
coffee
```

![](bbox=[0.11, 0.61, 0.93, 0.91])

Figure 16-12: Redirecting the output to a file