```
```php
<TD ALIGN=LEFT><STRONG>Birth Date</STRONG></TD>
</TR>
";
for ($i = 1; $i <= $numresults; $i ++) {
    $row = mysql_fetch_array($result);
    echo "
        <TR VALIGN=TOP>
            <TD ALIGN=LEFT>$row[0]</TD>
            <TD ALIGN=LEFT>$row[1]</TD>
            <TD ALIGN=LEFT>$row[2]</TD>
            <TD ALIGN=LEFT>$row[3]</TD>
        </TR>
    ";
}
echo "</TABLE>";
} else {
    echo "No matches.";
}
?>
</BODY>
</HTML>
```
```

> **Note**
> 
> The line numbers in the previous file have been added for reference and are not part of the script.

This PHP file produces results similar to those shown in Figure 25.5.

**Figure 25.5**

Search results with PHP.

![](bbox=[0.269, 0.579, 0.812, 0.881])