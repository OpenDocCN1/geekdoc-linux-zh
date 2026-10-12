```
```
C:\MyScripts>python unicode.py

Red String: Röd
Type: <class 'str'>       Length: 3

Encoded String: b'R\xc3\xb6d'
Type: <class 'bytes'>     Length: 4

Decoded String: Röd
Type: <class 'str'>       Length: 3
R : LATIN CAPITAL LETTER R
ö : LATIN SMALL LETTER O WITH DIAERESIS
d : LATIN SMALL LETTER D

Green String: Grön
Green String: Grön
C:\MyScripts>
```
```

![](bbox=[0.12, 0.37, 0.23, 0.44])

A string containing byte addresses must be immediately prefixed by a **b** to denote that string as a byte literal.

![](bbox=[0.12, 0.53, 0.23, 0.6])

Unicode names are uppercase and referenced by inclusion between `{ }` braces prefixed by a `\N` in this notation format.