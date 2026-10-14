This example named logic uses the file and directory mentioned in the previous compare3 example.

```
#!/bin/tcsh
if ( -x file1 && -x dir1 ) then
echo file1 and dir1 are executable
else
echo at least one of file1 or dir1 are not executable
endif
```

```
if ( -w file1 || ! -w dir1 ) then
echo file1 or dir1 are writable
else
echo neither file1 or dir1 are executable
endif
```

```
if ( ! -w file1 ) then
echo file1 is not writable
else
echo file1 is writable
endif
```

If you execute logic, it will yield the following result:

```
file1 and dir1 are executable
file1 or dir1 are writable
file1 is not writable
```

# The for Statement

The for statement is used to execute a set of commands once each time a specified condition is true. The for statement has a number of formats. The first format used by pdksh and bash is as follows:

```
for curvar in list
do
    statements
done
```

This form should be used if you want to execute statements once for each value in list. For each iteration, the current value of the list is assigned to curvar. list can be a variable containing a number of items or a list of values separated by spaces. The second format is as follows:

```
for curvar
do
    statements
done
```