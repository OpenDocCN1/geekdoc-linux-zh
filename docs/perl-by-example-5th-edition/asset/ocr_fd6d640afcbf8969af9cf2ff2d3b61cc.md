![](bbox=[0.55, 0.07, 0.85, 0.35])

# 6
Where's the
Operator?

In the real world, there are operators who operate switchboards, computers, bulldozers, tanks, and so forth. In Perl, operators operate on numbers and strings, or a combination of them. Operators are symbols, such as +, -,*, >, <, that produce a result based on some rules. This chapter is all about Perl operators, their use, and their rules.

By the end of this chapter, you should be able to explain how Perl evaluates the following example:

```
$year= (localtime) [5] + 1900;
$year % 100 == 0 && $year % 400 == 0 || $year % 100 != 0 &&
$year % 4 == 0? printf "Year %d is leap year."\n",$year :
printf "\nYear %d is not a leap year.\n", $year;
```

# 6.1 About Perl Operators—More Context

Before getting into the nitty gritty of Perl operators, consider the following Example 6.1. The user is asked a question and his answer is tested. The results would normally be unexpected unless you have a good grasp on how Perl operators handle context, a subject we have been discussing from the beginning. The problem with this example is the use of the == operator, the equality operator used to test whether two numbers are equal. But in the example, the operators are used incorrectly to evaluate the equality of two strings.