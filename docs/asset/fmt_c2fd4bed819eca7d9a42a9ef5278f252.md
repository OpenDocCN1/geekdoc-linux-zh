
```
load printers = yes

printing = cups

printcap name = cups
```

在 `[printers]` 部分，你应该会有类似下所示的内容：

```
[printers]

comment = All Printers

path = /var/spool/samba

browseable = no

public = yes

guest ok = yes

writeable = no

printable = yes

printer admin = root, @atndamba
```
