we’ll get this:

```
< html>
    <head>
        <title>Mispelled HTML file</title>
    </head>
    <body>
        <p>The quick brown fox jimped over the lazy dog.</p>
    </body>
</html>
```

+   1) HTML
+   2) ht ml
+   3) ht-ml
+   i) Ignore
+   r) Replace
+   a) Add
+   b) Abort
+   4) Hamel
+   5) Hamil
+   6) hotel
+   I) Ignore all
+   R) Replace all
+   l) Add Lower
+   x) Exit
+   ?

aspell will see the contents of the HTML tags as misspelled. This problem can be overcome by including the -H (HTML) checking-mode option, like this:

```
[me@linuxbox ~]$ aspell -H check foo.txt
```

which will result in this:

```
<html>
    <head>
        <title>Mispelled HTML file</title>
    </head>
    <body>
        <p>The quick brown fox jimped over the lazy dog.</p>
    </body>
</html>
```

+   1) Mi spelled
+   2) Mi-spelled
+   3) Misspelled
+   4) Disspelled
+   5) Spelled
+   i) Ignore
+   6) Misapplied
+   7) Miscalled
+   8) Respelled
+   9) Misspell
+   0) Misled
+   I) Ignore all