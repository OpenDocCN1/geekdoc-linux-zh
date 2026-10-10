Sometimes, you might be interested in only a certain part of a line in a file—just the first half of each line, for instance—or you might want to divide up each line at commas or tab characters and print out only the third field of each. You can use the `cut` command to cut only certain fields or parts thereof from a file for display. For example, suppose you have a text file named `phone.txt` that contains the following simple address book:

```
```
Doe, John-105 Some Street-Anytown-NY-55555-123-555-1212
Doe, Jane-105 Some Street-Anytown-NY-55555-123-555-1212
James, Joe-251 Any Street-Sometown-CA-51111-321-555-1212
```
```

If you only want to see five characters of each line, you can use `cut -c1-5 phone.txt`, in which the argument to `-c (1-5)` specifies a list of character positions, which in this case is characters 1 through 5. This results in the following:

```
```
$ cut -c1-5 phone.txt
Doe,
Doe,
James
```
```

A more useful application of `cut` is to cut only certain fields from a line with regular delimiters. The following command will return the first field from a set of lines delimited by tabs:

```
```
$ cut -f1 phone.txt
```
```

By default, `cut` expects fields to be separated with tab characters. However, you can change the field separator to any character you want. In this case, our address book text file doesn’t use tab characters as field separators—it uses tildes (~). We can specify which delimiter character we want to use with the `-d` option:

```
```
$ cut -f1 -d'~' phone.txt
Doe, John
Doe, Jane
James, Joe
```
```

Here, we have told `cut` to display only the first field, and we also told it that fields are delimited by tildes (~). Because the first tilde comes after the name, the command lists only the name of the person and leaves out the rest of the information.

Similarly, you can get a listing of all the users on your system by using `cut` on the `/etc/passwd` file:

```
```
$ cut -f1 -d':' /etc/passwd
frank
```
```