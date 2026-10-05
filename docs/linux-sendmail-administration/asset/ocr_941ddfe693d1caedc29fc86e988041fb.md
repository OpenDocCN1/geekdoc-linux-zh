# 186 Chapter 7 The sendmail.cf File

So if g contains kathy@foobirds.org and x contains Kathleen McCafferty, q will contain
kathy@foobirds.org (Kathleen McCafferty)

But if g contains sara@hawk.foobirds.org and x is empty, q will contain only
sara@hawk.foobirds.org.

$? is the test—“if” of the conditional. $. is “endif.” The conditional also has
else”, which is $1. The full syntax of the conditional is

```
$x value1 $| value2 $
```

is interpreted
if ($?) x set;

+   - usevalue1;
else ($);
usevalue2;
end (.).

This same syntax can be used in other sendmail.cf configuration com-
mands. We didn't see it in the D commands from our sample system, but we will see it later in the configuration file when we look at the H command.

All of the D commands shown in Listing 7.2 are found in the Local Info section of the
sendmail.cf file. Another command that is almost exclusively used in the Local Info sec-tion is the C command.

# The Define Class Command

A C command defines a sendmail class. A class is an array of values. Classes are used for
ings with multiple values that are handled in the same way, as such multiple namesor the local host or a list of domain names for which mail will be relayed. The C com-mand can define the values for a class variable on a single line or on multiple lines. For
t following line:

```
C{Accept}OK RELAY
```

performs the same function as these two lines:

```
C{Accept}0K
C{Accept}RELAY
```

The syntax of the C command is similar to that of the D command. The first character is
the command C. It is followed by the name of the class variable, which in turn is followed