**6** Type `echo $?` and press **Enter**. Your screen looks similar to Figure 7-11.

![](bbox=[0.2, 0.15, 0.75, 0.52])

The test command returns an exit status of 0 indicating test_file is readable.

# Performing Boolean Tests with the test Command

The test command's Boolean operators let you combine multiple expressions with AND and OR relationships. You can also use a Boolean negation operator. Table 7-4 describes Boolean operators.

| Option | Meaning | Example |
| :--- | :--- | :--- |
| -a | Logical AND | test expression1 -a expression2 |
| -o | Logical OR | test expression1 -o expression2 |
| ! | Logical negation | test !expression |

Table 7-4: Test command's Boolean operators

The -a operator combines two expressions and tests a logical AND relationship between them. The form of the test command with the -a option is:

`test expression1 -a expression2`