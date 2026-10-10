```
8 -from 0 -to 255 -command setcolor -label Blue
9 button .ok -text OK -command printcolor
10 pack .swatch -expand 0 -fill x
11 pack .red .green .blue .ok

12 # Set the swatch color based on scales
13 proc setcolor { dummy } {
14 set r [.red get]
15 set g [.green get]
16 set b [.blue get]
17 set color [format "#%02x%02x%02x" $r $g $b]
18 .swatch configure -background $color
19 }
```

```
20 # Print color and exit
21 proc printcolor {} {
22 set r [.red get]
23 set g [.green get]
24 set b [.blue get]
25 set color [format "#%02x%02x%02x" $r $g $b]
26 puts $color
27 exit 0
28 }
```

Put this in a file called color.tcl and type

$ wish color.tcl

You should see a window that looks like Figure 33.2.

![](bbox=[0.1, 0.61, 0.78, 0.98])