# Advanced Bash-Scripting Guide

Example 37-6. A somewhat elaborate address database

```
#!/bin/bash4
# fetch_address-2.sh
# A more elaborate version of fetch_address.sh

SUCCESS=0
E_DB=99 # Error code for missing entry.

declare -A address
# -Velma option declares associative array.

store_address () {
  address[$1]="$2"
  return $?
}

fetch_address () {
  if [[ -z "${address[$1]}\ ]]; then
    echo "$1's address is not in database."
    return $E_DB
  fi

  echo "$1's address is ${address[$1]}"
  return $?
}
```

store_address "Lucas Fayne "414 13th Ave., Baltimore, MD 21236"
store_address "Arvid Boyce "202 E. 3rd St., New York, NY 10009"
store_address "Velma Winston "1854 Vermont Ave, Los Angeles, CA 90023"
# Execution.
# Rewrite the above store_address calls to read data from a file,
# then assign field 1 to name, field 2 to address in the array.
# Each line in the file would have a format corresponding to the above.
# Use a use-read loop to read from file, sed or awk to parse the fields.

```
fetch_address "Lucas Fayne"
# Lucas Fayne's address is 414 13th Ave., Baltimore, MD 21236.
fetch_address "Velma Winston"
# Velma Winston's address is 1854 Vermont Ave, Los Angeles, CA 90023
fetch_address "Arvid Boyce"
# Arvid Boyce's address is 202 E. 3rd St., New York, NY 10009.
fetch_address "Bozo Bozeman"
# Bozo Bozeman's address is not in database.
```

exit $ # In this case, exit code = 99, since that is function returns.
See Example A-53 for interesting usage of an associative array.

> Elements of the index array may include space characters, or even leading and/or trailing characters. However, index array elements containing only whitespace are not permitted.

```
address[="Blank"] = # Error!
```

37. Bash, versions 2, 3, and 4

553