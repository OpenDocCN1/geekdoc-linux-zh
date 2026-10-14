A computer program runs like a river. Unless diverted, a river's water flows in the shortest path to the sea. Likewise, with no intervention, a C++ program's statements execute one after the other from top to bottom until the program ends. In C and C++ programs, flow-control statements operate like dams, channels, water wheels, and aqueducts to direct the program's execution along whatever path you want it to follow.

C and C++ provide two basic types of flow-control statements: those that make decisions based on a conditional true or false argument, and those that create loops for repeatedly executing various operations. This chapter introduces both types of C and C++ flow-control statements.

# CONDITIONAL STATEMENTS

Conditional statements make decisions by examining true or false expressions. Although simple in concept, directing a program's flow through the use of conditional statements is one of the most powerful programming tools at your disposal. The following sections introduce C and C++ conditional if and else statements, and also explain how to use conditional expressions—a handy shorthand if-else.

# THE if STATEMENT

The if statement operates just as you might expect. If its stated condition is true, the statement performs an action; otherwise, execution continues with the following statement. A simple if statement in outline form looks like this:

```
if (condition)
    statement;
```

The condition can be any expression that evaluates to a true or false value. It must be in parentheses. If the condition is true (nonzero), the statement executes. If condition is false (zero), the statement is skipped. The statement can be any valid C or C++ statement, or it can be a statement block containing one or more statements. For example, this if statement performs two statements if its condition is true:

```
if (condition) {
    statement1;
    statement2;
}
```

> Note
> Indenting statements helps show their relationship in the program's source code. Many C and C++ programmers indent statements by pressing the Tab key. Some also indent the braces around a compound statement block. So that I can fit as much code as possible on the page, however, I use minimal indentation of two spaces in this book's listings.