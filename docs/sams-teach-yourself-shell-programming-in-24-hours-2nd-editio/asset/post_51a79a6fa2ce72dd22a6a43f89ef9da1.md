
only for actions that contain more than one statement, but most programmers include them for the sake of clarity and maintainability.

As an example, you can rewrite the while loop in the previous example using a do loop:

```
#!/bin/sh
awk '{
x=NF;
do {
printf("%ld\t%s", $x);
x-=1;
} while(x>0);
print "";
}' fruit_prices.txt
```

![](img/3def70414996f811615f713b2077a154_302_0.png)

> The behavior of the do statement varies among nawk, gawk, and awk. If you want to use the statement, you should stick to nawk or gawk because older versions of awk might have trouble with it. If you are concerned with portability to older versions of UNIX, you should avoid using the do statement.

## The for Statement

The for statement enables you to repeat commands a certain number of times. The for loop in awk is similar to the for loop in the C language. The for loop has a counter that is initialized before the loop starts executing. At the beginning of every iteration, the value of the counter is compared to a predefined value. The loop executes when the comparison is true. If the comparison is false, the loop terminates. Every time the loop executes, the counter is incremented. This is quite different from the for loop in the shell, which executes a set of commands for each item in a list.

The basic syntax of the for loop is

```
for (init_entr; test_entr; incr_entr) {
    action
}
```

Here init_entr initializes the counter variable, test_entr is an expression that tests the counter variable's value, and incr_entr increments the value of the counter. The parentheses surrounding the expression used by the for loop are required. The actions that should be performed, action, are any sequence of valid awk commands. The braces surrounding the action are required only for actions that contain more than one statement, but most programmers always include them for the sake of clarity and maintainability.

A common use of the for loop is to iterate through the fields in a record and output them, possibly modifying each record in the process. The following for loop prints each field in a record separated by two spaces:

```
#!/bin/sh
awk '{
  for (x=1;x<=NF;x++) {
    printf "%s  ",$x ;
  }
  printf "\n";
}' fruit_prices.txt
```

## Summary

This chapter introduced awk programming. awk is one of the most powerful text-filtering tools available in UNIX. By using awk, it is possible to modify and transform text in ways that are difficult or impossible using only the shell.

Some of the important topics covered in this chapter include:

- Field editing
- Pattern specific actions
- Using STDIN as input
- Variables
- Numeric and assignment expressions
- Using flow control

In addition to these topics, awk offers features such as multiple-line editing, arrays, and functions. If you are interested in learning more about these topics, consult one of the following sources:

*The UNIX Programming Environment* by Brian Kernighan and Rob Pike (Prentice-Hall, 1984)

*The AWK Programming Language* by Alfred Aho, Peter Weinberger, and Brian Kernighan (Addison-Wesley, 1984)

*Effective AWK Programming* by Arnold Robbins and Michael Brennan (O'Reilly & Associates, 2001)

*sed & awk* by Arnold Robbins and Dale Dougherty (O'Reilly & Associates, 1997)

*The GNU awk User's Guide* by Arnold Robbins (SCC, 1996)

## Questions

1. Using the for statement, write an awk script that prints each of the fields in a record in reverse order.

2. Write an awk script that balances a checking account. Your program needs to print the balance in the account every time the user makes a transaction.

The transactions are stored in a file. Each line or record in the file has the following format:

```
command:date:comment:amount
```

Here date is the date on which the transaction was made, comment is a string (including embedded spaces) describing the transaction, and amount is the amount of the transaction. The command determines what should be done to the balance with amount. The valid commands are

- B indicates balance. When this command is encountered, the balance in the account should be set to the transaction amount.
- D indicates a deposit. When this command is encountered, the transaction amount should be added to the balance.
- C indicates a check. When this command is encountered, the transaction amount should be subtracted from the balance.
- W indicates a withdrawal. When this command is encountered, the transaction amount should be subtracted from the balance.

The main difference between the C (check) and the W (withdrawal) commands is that the C (check) command adds an extra field to its records:

```
command:date:comment:number:amount
```

In addition, the B (balance) command uses only two fields:

```
B:amount
```

Here amount is the balance amount in the account.

For the purposes of this problem, you need to be concerned with the first field, which contains the command; the second field, which contains the transaction date; and the last field, which contains the transaction amount.

The sample input file looks like the following:

```
$ cat account.txt
B:0
D:10/24/97:initial deposit:1000
C:10/25/97:credit card:101:100
W:10/30/97:gas:21.43
W:10/30/97:lunch:11.34
C:11/02/97:toner:41.45
C:11/04/97:car payment:347.23
D:11/06/97:dividend:87.34
W:11/10/97:emergency cash:200
```

Your output should look like the following:

```
10/24/97 1000.00
10/25/97 900.00
10/30/97 878.57
10/30/97 867.23
11/02/97 825.78
11/04/97 478.55
11/06/97 1165.89
11/10/97 965.89
```

## 3. Modify the program you wrote for question 2, to print the ending (total) balance after all input records have been considered. Your output should now look like the following:

```
10/24/97 1000.00
10/25/97 900.00
10/30/97 878.57
10/30/97 867.23
11/02/97 825.78
11/04/97 478.55
11/06/97 1165.89
11/10/97 965.89
Total 965.89
```

(HINT: Use the END pattern)

## 4. Modify the program you wrote in question 3 to support a new command:

- M indicates the minimum balance. When the balance drops below this minimum balance, a warning should be printed at the end of the output line.

The M (minimum balance) command uses only two fields:

```
M:amount
```

Here amount is the balance amount in the account.

The input file changes as follows:

```
$ cat account.txt
B:0
M:500
D:10/24/97:initial deposit:1000
C:10/25/97:credit card:101.00
W:10/30/97:gas:21.43
W:10/30/97:lunch:11.34
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

## Terms

**Field** A set of characters that are separated by one or more field separator characters. The default field separator characters are tab and space.

**Field Separator** Controls the manner in which an input line is broken into fields. In the shell, the field separator is stored in the variable IFS. In awk, the field separator is stored in the awk variable FS. Both the shell and awk use the default value of space and tab for the field separator.

![](img/3def70414996f811615f713b2077a154_306_0.png)

![](img/3def70414996f811615f713b2077a154_308_0.png)

## Hour 18

## Other Tools

In this chapter, you will look at several useful UNIX commands that are often encountered in shell scripts and that you can use in your own programs. The specific set of commands covered in this chapter includes:

- `eval`
- `:`
- `type`
- `sleep`
- `find`
- `xargs`
- `bc`
- `expr`

## The Built-In Commands

The first set of commands examined in this chapter are built-in commands. A built-in command is part of the shell itself; it is not stored in a separate file on disk. Built-in commands are slightly more efficient than external
