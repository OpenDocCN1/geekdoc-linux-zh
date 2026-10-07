# 480 Lab 10.3: Parameter Expansion

the value of SAMPLE. Remember, "any number of characters" can mean,
as in this case, "none.",

The pattern in line 1069 is /***/ which is the same as the previous one,
except that the shell is to match the longest matching sequence that it
can find. So, in this case the asterisk ( *) matches everything up to the
last slash ( / ), leaving just the characters following slash after the
deletion.

![](bbox=[0.015, 0.245, 0.178, 0.313])

> The command print ${SAMPLE##} behaves much like the UNIX
command $SAMPLE, provided that the value of SAMPLE is
valid pathname.

The pattern in line 1070 is /* which tells to "delete the shortest
sequence of characters that consist of a slash, followed by any number
of characters, ending at the end of the string." In this case, the shell deletes
t last slash and everything to the right of it.

> The command print ${SAMPLE%*} is much like the UNIX com-
ndir $SAMPLE provided that the value of SAMPLE is a valid
pathname.

![](bbox=[0.178, 0.533, 0.283, 0.623])

The pattern in line 1071 is %/*, which is the same as the previous one,
except that the shell is to match the longest matching sequence that it can
find. In this case, the slash is found at the beginning of the string and the
asterisk matches else, resulting in everything being deleted,
a a blank line prints.

+   g) Explain the outputs of the three print commands.
Answer:Your interaction should look like the following:

```
[1072]: integer i=( 99 88 77 66 55 )
[1073]: typeset -A a
[1074]: a[aa]=99 a[bb]=88 a[cc]=77 a[dd]=66 a[ee]=55
[1075]: set 99 88 77 66 55
[1076]: print $@ '$\n' ${@:1:2}
99 88 77 66 55
99 88
[1077]: print ${a[@]} '$\n' ${a[@]:1:2}
77 55 66 99
55 88
```

![](bbox=[0.178, 0.893, 0.283, 0.983])