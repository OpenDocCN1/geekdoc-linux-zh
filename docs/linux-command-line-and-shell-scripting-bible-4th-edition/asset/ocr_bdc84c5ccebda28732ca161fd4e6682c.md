```
$ sed -n '{
> 1N
> N
> s// /g
> s/\\t/\\/g
> s/\\n/\\a/g
> p
> s/\\a/\\n/
> D}
> ' ScriptDataB.txt
Line1Line2Line3
Line2Line3Line4
Line3Line4Line5
Line4Line5Line6
Line5Line6Line3
Line6Line3Line4
Line3Line4Line5
Line4Line5Line7
Line5Line7Line8
Line7Line8Line3
Line8Line3Line4
Line3Line4Line5
Line4Line5Line9
Line5Line9Line10
Line9Line10Line11
Line10Line11Line12
$
```

Now we'll employ two other Bash shell commands to help us sort the file (sort) and find any duplicates (uniq -d):

```
$ sed -n '{
> 1N;
> N;
> s// /g;
> s/\\t/\\/g;
> s/\\n/\\a/g;
> p
> s/\\a/\\n/;
> D}
> ' ScriptDataB.txt |
> sort | uniq -d |
> sed 's/\\a/\\n/g'
Line3
Line4
Line5
$
```