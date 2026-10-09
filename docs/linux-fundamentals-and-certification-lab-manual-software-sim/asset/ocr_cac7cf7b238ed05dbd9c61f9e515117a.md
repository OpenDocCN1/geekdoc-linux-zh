The file list

```
-rw-rw-r-- 1 dngle dngle 0 Sep 15 15:59 mydocument
```

indicates that mydocument has read/write permissions for the owner and the group and read permission for everyone else. To change the owner permissions to read/write/execute, the execute permission would have to be added. To make the change using symbolic mode, type the command u+x mydocument.

The u indicates the user or owner of the file, the plus (+) indicates to add the following permission, and the x indicates the execute permission. The results of an ls -l command after the change would be

```
-rw-rwxr-x-- 1 dngle dngle 0 Sep 15 15:59 mydocument
```

indicating that the owner permissions have changed.

The octal mode is based on the base eight number system, as the name implies. In base eight there are only eight symbols, 0 through 7.

Base eight numbers can be expressed in three binary numbers. Binary is the base two number system. Binary is used by all computer systems to process information. An example of a binary number is 101. This number represents the number 5 in octal. Following from right to left, the rightmost number is in the ones column and has the value of 1. The middle number is in the two's column and has a value of 0. The leftmost number is in the fours column and has the value of 4. In this case the values 1 + 0 + 4 give the octal value 5. All of the base eight symbols, as stated earlier, can be expressed in three binary values. Table 4-3 associates octal values with the full range of available permissions. Notice that a zero (0) in the binary position of the octal value translates to a dash (-) in the permission.

# Table 4-3

Permission values.

| Binary Value | Octal Value | Permissions |
| --- | --- | --- |
| 000 | 0 | --- |
| 001 | 1 | --x |
| 010 | 2 | -w- |
| 011 | 3 | -wx |
| 100 | 4 | r-- |
| 101 | 5 | r-x |
| 110 | 6 | rw- |
| 111 | 7 | rwx |

Notice the relationship between the rwx combination and the binary ones in the same positions. For the last octal value 7 the binary value is 111 and indicates that the r, w, and x are all to be set.

To set permissions for the owner, group, and others, use three sets of octal numbers to indicate the permissions desired. For example, to express the permissions rwxr-xr-x the octal value 755 would be used—7 for the first group (rwx), 5 for the second group (r-x), and 5 for the third group (r-x).

To use chmod with octal mode to change the following expression from owner read/write, group read/execute, and others read to owner read/write/execute, group read/write, and others read, use chmod 764 mydocument.

```
-rw-rw-r-- 1 dngle dngle 0 Sep 15 15:59 mydocument
```

The 7 represents rwx, the 6 represents rw-, and the 4 represents r--. A subsequent listing with ls -l would display

```
-rw-rw-r-- 1 dngle dngle 0 Sep 15 15:59 mydocument
```