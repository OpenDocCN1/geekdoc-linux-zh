```
i
{

}
```

# Program 6.7 Output

> Click here to view code image

```
N 10
B 2
C
```

# Program 6.7 Output (Rerun)

> Click here to view code image

```
N 128362
B 16
C
```

# The const Qualifier

The compiler allows you to associate the c qualifier with variables whose values will not be changed by the program. That is, you can tell the compiler that the specified variables have a constant value throughout the program's execution. If you try to assign a value to a c variable after initializing it, or try to increment or decrement it, the compiler might issue an error message, although it is not required to do so. One of the motivations for the c attribute in the language is that it allows the compiler to place your c variables into read-only memory. (Normally, the instructions of your program are also placed into read-only memory.)