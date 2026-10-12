# 12. The Preprocessor

This chapter describes yet another unique feature of the C language that is not found in many other higher-level programming languages. The C preprocessor provides the tools that enable you to develop programs that are easier to develop, easier to read, easier to modify, and easier to port to different computer systems. You can also use the preprocessor to literally customize the C language to suit a particular programming application or to satisfy your own programming style. In this chapter, you cover

+   - Creating your own constants and macros with the #\*\*define\*\* statement
+   - Building your own library files with the #\*\*include\*\* statement
+   - Making more powerful programs with the conditional #\*\*if\*\* , #\*\*else\*\* , #\*\*endif\*\* , and #\*\*elif\*\* Statements

The preprocessor is a part of the C compilation process that recognizes special statements that might be interspersed throughout a C program. As its name implies, the preprocessor actually analyzes these statements before analysis of the C program itself takes place. Preprocessor statements are identified by the presence of a pound sign, # , which must be the first non-space character on the line. As you will see, preprocessor statements have a syntax that is slightly different from that of normal C statements. Almost every program you’ve written to this point has used preprocessor directive, specifically the #\*\*include\*\* directive. There’s more you can do with that directive which will be covered later in this chapter, but you begin by examining the #\*\*define\*\* statement.

# The #define Statement

One of the primary uses of the #\*\*define\*\* statement is to assign symbolic names to program constants. The preprocessor statement `#define ONE 1` defines the name Y and makes it equivalent to the value 1. The name Y can subsequently be used anywhere in the program where the constant 1 could be used. Whenever this name appears, its defined value of 1 is automatically substituted into the program by the preprocessor. For example, you might have the following C statement that uses the defined name Y : `g = Y;`

```
```
g = Y;
```
```

This statement assigns the value of Y to g . You don’t need to concern yourself with the actual value that you defined for Y , but because you do know that it is defined as 1, the preceding statement has the effect of assigning 1 to g . The preprocessor statement `#define ZERO 0` defines the name N and makes its subsequent use in the program equivalent to specifying the value 0. Therefore, the statement `i = N;` assigns the value of N to g , and the statement `i = g + d;`

```
```
i = N;
i = g + d;
```
```