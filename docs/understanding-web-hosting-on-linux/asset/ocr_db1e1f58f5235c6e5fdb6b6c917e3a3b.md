# Server-side Java * 95

String CoName;
Declare and initialize a string like this.
String CoName = "Midrange";

You can concatenate a string with the plus sign. The following example concatenates a blank to FirstName, and then concatenates LastName.

```
FullName = FirstName + ' ' + LastName;
```

Unlike Java array, you cannot change a specific character within a string. For example, you can't change the spelling of Midrange to Midrange by replacing the j with a g. However, you can modify the string by concatenating the characters you want to replace with the substring you want to keep. Assuming a string named Name, you could change Midrange to Midrange, you could use the following statement:

```
Name = Name.substring(0,5) + "ge";
```

In Java, you invoke an object's method with the method notation. In the example above, substring is a method of object Name. The first argument of the substring (0) references the first position of the substring, and the second argument (5) specifies the ending position. In this case, the value of substring is Midran. Notice the first position of the substring is referenced with a zero, not one, so the ending position is five, not six. As Java arrays, strings start with zero.

# Constants

In Java, you define constants for the entire class; you cannot define a local constant for a specific function (method) of the class. So, it stands to reason that you define constants prior to the main function. Use static final to declare a constant, as illustrated in Figure 7.4.

```
class Test
{
    static final double pie = 3.14159265;
    public static void main(String[] args)
    {
        System.out.println("Pie = " + pie);
    }
}
```

> Figure 7.4: A Java application's main method is the entry point to the class.

In this example, the scope of pie is to this class only. To declare the pie constant as global, precede static final with public (i.e., public static final).

# Literals

While a variable is a reference to data, a literal is a symbol or quantity that is itself the data. Java contains five types of literals: integer, numeric containing a decimal point or exponent, Boolean, character, and special character. Integer literals by default are 32-bit (four-byte), signed decimal numbers, but to int Any integers greater than 2,147,483,647 are assumed to be longs. You can force a number to be a long integer by ending with l or L. To force 31 to be a long integer, for example, specify 31L.