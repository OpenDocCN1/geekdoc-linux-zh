# Chapter 12. Writing a Tcl Extension

For more complex situations, the Tcl library includes functions that let you use a Tcl hash table to store key and value pairs. Your extension can allocate memory for a data structure, define a key to identify that structure, and then place a pointer to the structure in the hash table, to be accessed with the key. The key may be an alphanumeric string that can be returned to the Tcl script. When a Tcl script needs to access the data, it passes the key back to the extension code, which then retrieves the data from the hash table.

The Tcl hash table consists of a Tcl_HashTable structure that is allocated by your extension code and Tcl_HashEntry structures that are created as necessary to hold Key/Value pairs.

You must initialize the hash table before using it with the functions that access hash table entries. Once the table is initialized, your code can add, access, or delete items from the hash table.

```
Syntax: void Tcl_InitHashTable(tablePtr, keyType)
Tcl_InitHashTable
```

Initializes the hash table.

> Tcl_HashTable *tablePtr
A pointer to the Tcl_HashTable structure. The space for this structure must be allocated before calling Tcl_Init-HashTable.

int keyType A Tcl hash table can use one of three types of keys to access the data saved in the hash table. The acceptable values for keyType are:

```
TCL_STRING_KEYS
```

The hash table will use a NULL-terminated string as the key. This is the most commonly used type of hash key. The string representation of a Tcl_Obj object can be used as the key, which makes it simple to pass a value from a script to the Tcl hash table functions.