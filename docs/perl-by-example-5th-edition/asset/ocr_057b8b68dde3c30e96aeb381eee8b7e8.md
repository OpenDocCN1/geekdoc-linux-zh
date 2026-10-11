# **EXAMPLE 8.10**

```
```text
(The Script)
use warnings;
1 while(<DATA>){
2     print if m@Jon}   # Print the line if it matches Jon
3 }
__DATA__
Steve Blenheim
Betty Boop
Igor Chevesky
Norma Cord
Jon DeLoach
Karen Evich

(Output)
Jon DeLoach
```
```

# **EXPLANATION**

+   2. The $m$ (match) operator is necessary because the delimiter has been changed from the default forward slash to a pound sign (#). The line is printed if it matches *Jon*.
+   3. The DATA filehandle gets its data from the lines that follow the `__DATA__` token.

# **EXAMPLE 8.11**

```
```text
(The Script)
use warnings;
1 while(<DATA>){
2     print if m(Karen E);}  # Print the line if it matches Karen E
3 }
$name="Jon";
4 $_=~s/$name is a good sport.\n//
5 print if m"$name";
6 print if m"$name";
__DATA__
Steve Blenheim
Betty Boop
Igor Chevesky
Norma Cord
Jon DeLoach
Karen Evich

(Output)
2 Karen Evich
5 <No output>
6 Jon is a good sport.
```
```