Reclining Chair,_ . ' ' _
Bunk Bed, _ . ' ' _
Queen Bed, _ . ' ' _
Two-drawer Nightstand, _ . ' ' _
Cedar Toy Chest, _ . ' ' _
Six-drawer Dresser, _ . ' ' _
Pine Round Table, _ . ' '

The d (delete) command deletes a matching line. You can delete blank lines with the pattern '^\$' (that is, a blank line is the start of line, end of line, with nothing between).

```
$ head orders.txt | sed '1/$/d'
```

Without a pattern, you can delete particular lines by placing the line number before the d. For example, '1d' deletes the first line.

```
$ head orders.txt | sed '1d'
Bookcase Oak Veneer,205.99,1,756
Small Bookcase Oak Veneer,205.99,1,756
Reclining Chair,1599.99,1,757
Bunk Bed,705.99,1,757
Queen Bed,925.99,1,757
Two-drawer Nightstand,125.99,1,756
Cedar Toy Chest,65.99,1,757
Six-drawer Dresser,525.99,1,757
Pine Round Table,375.99,1,757
```

A d by itself deletes all lines.

There are several line-oriented commands. The a (append) command inserts new text after a matching line. The i (insert) command inserts text before a matching line. The c (change) command replaces a group of lines.

To insert the title DISCOUNTED ITEMS: prior to Cedar Toy Chest, you do this

```
$ head orders.txt | sed '/Cedar Toy Chest/i\
DISCOUNTED ITEMS:'
Birchwood China Rutch,475.99,1,756
Bookcase Oak Veneer,205.99,1,756
Small Bookcase Oak Veneer,205.99,1,756
Reclining Chair,1599.99,1,757
Bunk Bed,705.99,1,757
Queen Bed,925.99,1,757
Two-drawer Nightstand,125.99,1,756
DISCOUNTED ITEMS:
Cedar Toy Chest,65.99,1,757
Six-drawer Dresser,525.99,1,757
Pine Round Table,375.99,1,757
```

To replace Bunk Bed, Queen Bed, and Two-drawer Nightstand with an Items deleted message, you can use