# 37.2.2. Bash, version 3.2

This is pretty much a bugfix update.

+   - global parameter substitutions, the pattern no longer anchors at the start of the string.
- --wordexp option enables process substitution.
- =~ Regular Expression match operator no longer requires quoting of the pattern within [...].

> In fact, quoting in this context is not advisable as it may cause regex evaluation to fail. Chet Ramesh states in the Bash FAQ that explicitly disables regex evaluation. Also see the Ubuntu Bug List and Wiknerds on Bash syntax.

Setting shop -s compatat3 in a script causes reversion to the original behavior.

# 37.3. Bash, version 4

Chet Ramesh announced Version 4 of Bash on the 20th of February, 2009. This release has a number of significant new features, well as some important bugfixes.

Among the new goodies:

+   - Associative arrays. [130]

> An associative array can be thought of as a set of two linked arrays -- one holding the data, and the other keys index the individual elements of the data array.

Example 37-5. A simple address database

```
#!/bin/bash4
# fetch_address.sh

declare -A address
# -Option declares associative array.

address[Charles]="414 10th Ave., Baltimore, MD 21236"
address[John]="202 3rd St., New York, NY 10009"
address[Wilma]="1854 Vermont Ave, Los Angeles, CA 90023"

echo "Chet's address is ${address[Charles]]}"
# Chet's address is 414 10th Ave., Baltimore, MD 21236
echo "Wilma's address is ${address[Wilma]}"
# Wilma's address is 1854 Vermont Ave, Los Angeles, CA 90023
echo "John's address is ${address[John]}"
# John's address is 202 3rd St., New York, NY 10009.

echo
echo "${!address[@]}" # The array indices ...
# Charles John Wilson
```

Chapter 37. Bash, versions 2, 3, and 4