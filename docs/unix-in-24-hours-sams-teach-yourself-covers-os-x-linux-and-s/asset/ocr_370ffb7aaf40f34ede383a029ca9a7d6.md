```
$ !awk &
awk -F: '{print $1" = "$5}' </etc/passwd | awk -F, '{print $1}'
→ | awk '{ if (NF > 2) print $0 }' | sort > ! who.is.who &
[1] 27556 27557 27558 27559
$
```