```
C:11/02/97:toner:41.45
C:11/04/97:car payment:247.23
D:11/06/97:dividend:987.34
W:11/10/97:emergency cash:280
```

Your output should be similar to the following:

```
10/24/97    1000.00
10/25/97    980.00
10/30/97    878.57
10/30/97    867.23
11/02/97    825.78
11/04/97    478.55 * Below Min. Balance
11/06/97    1165.89
11/10/97    965.89
      Total    965.89
```

# Terms

**Field** A set of characters that are separated by one or more field separator characters. The default field separator characters are tab and space.

**Field Separator** Controls the manner in which an input line is broken into fields. In the shell, the field separator is stored in the variable IFS. In awk, the field separator is stored in the awk variable FS. Both the shell and awk use the default value of space and tab for the field separator.

![](bbox=[0.85, 0.48, 0.98, 0.65])