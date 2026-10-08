# Advanced Bash-Scripting Guide

+   - done
- The ${!array[@]} operator, which expands to all the indices of a given array.

```
#!/bin/bash
Array=(element-zero element-one element-two element-three)
echo ${Array[0]}      # First element of array.
echo ${!Array[@]}     # 0 1 2 3
                      # All the indices of array.

for i in ${!Array[@]}
do
    echo ${Array[i]}      # element-zero
                         # element-one
                         # element-two
                         # element-three

                         # All the elements in array.
done
```

The =~ Regular Expression matching operator within a double brackets test expression. (Perl has a similar operator.)

```
#!/bin/bash
variable="This is a fine mess."
echo "$variable"

# Regex matching with =~ operator within [[ double brackets ]]
if [[ "$variable" =~ T........fines* ]];
# NOTE: As of version 3.2 of Bash, expression to match no longer works.
then
    echo "match found"
    # match found
fi
```

```
#!/bin/bash
input=$1

if [[ "$input" =~ "[0-9][0-9][0-9][0-9][0-9][0-9][0-9][0-9]" ]];
# NOTE: quoting not necessary, as of version 3.2 of Bash.
# NNN-NNNN (where each N is a digit).
then
    echo "Social Security number."
    # Process SSN.
else
    echo "Not a Social Security number!"
    # Or, ask for corrected input.
fi
```

Chapter 37. Bash, versions 2, 3, and 4

550