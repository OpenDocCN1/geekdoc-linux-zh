```
/
i {
```

```
}
```

# Program 18.2 Output

[Click here to view code image](#)

```
T T
```

As you can see from the comments in Program 18.2, the program is logically divided into three sections: the @interface section, the @implementation section, and the program section. These sections are typically placed in separate files. The @interface section is usually put into a header file that gets included in any program that wants to work with that particular class. It tells the compiler what variables and methods are contained in the class.

The @implementation section contains the actual code that implements these methods. Finally, the program section contains the program code to carry out the intended purpose of the program.

The name of the new class is F              , and its parent class is O             . Classes inherit methods and variables from their parents.

As you can see in the @interface section, the declarations

```
i
```

say that a F              object has two integer members called n               and d               .

The members declared in this section are known as the instance variables. Each time you create a new object, a new and unique set of instance variables is created. Therefore, if you have two fractions, one called f               and another called f               , each has its own set of instance variables. That is, f              and f              each has its own separate n              and d               .

You have to define methods to work with your fractions. You need to be able to set the value of a fraction to a particular value. Because you don’t have direct access to the internal representation of a fraction (in other words, direct access to its instance variables), you must write methods to set the numerator and denominator (these are known as setters). You also need methods to retrieve the values of your instance variables (such methods are known as getters).¹