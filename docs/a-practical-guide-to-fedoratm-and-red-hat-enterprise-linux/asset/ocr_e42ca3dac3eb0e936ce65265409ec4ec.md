![](bbox=[0.35, 0.08, 0.85, 0.62])

Figure 27-7 A case flowchart

# case

The case structure (Figure 27-7) is a multiple-branch decision mechanism. The path taken through the structure depends on a match or lack of a match between the *test-string* and one of the *patterns*. When the *test-string* matches one of the *patterns*, the shell transfers control to the *commands* following the *pattern*. The *commands* are terminated by a double semicolon (`;;`) control operator. When control reaches this control operator, the shell transfers control to the command following the esac statement. The case control structure has the following syntax:

```
```
case test-string in
    pattern-1)
        commands-1
    ;;
```
```