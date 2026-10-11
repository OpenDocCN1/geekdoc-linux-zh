It is possible for two items to generate the same hash value. This is called a *collision* and the item has to be stored in a different table position.

Like associative arrays, hash tables can be stored in Bash arrays, as shown in Listing 17.2.

# **Listing 17.2**  hash.sh

```
#!/bin/bash
# 
# hash.sh
# 
# Create a hash table and look up items
# 
# Ken O. Burtch
# CVS: $Header$
shopt -s -o nounset

declare -ax TABLE			# the hash table
declare -ix TABLE_SIZE=100	# size of the hash table
declare -rx SCRIPT=${0##*/}	# name of the script
declare -rx MD5SUM='/usr/bin/md5sum'	# used for hash generation

# hash_of: generate a table position from a string
#
function hash_of {
    declare HEXCODE			# 4 hex digits of MD5 signature
    declare -i CODE			# the hex digits in decimal

    HEXCODE=`echo "$1" | $MD5SUM`	# compute the hash value (hex)
    HEXCODE=${HEXCODE:0:4}		# take first 4 hex digits
    CODE=`printf '%d\n' 0x$HEXCODE`	# covert to 0...65535
    printf '%d\n' $((CODE%TABLE_SIZE))	# restrict to table size
}
readonly -f hash_of

# add_hash: add item to the hash table
#
function add_hash {
    declare -i ITEM=0			# current position in table

    # Empty strings are used for empty table positions

    if [ -z "$1" ] ; then
        printf '%s\n' "$SCRIPT: $FUNCNAME: Cannot add empty items" >&2
        return
    fi

    # Search for a free position
```