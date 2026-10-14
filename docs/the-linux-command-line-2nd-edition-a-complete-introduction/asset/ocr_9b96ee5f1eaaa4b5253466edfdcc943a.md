```
```html
<TITLE>$TITLE</TITLE>
</HEAD>
<BODY>
    <H1>$TITLE</H1>
    <P>$TIMESTAMP</P>
    $(report_uptime)
    $(report_disk_space)
    $(report_home_space)
</BODY>
</HTML>
_EOF_
```
```

We could create these additional commands two ways. We could write three separate scripts and place them in a directory listed in our PATH, or we could embed the scripts within our program as *shell functions*. As we have mentioned before, shell functions are “mini-scripts” that are located inside other scripts and can act as autonomous programs. Shell functions have two syntactic forms:

```
```text
function *name* {
    *commands*
    return
}
```
```

and

```
```text
*name* () {
    *commands*
    return
}
```
```

where *name* is the name of the function and *commands* is a series of commands contained within the function. Both forms are equivalent and may be used interchangeably. Below we see a script that demonstrates the use of a shell function:

```
```bash
 1  #!/bin/bash
 2
 3  # Shell function demo
 4
 5  function funct {
 6      echo "Step 2"
 7      return
 8  }
 9
10  # Main program starts here
11
12  echo "Step 1"
```
```