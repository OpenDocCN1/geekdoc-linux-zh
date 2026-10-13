```
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

# 3. Modify the program you wrote for question 2, to print the ending (total) balance after all input records have been considered. Your output should now look like the following:

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

# 4. Modify the program you wrote in question 3 to support a new command:

+   M indicates the minimum balance. When the balance drops below this minimum balance, a warning should be printed at the end of the output line.

The M (minimum balance) command uses only two fields:

```
M:amount
```

Here amount is the balance amount in the account.

The input file changes as follows:

```
$ cat account.txt h
$0.0
M:500
D:10/24/97:initial deposit:1000
C:10/25/97:credit card:101.00
W:10/30/97:gas:21.43
W:10/30/97:lunch:11.34
```