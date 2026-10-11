|| operator tells the computer to return a `true` value only if one or both `LowestPrice` and `LikeCar` have a `true` value. Following are all the possible outcomes:

| BuyCar | LowestPrice | LikeCar |
| :----------- | :--------------------- | :------- |
| True | True | True |
| False | False | False |
| True | True | False |
| True | False | True |

# ## Comparison Operators

*Comparison operators* tell the computer to compare the values of two numbers or two strings to decide whether they’re equal to, not equal to, greater than, or less than one another. Table 6-3 shows the common comparison operators.

| **Table 6-3** Comparison Operators |
|:---------------------------------|:------------------------------------|
| **Operator** | **What It Does** |
| -eq | Equal to |
| -ne | Not equal to |
| -gt | Greater than |
| -ge | Greater than or equal to |
| -lt | Less than |
| -le | Less than or equal to |

# ### The -eq (equal to) operator

To determine whether two values are the same, you use the `-eq` operator. Notice that no space falls between the hyphen (-) and the symbol eq. The following example shows you how to use this operator:

```
let Salary=3000
let NewSalary=2000
test $Salary -eq $NewSalary
echo " $?" 
```