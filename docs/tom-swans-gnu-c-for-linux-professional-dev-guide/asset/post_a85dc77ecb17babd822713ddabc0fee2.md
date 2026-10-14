
Because the expression `ch++` increments `ch` before the statement that outputs the variable, that loop prints the alphabet from b to z. To start at a, the `char ch` variable must be initialized to one less than that letter. Here’s the bug-free version (where chars are just integers, and as such, may be used as shown here in mathematical expressions):

```
char ch = 'a' - 1;  // !!!
while (ch++ < 'z')
    cout << ' ' << ch;
```

This type of mistake—called an “off-by-one error”—is easy to make, especially in loops that examine and alter the control variable. Even for experienced programmers, off-by-one errors are a common source of bugs. A good way to avoid this trouble is to write your while and other statements the long way, as in preceding examples.

You can similarly use the decrement operator—two minus signs—in repetitive statements. For example, this while loop counts down from 10 to 1:

```
int i = 11;
while (--i > 0)
    cout << ' ' << i << endl;
```

## THE do-while STATEMENT

The do-while (which sounds to me like a ’60s pop-group vocal embellishment—do-while diddy dum diddy do) is a sort of upside-down while loop. C’s do-while looks like this:

```
do {
    statement;
} while (condition);
```

The statement executes while the condition is true. Compare this with a plain while, which evaluates its condition before executing any statements. A plain while loop can never perform any action if the controlling condition is initially false. But a do-while always performs its action at least once because it doesn’t get around to evaluating the condition until the end of the loop. This leads to a general two-part rule for choosing between while and do-while:

- 1. Ask yourself: “Is there at least one condition when the statements in the loop should not execute, not even once?” If the answer is yes, a while loop probably is the correct choice.
- 2. If the answer to the preceding question is no, a do-while might be appropriate. If the statements in a loop must execute at least once, regardless of the controlling expression’s value, use a do-while.

A do-while statement can be simple or compound. Technically, braces are needed only if two or more statements are in the loop. However, although you can write do-while statements such as this:

```
do
    statement;
while (condition);
```

it is more common to surround even a single statement in braces:

do {
    statement;
} while (condition);

Inside the braces, you may insert as many statements as you need:

do {
    statement1;
    statement2;
    ...
} while (expression);

To demonstrate do-while, Listing 9.6, dwcount.cpp, is similar to the wcount.cpp program but uses a do-while loop to count from 1 to 10.

### LISTING 9.6 DWCOUNT.CPP

```
#include <iostream.h>

int counter;

int main()
{
    cout << "Counting with do-while" << endl;
    counter = 1;
    do {
        cout << "counter == " << counter << endl;
        counter++;
    } while (counter <= 10);
    return 0;
}
```

As you can with while loops, it is often possible to combine the use and increment of the control variable. For example, the do-while loop in dwcount.cpp can be shortened to the following:

```
do {
    cout << "counter == " << counter << endl;
} while (++counter <= 10);
```

In this case, however, the operator must be applied before counter is evaluated. In other words, the expression ++counter equals the incremented value of the variable; and, therefore, the loop executes one final time when that value is 10. If the statement used counter++ as the condition, the loop would count from 1 to 11. (The expression, however, could also be changed to (counter++ <= 10).) Here again, an off-by-one error is easy to make, and the longer version, which costs nothing in performance, is clear and understandable.

## THE for STATEMENT

The for statement is one of the most powerful programming tools in C and C++. When you know, or can calculate in advance, the number of times a statement block should execute, a for statement is usually the best choice of repetitive statements. In general outline form, a for statement looks like this:

```
for (expression1; condition; expression2) {
    statements;
}
```

Following the reserved word for are three elements in parentheses. To understand the purpose of each element, it's helpful to examine the equivalent while loop:

```
expression1;
while (condition) {
    statements;
    expression2;
}
```

Compare the for and while loops. Each executes expression1 exactly one time before entering the loop. Usually, this initializes the loop's control variable, but it can be any valid expression. As long as condition is true, one or more statements are executed, followed by expression2. Typically, expression2 modifies the control variable initialized by expression1.

For example, the following for loop counts from 1 to 10:

```
int i;
for (i = 1; i <= 10; i++)
    cout << "i == " << i << endl;
```

That initializes the int variable i to 1, and while i is less than or equal to 10, writes its value and executes i++ to increment i so the loop eventually ends. The preceding for loop is functionally equivalent to this while statement:

```
int i = 1;
while (i <= 10) {
    cout << "i == " << i << endl;
    i++;
}
```

C++ permits variables such as i to be declared and initialized inside a for loop. The preceding for loop can be shortened by one line as follows:

```
for (int i = 1; i <= 10; i++)
    cout << "i == " << i << endl;
```

Unfortunately, this leads to a controversial question. Should the integer i belong to the for loop itself, or to the for loop's parent (function main(), for example, if that's where the loop resides)? Current ANSI C++ rules state that the control variable i in this case belongs to the for statement—that is, it's scope extends only to its declaring statement block. By this rule, a subsequent statement can define another int i control variable without conflict. However, this isn't true of all C++ compilers, and for more on this controversy, see "for Loop Scoping" in this chapter.
