# **Number Comparison**

These operators can be used to compare two numbers:

> >=—To compare whether one number is greater than or equal to the other number
>
> <=—To compare whether one number is less than or equal to the other number
>
> >—To compare whether one number is greater than the other number
>
> <—To compare whether one number is less than the other number

The next examples compare two numbers, *number1* and *number2*, in a shell program called compare2:

```
```bash
#!/bin/tcsh
set number1=5
set number2=10
set number3=5

if ($number1 > $number2) then
    echo "number1 is greater than number2"
else
    echo "number1 is not greater than number2"
endif

if ($number1 >= $number3) then
    echo "number1 is greater than or equal to number3"
else
    echo "number1 is not greater than or equal to number3"
endif

if ($number1 < $number2) then
    echo "number1 is less than number2"
else
    echo "number1 is not less than number2"
endif

if ($number1 <= $number3) then
    echo "number1 is less than or equal to number3"
else
    echo "number1 is not less than or equal to number3"
endif
```
```

When executing the shell program *compare2*, you get the following results:

number1 is not greater than number2
number1 is greater than or equal to number3
number1 is less than number2
number1 is less than or equal to number3

![](bbox=[0.89, 0.41, 0.97, 0.48])