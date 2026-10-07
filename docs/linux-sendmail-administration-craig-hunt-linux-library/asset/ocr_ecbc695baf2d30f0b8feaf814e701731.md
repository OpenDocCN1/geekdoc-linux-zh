So g contains kathy@foobirds.org and x contains Kathleen McCafferty, q will contain

kathy@foobirds.org (Kathleen McCafferty)

But g contains sara@hawk.foobirds.org and x is empty, q will contain only

sara@hawk.foobirds.org.

$? is the test—“if” of the conditional. $. is the “endif.” The conditional also has

“else,” which is $|$. The full syntax of the conditional is

```
$x value1 $|$ value2 $
```

which is interpreted as

```
if ($?) x is set;
```

```
use value1;
```

```
else ($);
```

```
use value2;
```

```
end if ($).
```

This conditional syntax can be used in other sendmail.cf configuration commands. We didn't see it in the D commands from our sample system, but we will see it later
in the configuration file when we look at the H command.

All of the D commands shown in Listing 7.2 are found in the Local Info section of the
sendmail.cf file. Another command that is almost exclusively used in the Local Info section is the D command.

# The Define Class Command

A C command defines a Sendmail class. A class is an array of values. Classes are used for
anything with multiple values that are handled in the same way, such as multiple names
it the local host or a list of domain names for which mail will be relayed. The command can define the values for a class variable on a single line or on multiple lines.
example, the following:

```
C(Accept)OK RELAY
```

performs the same function as these two lines:

```
C(Accept)OK
```

```
C(Accept)RELAY
```

The syntax of the C command is similar to that of the D command. The first character is
t command C. It is followed by the name of the class variable, which in turn is followed