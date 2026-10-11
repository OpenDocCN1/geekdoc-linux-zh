
## The -ne (not equal to) operator

let Salary=3000 tells the computer to create a variable by the name of Salary and to assign the value 3000.

let NewSalary=2000 tells the computer to create a variable by the name of NewSalary and to assign that variable the value 2000.

test $Salary -ne $NewSalary tells the computer to test to determine whether the value of the Salary variable is not equal to the value of the NewSalary variable. If not, test returns a true value; otherwise test returns a false value. Finally, echo "$?" displays the value that test returns.

## The -gt (greater than) operator

To determine whether the value of the first variable is greater than the value of the second variable, you use the -gt operator, as in the following example:

```
let Salary=3000
let NewSalary=2000
test $Salary -gt $NewSalary
echo " $?"
```

let Salary=3000 tells the computer to create a variable by the name of Salary and to assign the value 3000.

let NewSalary=2000 tells the computer to create a variable by the name of NewSalary and to assign that variable the value 2000.

test $Salary -gt $NewSalary tells the computer to test to determine whether the value of the Salary variable is greater than the value of the NewSalary variable. If so, test returns a true value; otherwise, test returns a false value. Finally, echo "$?" displays the value that test returns.

## The -ge (greater than or equal to) operator

To determine whether the value of the first variable is greater than or equal to the value of the second variable, you use the -ge operator, as in the following example:

```
let Salary=3000
let NewSalary=2000
test $Salary -ge $NewSalary
echo " $?"
```

let Salary=3000 tells the computer to create a variable by the name of Salary and to assign that variable the value 3000.

let NewSalary=2000 tells the computer to create a variable by the name of NewSalary and to assign that variable the value 2000.

test $Salary -ge $NewSalary tells the computer to test to determine whether the value of the Salary variable is greater than or equal to the value of the NewSalary variable. If so, test returns a true value; otherwise, test returns a false value. Finally, echo "$?" displays the value that test returns.

## The -lt (less than) operator

To determine whether the value of the first variable is less than the value of the second variable, you use the -lt operator, as in the following example:

```
let Salary=3000
let NewSalary=2000
test $Salary -lt $NewSalary
echo " $?"
```

let Salary=3000 tells the computer to create a variable by the name of Salary and to assign that variable the value 3000.

let NewSalary=2000 tells the computer to create a variable by the name of NewSalary and to assign that variable the value 2000.

test $Salary -lt $NewSalary tells the computer to test to determine whether the value of the Salary variable is less than the value of the NewSalary variable. If so, test returns a true value; otherwise, test returns a false value. Finally, echo "$?" displays the value that test returns.

![](img/05279073f26be7df99b3c487360dec6a_107_0.png)

## Test your programming knowledge

1. Is the following statement true or false?
   ```
   $BobSalary -le $MySalary
   "I want a raise" --eq "Find another job."
   ```
   - a. False.
   - b. True.
   - c. Could be true or it could be false.
   - d. It all depends on how you look at it.

2. What does the following line tell the computer to do?
   - a. Determine whether BobSalary is less than or equal to MySalary.
   - b. Determine whether BobSalary is less than MySalary.
   - c. Tell me how much Bob is making.
   - d. Justify my request for a raise.

Answers: 1 a. See “The -eq (equal to) operator.” 2 a. “The -le (less than or equal to) operator.”

## The -le (less than or equal to) operator

To determine whether the value of the first variable is less than or equal to the value of the second variable, you use the -le operator, as in the following example:

```
let Salary=3000
let NewSalary=2000
test $Salary -le $NewSalary
echo "$?"
```

let Salary=3000 tells the computer to create a variable by the name of Salary and to assign that variable the value 3000.

let NewSalary=2000 tells the computer to create a variable by the name of NewSalary and to assign that variable the value 2000.

test $Salary -le $NewSalary tells the computer to test to determine whether the value of the Salary variable is less than or equal to the value of the NewSalary variable. If so, test returns a true value; otherwise, test returns a false value. Finally, echo "$?" displays the value that test returns.

A true value is one; a false value is a zero.

![](img/05279073f26be7df99b3c487360dec6a_108_0.png)

# Part III
# Making Decisions

The 5th Wave
By Rich Tennant

![](img/05279073f26be7df99b3c487360dec6a_110_0.png)

## In this part . . .

Our program contains many instructions for the computer. Simply stated, programs contain a list of instructions that the computer follows one after the other.

But what if your computer needs to follow some of those instructions only if a particular condition exists? For this situation, you must tell the computer to make a decision.

Your computer's decision-making capability enables you to build complex programs that further enable your computer to perform mundane tasks that you'd otherwise get stuck doing.

In this part, you find out how to instruct your computer to make decisions.

## Chapter 7
## The if, if else, and if elif Statements

### In This Chapter

- Specifying a condition
- Using the `if` statement
- Using the `if else` statement
- Using the `if elif` statement

Decisions, decisions, decisions. We're always asked to make decisions. Where, for example, do you want to go on vacation? To my mother's or to Hawaii?

Some decisions are obvious choices, but you base even those no-brainers on *prevailing conditions*: Do we have enough money for a trip to the islands? And if conditions aren't right, even the most desirable choice is just a memory. (It's Mom's again this year.)

Linux programming also can make decisions by checking conditions and then reaching a conclusion.

In this chapter, I show you how you can have your program make decisions for you based on information your program receives from the keyboard or from a file.

### Conditions

A *condition* is a situation that must exist or must not exist. If the condition exists, the condition is true; otherwise the condition is false.

You either have enough money for the trip to Hawaii . . . or you don't. You have no room for an almost enough money condition. In Linux, a condition takes the form of the following:

- A single variable
- An expression

Say that you have all your money in your wallet. We can call the variable *wallet* and the value of the variable is thus the *amount of money* that you have in your wallet. So do you have enough money for the trip to Hawaii? Look in your wallet. You say that you don’t have much money in it? You’re broke! The value of the wallet variable, therefore, is zero — which means that you don’t have enough money for the trip. The condition is false.

Say, however, that you have a good deal of money in the wallet. Is it enough money for the trip? You ask yourself whether the amount of money in the wallet is equal to or greater than $10,000 (the amount that you need for the trip). This question is an *expression* that results in either a true or false answer.

### The condition as a single variable

The value of a single variable must be either *true* or *false*. You represent a *true* value as a *nonzero* value; a *false* value is a *zero* value. Following are two ways to determine whether the value of a variable is either true or false. The first method is to explicitly check the value of the variable, as in the following example:

```
if [ $#HaveEnoughMoney -eq 1 ]
```

Your program checks whether the value of the variable is true or false by using the equal operator (-eq).

If you can have your program check whether a condition is true, you can also have your program check whether the value of the variable is false, as in the following example:

```
if [ $#HaveEnoughMoney -ne 0 ]
```

The -ne (not equal) operator tells your program to reverse the logic. If you use the -eq operator, your program checks whether the variable is true. Place the -ne operator in the expression, and your program checks whether the variable is not true, which is false.

### The condition as an expression

A condition can also be an *expression*. An expression tells your program to perform an operation on information. You can ask the program to check whether the value of a variable — your bank balance, for example — is more than a specific amount. In this case, the result of an expression is either true or false, as shown in the following example:

```
if [ $#BankBalance -gt 3000 ]
```
