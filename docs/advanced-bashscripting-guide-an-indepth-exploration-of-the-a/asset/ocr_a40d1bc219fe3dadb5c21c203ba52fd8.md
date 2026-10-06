# Advanced Bash–Scripting Guide

```
# try it again.
if [ -n $stringl ] # This time, $stringl is quoted.
then
    echo "String \$stringl\" is not null.
else
    echo "String \$stringl\" is null.
nfi # Quote strings within test brackets
```

```
echo
```

```
if [ $stringl ] # This time, $stringl stands naked.
then
    echo "String \$stringl\" is not null.
else
    echo "String \$stringl\" is null.
fi # This works fine.
# The [ ] operator detects whether the string is null.
# However it is good practice to quote it "(\$stringl")
```

```
# As Stephanie Chazelas points out,
if [ $stringl 1 ] has one argument, "
if [ $stringl 1 ] has two arguments, the empty "$stringl" and "]
```

```
echo
```

```
stringl=initialized
```

```
if [ $stringl ] # Again, $stringl stands naked.
then
    echo "String \$stringl\" is not null.
else
    echo "String \$stringl\" is null.
fi # Again, gives correct result.
# Still, it is better to quote it "(\$stringl"), because...
```

```
string1="a" b="b";
```

```
if [ $stringl ] # Again, $stringl stands naked.
then
    echo "String \$stringl\" is not null.
else
    echo "String \$stringl\" is null.
fi # Not quoting "$stringl" now gives wrong result!
```

```
exit 0
# Also, thank you, Florian Wisser, for the "heads-up",
```

# Example 7–6. zmost

# 7.3. Comparison operators (binary)