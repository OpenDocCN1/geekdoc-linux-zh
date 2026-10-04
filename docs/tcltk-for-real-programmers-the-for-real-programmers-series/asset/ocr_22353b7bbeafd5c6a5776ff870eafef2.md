# 14.3 Debugging

```
set total [expr $total + $num]
)
  return $total
}
proc mean {lst} {
  set sum [addList $lst]
  set count [length $lst]
  set mean [expr $sum / $count]
  return $mean
}
```

```
set 1st [list 2 4 6 8]
puts "Mean $lst : [mean $lst]"
Debugging Session
$ expect
expect1.1> debug 1
0
expect1.2> source test.tcl
dbg1.1> b -g "*set count**" if {[length $lst] < 10} then puts "LIST: $lst"
0
dbg1.2> c
LIST: 2 4 6 8
3: set count [length $lst]
dbg3.4> w
0: expect
*1: mean {2 4 6 8}
3: set {count} {4}
dbg3.5> n 2
3: set mean [expr $sum / $count]
dbg3.6> w
0: expect
*1: mean {2 4 6 8}
3: set {mean} {5}
dbg3.7> c
Mean 2 4 6 8 : 5
```