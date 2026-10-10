![](bbox=[0.93, 0.135, 0.99, 0.265])

```
```
$ ./grabbingallparams.sh alpha beta charlie delta

Using the \$* method: alpha beta charlie delta
Using the \$@ method: alpha beta charlie delta

$ 
```
```

Notice that on the surface, both variables produce the same output, showing all the command-line parameters provided at once. The following example demonstrates where the differences are:

```
```
$ cat grabdisplayallparams.sh
#!/bin/bash
# Exploring different methods for grabbing all the parameters
#
echo
echo "Using the \$\* method: \$\*"
count=1
for param in "\$\*"
do
    echo "\$\* Parameter #\$count = \$param"
    count=\$\{ \$count + 1 \}
done
#
echo
echo "Using the \$\$ method: \$\$"
count=1
for param in "\$\$"
do
    echo "\$\$ Parameter #\$count = \$param"
    count=\$\{ \$count + 1 \}
done
echo
exit
```

$ ./grabdisplayallparams.sh alpha beta charlie delta

Using the \$\* method: alpha beta charlie delta
\$\* Parameter #1 = alpha beta charlie delta

Using the \$\$ method: alpha beta charlie delta
\$\$ Parameter #1 = alpha
\$\$ Parameter #2 = beta
\$\$ Parameter #3 = charlie
\$\$ Parameter #4 = delta

$
```