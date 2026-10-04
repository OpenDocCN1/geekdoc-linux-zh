# 14.2 Code Checkers

The tclparse program generates the following output from the script in Example 14.2.2-1:

# Example 14.2.3-1

```
1 proc upper_level () {
2   set_this_does_not_yet_exist
3   proc twoargs {a b} {
4
5   puts $a$b
6   }
7
8   expr 5+"a"
```

ERROR ( line 9 ) - wrong # args: should be 'proc name args body'

```
6
7   expr 5+"a"
8   expr (5+"a") {
9   proc foo {a} {
10    upvar $a x
11    set x 5
12  }
```

ERROR ( line 13 ) - unknown command 'foo'

```
10   upvar $a x
11   set x 5
12  }
13  foo
14  foo bar of this and that
15
16  proc foo {a} {
```