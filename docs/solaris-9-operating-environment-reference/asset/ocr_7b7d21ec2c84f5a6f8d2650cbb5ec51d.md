# hash, rehash, unhash, hashstat — Evaluate the Internal Hash Table of the Contents of Directories

# Synopsis

```
/usr/bin/hash [name]
/usr/bin/hash [- r]
```

sh
hash [- - r] [name...]

csh
rehash
unhash
hashstat

ksh
hash [name...]

# Description

Hashing is a method of indexing information by using an algorithm that generates an index of values indicating the ordered position of each item. For example, when the C shell starts, it finds all of the commands in directories specified by the path environment variable and builds an internal hash table of full path names. Then, when you execute a command, the C shell uses the hash table instead of searching directly for the path. This hashing technique is designed to improve performance. However, if you change your