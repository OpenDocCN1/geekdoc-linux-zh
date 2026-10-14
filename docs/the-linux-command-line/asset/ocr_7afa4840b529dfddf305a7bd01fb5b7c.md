I/O redirection allows us to change where output goes and where input comes from. Normally, output goes to the screen and input comes from the keyboard, but with I/O redirection, we can change that.

# Redirecting Standard Output

I/O redirection allows us to redefine where standard output goes. To redirect standard output to another file besides the screen, we use the “>” redirection operator followed by the name of the file. Why would we want to do this? It’s often useful to store the output of a command in a file. For example, we could tell the shell to send the output of the ls command to the file ls-output.txt instead of the screen:

```
[me@linuxbox ~]$ ls -l /usr/bin > ls-output.txt
```

Here, we created a long listing of the /usr/bin directory and sent the results to the file ls-output.txt. Let’s examine the redirected output of the command:

```
[me@linuxbox ~]$ ls -l ls-output.txt
-rw-rw-r-- 1 me me 167878 2008-02-01 15:07 ls-output.txt
```

Good; a nice, large, text file. If we look at the file with less, we will see that the file ls-output.txt does indeed contain the results from our ls command:

```
[me@linuxbox ~]$ less ls-output.txt
```

Now, let’s repeat our redirection test, but this time with a twist. We’ll change the name of the directory to one that does not exist:

```
[me@linuxbox ~]$ ls -l /bin/usr > ls-output.txt
ls: cannot access /bin/usr: No such file or directory
```

We received an error message. This makes sense since we specified the non-existent directory /bin/usr, but why was the error message displayed on the screen rather than being redirected to the file ls-output.txt? The answer is that the ls program does not send its error messages to standard output. Instead, like most well-written Unix programs, it sends its error messages to standard error. Since we only redirected standard output and not standard error, the error message was still sent to the screen. We’ll see