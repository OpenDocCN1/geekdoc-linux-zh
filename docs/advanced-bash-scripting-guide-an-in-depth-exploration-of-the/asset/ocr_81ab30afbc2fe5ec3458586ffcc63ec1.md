# Advanced Bash-Scripting Guide

```
# Element 9: 1051224068   Last Access
# Element 10: 1051224068  Last Modify
# Element 11: 1051224068  Last Status
# Element 12: 0             UUID (to be)
# Element 13: 0             Volume Label (to be)
# Element 14: ef53            Filesystem type
}
```

And then were some test code

```
declare -a CUR_DIR
# For small arrays
ListDirectory "${PWD}" CUR_DIR
ListArray CUR_DIR
```

```
declare -a DIR_DIG
DigestFile CUR_DIR_DIG_IND
echo "The \name\" (checksum) for ${${CUR_DIR[9]} is ${DIR_DIG[0]}"
```

```
declare -a DIR_ENT
# BIG_DIR # For really big arrays - use a temporary file in ramdisk
# BIG_DIR # ListDirectory -of "${CUR_DIR[11]}"/* /tmp/junk2
ListDirectory "${CUR_DIR[11]}\/* DIR_ENT
```

```
declare -a DIR_IDX
# BIG_DIR # Indexlist -if "/tmp/junk2" DIR_IDX
ListIndex DIR_ENT_DIR_IND
```

```
declare -a IDX_DIG
# BIG_DIR # DIR_ENT-=$(cat /tmp/junk2)
# BIG_DIR # getfile -if "/tmp/junk2" IDX_DIG
DigestFile IDX_ENT_DIG_IND
# Small (should) be able to parallelize Indexlist & DigestFile
# Large (should) be able to parallelize Indexlist & DigestFile & the assignment
echo "The \name\" (checksum) for the contents of ${PWD} is ${${IDX_DIG[0]}"
```

```
declare -a FILE_LOC
LocateFile "${PWD}" FILE_LOC
ListArray FILE_LOC
```

exit 0
Stephane Chazelas demonstrates object-oriented programming in a Bash script.

Appendix A. Contributed Scripts