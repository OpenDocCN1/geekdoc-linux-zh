
## Warning

> When using continue, especially in while and do-while loops, be sure that the loop's condition performs an action that eventually ends the loop. In this case, for example, i++ in the while loop's conditional expression ensures that the value of i eventually equals 100, ending the loop.

## Other Types of Statements

Following are some other types of flow-control statements you might find useful. First is the notorious goto, which most experienced programmers rightly avoid using. I also show some interesting variations on for loops, and I explain how to use one of the most powerful of C and C++ statements, the switch.

### The goto Statement

A goto statement directs a program to execute another statement and to continue executing subsequent statements starting from that location. Because a goto can "jump" to any place in a program, using goto is like exiting a highway through a field rather than at a marked exit. Be prepared for a bumpy ride.

At first glance, goto seems tremendously versatile. In practice, however, the statement gives programmers too much freedom to jump from here to there and over yonder. At best, it's difficult to fathom the results of a program that has several goto statements. At worst, the code doesn't work at all.

If you must use goto, insert a label (an unused identifier and colon) above any statement. Execute goto LABEL to direct the program flow to that location. Listing 9.9, gcount.cpp, demonstrates how to use goto to count from 1 to 10.

### LISTING 9.9 GCOUNT.CPP

```
#include <iostream.h>

int count;

int main()
{
    count = 1;
TOP:
    cout << "count = " << count << endl;
    count++;
    if (count <= 10)
        goto TOP;
    return 0;
}
```

In the sample program, the label TOP: marks a target location for a goto statement. You may specify any unused identifier as a label. The if statement examines an integer variable count.

If count is less than or equal to 10, goto transfers control to TOP:, executing the output and count++ statements until count becomes larger than 10. When that happens, the if statement does not execute the goto, and the program continues to the bitter end.

The program works, but it lacks the intuitive clarity of the while, do-while, and for loops described in this chapter. By all means, learn how to use goto. You might stumble over one in somebody else's code. But avoid using goto in your own programs. This is one statement you can do without.

## Do-Nothing for Loops

This is not a new kind of C++ statement (I'm tempted to call it a do-for-nothing loop), but is simply a variation of a common for statement. However, a Do-Nothing for loop is easy to create unintentionally by a misplaced semicolon, as in this faulty code:

```
for (int i = 1; i <= 100; i++) { // ???
cout << " " << i;
```

Because of the semicolon before the comment, C++ "sees" a null statement between the closing parenthesis and semicolon. Although the for loop iterates variable i from 1 to 100, the loop merely executes the phantom null statement, not the output statement as the programmer probably intended. Worse, because the output statement does not belong to the for statement, it executes once after the loop is finished. Fix the code by removing the semicolon before the comment.

> Tip
> GNU C++ does not warn you about this type of mistake as do some other compilers such as Borland C++. If your code compiles but a for loop doesn't seem to operate correctly, check whether you ended it prematurely with a misplaced semicolon.

On rare occasions, a Do-Nothing for loop can be useful if, for example, the conditional expression calls a function or performs some work of its own. In that case, it is traditional to insert a space between the closing parenthesis and semicolon to indicate that the construction is intentional. It's not a bad idea to add a comment as well:

```
int i;
for (i = 1; f(i); i++) ; // Semicolon intentional
```

This loop calls function f() as long as that function evaluates to true. Presumably, the function uses the value of i in some way and returns true or false. (See Chapter 10, "Creating and Calling Functions," for more about functions.)

> Warning
> Beware of side effects in code such as the preceding. If function f() affects the value of i, it might cause unpredictable conflicts with the use of the control variable!
