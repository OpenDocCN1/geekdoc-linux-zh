# Listing 8.3 Testing for Class Values

```
[root]# cat >> test.cf
ClassTest
R$+ @=w $@ Found it
R$+ @=w $@ Not in class w
R$* $: Wrong format
[root]# sendmail -bt -Ctest.cf
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enter <ruleset> <address>
>$w
robin.foobirds.org
other.org
wren.foobirds.org
[172.16.12.3]
patient-rights.com
autofbusiness.com
wren
localhost
weBroke.com
robin
thatplace.com
imaginary.com
> ClassTest christopher@robin
ClassTest input: christopher @ robin
ClassTest returns: Found it
> ClassTest sara@hawk
ClassTest input: sara @ hawk
ClassTest returns: Not in class w
> ClassTest craig
ClassTest input: craig
ClassTest returns: Wrong format
> ^D
```

In Listing 8.3, a command is used to append the ClassTest ruleset to the test.cf configuration file. Then the sendmail command runs with the -bt option and the modified test.cf configuration. The contents of class w are displayed. The values displayed for class vary from system to system. If you run this test on your own system, use values from your system's class w.

In Listing 8.3, three tests of the ClassTest ruleset are run. First, we send ClassTest the address Christopher@robin. The ruleset returns the value “Found it.” A quick glance at