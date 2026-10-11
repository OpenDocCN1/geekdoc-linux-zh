For a more complex example, the following `sort` command sorts on the `account` number, in reverse order, and then by the `product` name. The sort is case insensitive and skips leading blanks:

```
```
$ head orders.txt | sort -t, -k4,4rn -k1,1fb
Bunk Bed,705.99,1,757
Cedar  Toy  Chest,65.99,1,757
Pine Round Table,375.99,1,757
Queen Bed,925.99,1,757
Reclining Chair,1599.99,1,757
Six-drawer Dresser,525.99,1,757
Birchwood China Hutch,475.99,1,756
Bookcase Oak Veneer,205.99,1,756
Small Bookcase Oak Veneer,205.99,1,756
Two-drawer Nightstand,125.99,1,756
```
```

For long sorts, the `-c` (*check only*) switch checks the files to make sure they need sorting before you attempt to sort them. This switch returns a status code of `0` if the files are sorted.

A complete list of `sort` switches appears in the reference section.

# ## Character Editing (`tr`)

The Linux `tr` (*translate*) command substitutes or deletes characters on standard input, writing the results to standard output.

The `-d` (*delete*) switch deletes a specific character.

```
```
$ printf "$a\n" 'The total is $234.45 US'
The total is $234.45 US
$ printf "$a\n" 'The total is $234.45 US' | tr -d '$'
The total is 234.45 US
```
```

Ranges of characters are represented as the first character, a minus sign, and the last character.

```
```
$ printf "$a\n" 'The total is $234.45 US' | tr -d 'A-Z'
The total is $234.45
```
```

`tr` supports GNU character classes.

```
```
$ printf "$a\n" 'The total is $234.45 US' | tr -d '[:upper:]'
The total is $234.45
```
```

Without any options, `tr` maps one set of characters to another. The first character in the first parameter is changed to the first character in the second parameter. The second character in the first parameter is changed to the second character in the second parameter. (And so on.)

```
```
$ printf "$a\n" "The cow jumped over the moon" | tr 'aeiou' 'AEIOU'
The cOw jUmPed OvEr tHe mOoN
```
```