# Part II: The Basics of Writing Code

Sometimes strings consist of numbers instead of letters, but they’re still strings, such as in the following telephone number:

```
declare Telephone="555-5555"
```

Don’t forget this rule: Put quotation marks around a string value. Quotation marks tell Linux that characters appearing between the quotation marks belong together and that it’s to treat them as a string.

# Assigning variables to other variables

You can take data that you stuff into one variable and copy it to another variable. You end up with two copies of the data. Your computer doesn’t remove the data from the original variable.

The following example shows you how to copy data from one variable to another by using a string variable:

```
declare MyGoal="Buy out Bill Gates"
declare OurGoal="$MyGoal"
```

In this example, you’re telling your computer in the first line to go to the variable MyGoal and copy the data that’s there. Next, you’re telling your computer to take that data and place it into the variable OurGoal. You’re doing so by using the name of the original variable, and you’re placing a dollar sign ($) in front of it.

You can perform this same copying procedure by using a numeric variable, as in the following example:

```
let MySalary=1000000
let OurSalaries=$MySalary
```

Your computer takes a copy of the value of your salary and stuffs it into the variable OurSalaries. The value of OurSalaries is now the same as your salary, 1000000. Your own million-dollar salary, however, remains safe in the MySalary variable.

# Using Data Types

A Linux variable can store any number or string. You can confuse your computer, however, if you first tell it one thing and then tell it to do something completely opposite (and computers don’t like you confusing them).