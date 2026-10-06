# break and continue

You can interrupt a for, while, or until loop with a break or continue state-ment. The break statement transfers control to the statement after the done state-ment, terminating execution of the loop. The continue command transfers control to the done statement, which continues execution of the loop.

The following script demonstrates the use of these two statements. The for...in structure loops through the values 1-10. The first if executes the commands when the value of the index is less than or equal to 3 ($index -le 3). The second if executes the commands when the value of the index is greater than or equal to 8 ($index -ge 8). In between the two its, echo displays the value of the index. For all values up to and including 3, the first if displays and executes a continue statement that skips $index and the second if and continues with the next for. For the value of 8, the second if displays and executes a break that exits from the for loop. The echo built displays the values of index:

```
cat brk
for index in 1 2 3 4 5 6 7 8 9 10
do
    if [$index -le 3 ]; then
        echo "continue"
        continue
    fi
    #
    echo $index
    #
    if [$index -ge 8 ]; then
        echo "break"
        break
    fi
done

cat brk
continue
continue
continue
4
5
6
7
8
break
```

# case

Figure 13-7 shows the case structure, a multiple-branch decision mechanism. The path taken through the structure depends on a match or lack of a match between the test-string and one of the patterns.