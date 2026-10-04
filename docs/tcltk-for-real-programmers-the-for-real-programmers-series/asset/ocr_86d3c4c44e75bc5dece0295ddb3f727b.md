# 14.2 Code Checkers

+   - Both invocations of procedure foo are incorrect.
- The unset x in the second definition of foo tries to unset a variable that does not exist.
- The invocation of twoargs in the second definition of foo is incorrect.
- Incorrect usage of lappend.

# Example 14.2.2-1

```
Example Script
proc upper_level {} {
  set this_does_not_yet_exist
  proc twoargs {a b} {
    puts $a$b
  }

  expr 5+"a"
  expr (5+"a")
  proc foo {a} {
    upvar sa x
    set x 5
  }
  foo
  foo bar of this and that

  proc foo {a} {
    catch {unset x}
    list [twoargs 1 2 3 4]
  }
  catch {lappend}
}
```

```
tcl lint Output
In proc "foo":
file "has_bugs_1.tcl" line 33.
At or near: "catch {unset x}"

--- ERROR ---: unset or undeclared Variable "x".
file "has_bugs_1.tcl" line 33.
At or near: "unset x"
```