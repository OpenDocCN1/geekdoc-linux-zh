# ### 23.7 Arithmetic Operations Using the expr Utility

This does not appear on the screen. Instead, the **set** command catches the output and stores it in the positional parameters **$1** through **$6**:

```
```
$1  contains  Fri
$2  contains  Aug
$3  contains  13
$4  contains  10:56:08
$5  contains  EST
$6  contains  1999
```
```

# ## 23.7 Arithmetic Operations Using the expr Utility

The shell is not intended for numerical work—if you have to do a lot of calculations, you should consider C, FORTRAN, or Pascal. Nevertheless, the **expr** utility may be used to perform simple arithmetic operations on integers. (**expr** is not a shell command, but rather a separate UNIX utility; however, it is most often used in shell scripts.) To use it in a shell script, you simply surround the expression with back-quotes. For example, let’s write a simple script called **add** that adds two numbers typed as arguments:

```
```
#!/bin/sh
#  Add  two  numbers
sum=`expr  $1  +  $2`
echo  $sum
```
```

Here we defined a variable **sum** to hold the result of the operation. (Note the spaces around the plus sign, but not around the equals sign.) To run this script, we might type the following line:

```
```
$  add  4  3<Return>
```
```

The first argument (4) is stored in **$1**, and the second (3) is stored in **$2**. The **expr** utility then adds these quantities and stores the result in **sum**. Finally, the contents of **sum** are echoed on the screen:

```
```
7
$
```
```

The **expr** command only works on integers (i.e., whole numbers). It can perform addition (+), subtraction (-), multiplication (*), integer division (/), and integer remainder (%).