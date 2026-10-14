# LISTING 9.1 CHOICE.CPP

```
#include <iostream.h>

int number; // User input

int main()
{
cout << "Enter a number from 1 to 10: ";
cin >> number;
if ( (number < 1) || (number > 10) )
    cout << "Incorrect answer!" << endl;
return 0;
}
```

Compile and run the program, and enter an integer value. If you enter a value outside the expected range, the program voices its annoyance as the following sample run shows:

```
$ g++ choice.cpp
$ ./a.out
Enter a number from 1 to 10: 11
Incorrect answer!
```

The program uses an if statement to test input for validity, probably one of the most common uses for this type of statement. Examine the program's if statement closely:

```
if ( (number < 1) || (number > 10) )
cout << "Incorrect answer!" << endl;
```

The condition tests whether number is less than 1 or (!!) greater than 10. If either condition is true, the entire expression is true and the program displays an error message. Parentheses group the full expression. Strictly speaking, the inner parentheses aren't needed because the less-than and greater-than operators < and > have higher precedence than the logical OR operator || (see Appendix B, "C++ Operator Precedence and Associativity"). However, the extra parentheses make the statement perfectly clear.

# THE else STATEMENT

You might think of the else statement as the if statement's sidekick. It must follow an if statement to select an alternative action. In general, use else like this:

```
if (condition)
    statement1;
else
    statement2;
```

If the condition is true, statement1 executes; otherwise, statement2 goes into action. The statements may be simple or compound. Use parentheses to group related statements as shown here:

```
if (condition) {
    statement1;
    statement2;
} else
    statement3;
```