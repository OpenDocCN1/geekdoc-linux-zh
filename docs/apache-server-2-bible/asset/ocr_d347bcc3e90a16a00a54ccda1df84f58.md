All of these constructions are risky if they involve user input that may contain shell meta-characters. For `system()` and `exec()`, there’s a somewhat obscure syntactic feature that enables you to call external programs directly rather than going through a shell. If you pass the arguments to the external program as separate elements in a list rather than in one long string, Perl will not go through the shell and shell meta-characters will have no unwanted side effects. For example:

```
    system "/usr/bin/sort", "data.dat";
```

You can take advantage of this feature to open up a pipe without going through a shell. Calling the character sequence – | forks a copy of Perl and opens a pipe to the copy. Then, the child copy immediately forks another program using the first argument of the `exec` function call.

To read from a pipe without opening a shell, you can do something similar with the sequence –|:

```
    open(GREP, "-|" ) || exec "/usr/bin/grep",$userpattern,$filename;
    while (<&GREP>) {
        print "match: $_";
    }
    close GREP;
```

These forms of `open()` are more secure than the piped `open()` and, therefore, you should use these whenever possible.

Note that there are many other obscure features in Perl that enable you to call an external program and to lie to it about its name. This is useful for calling programs that behave differently depending on the name by which they were invoked. The syntax is:

```
    system $real_name "fake_name", "argument1", "argument2"
```

One trick used by vandals is to alter the `PATH` environment variable so that it points to the program they want your script to execute, rather than to the program you’re expecting. You should invoke programs using full pathnames rather than relying on the `PATH` environment variable. That is, instead of this fragment of Perl code:

```
    system("cat /tmp/shopping.cart.txt");
```

use this:

```
    system "/bin/cat" . "/tmp/shopping.cart.txt ";
```

If you must rely on the `PATH` variable, set it yourself at the beginning of your CGI script, as follows:

```
    $ENV{' PATH'}="bin:/usr/bin:/usr/local/bin";
```