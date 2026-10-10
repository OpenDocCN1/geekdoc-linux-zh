This variable also provides a cool way of grabbing the last parameter on the command line without having to know how many parameters were used. However, you need to use a little trick to get there.

If you think this through, you might think that because the $# variable contains the value of the number of parameters, using the variable ${$#} would represent the last command-line parameter variable. Try that and see what happens:

```
```
$ cat badlastparamtest.sh
#!/bin/bash
# Testing grabbing the last parameter
#
echo The number of parameters is $#
echo The last parameter is ${$#}
exit
$ . /badlastparamtest.sh one two three four
The number of parameters is 4
The last parameter is 2648
$```

```

Obviously, something went wrong. It turns out that you can't use the dollar sign within the braces. Instead, you must replace the dollar sign with an exclamation mark. Odd, but it works:

```
```
$ cat goodlastparamtest.sh
#!/bin/bash
# Testing grabbing the last parameter
#
echo The number of parameters is $#
echo The last parameter is ${!}
exit
$ . /goodlastparamtest.sh one two three four
The number of parameters is 4
The last parameter is four
$ . /goodlastparamtest.sh
The number of parameters is 0
The last parameter is . /goodlastparamtest.sh
$```

```

Perfect. It's important to notice that, when there weren't any parameters on the command line, the $# value was 0, but the ${!#}