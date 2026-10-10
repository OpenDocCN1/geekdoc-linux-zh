| Name | Type | Default | Description |
|---|---|---|---|
| of | str | NULL | name of output filtering program |
| pc | num | 200 | price per foot or page in hundreds of cents |
| pl | num | 66 | page length (in lines) |
| pw | num | 132 | page width (in characters) |
| px | num | 0 | page width in pixels (horizontal) |
| py | num | 0 | page length in pixels (vertical) |
| rf | str | NULL | filter for printing FORTRAN style text files |
| rg | str | NULL | restricted group. Only members of group allowed access |
| rm | str | NULL | machine name for remote printer |
| rp | str | “lp” | remote printer name argument |
| rs | bool | false | restrict remote users to those with local accounts |
| rw | bool | false | open the printer device for reading and writing |
| sb | bool | false | short banner (one line only) |
| sc | bool | false | suppress multiple copies |
| sd | str | /var/spool/1pd | spool directory |
| sf | bool | false | suppress form feeds |
| sh | bool | false | suppress printing of burst page header |
| st | str | status | status file name |
| tf | str | NULL | troff data filter (cat phototypesetter) |
| tr | str | NULL | trailer string to print when queue empties |
| vf | str | NULL | raster image filter |