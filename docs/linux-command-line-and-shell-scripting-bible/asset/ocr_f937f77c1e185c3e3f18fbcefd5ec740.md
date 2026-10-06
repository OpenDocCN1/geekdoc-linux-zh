# Part I The Linux Command Line

Without the single quotation marks, the bash shell assumes that the next character is another command to process. Notice that for the local environment variable I defined, I used lower-case letters, while the system environment variables we've seen so far have all used upper-case letters.

This is a standard convention in the bash shell. If you create new environment variables, it is recommended (but not required) that you use lower-case letters. This helps年纪 your personal environment variables from the scores of system environment variables.

> CAUTION It is extremely important that there are no spaces between the environment variable name, the equal sign, and the value. If you put any spaces in the assignment, the bash shell interprets the value as a separate command:

```
$ test2 = test
$bash: test2: command not found
$
```

Once you set a local environment variable, it's available for use anywhere within your shell process. However, if you spawn another shell, it's not available in the child shell:

```
$ bash
$ echo $test

$ exit
$ echo $test
testing a long string
$
```

In this example I started a child shell. As you can see, the test environment variable is not available in the child shell (it contains a blank value). After I exited the child shell and returned to the original shell, the local environment variable was still available.

Similarly, if you set a local environment variable in a child process, once you leave the process the local environment variable is no longer available:

```
$ bash
$ test-testing
$ echo $test
testing
$ exit
exit
$ echo $test
$
```

The test environment variable set in the child shell doesn't exist when I go back to the parent shell.