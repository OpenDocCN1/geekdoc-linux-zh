The subroutine and its statements are not executed until called. You can call a subroutine by attaching a set of empty parentheses to its name (called the null parameter list), or by calling it as a built-in function. If you call the subroutine without parentheses, then you must declare it first$^2$

# EXAMPLE 11.1

(The Script)

```
1 sub grep{ print "Welcome, Välkommen till, Bienvenue!\n";}
# Define the subroutine

2 &grepme(); # Call the subroutine; could also say &greetme

3 print "Program continues....\n";

4 &greetme if defined &greetme; # Call to subroutine

5 print "More program here.\n";

6 &bye; # Older method of calling a subroutine
sub bye { print "Bye, adjó, adieu.\n"; }

8 bye(); # Call to subroutine using empty parameter list
```

(Output)

2 Welcome, Välkommen till, Bienvenue!
3 Program continues.....
4 Welcome, Välkommen till, Bienvenue!
5 More program here.
Bye, adjó, adieu.
Bye, adjó, adieu.

# EXPLANATION

+   1. This is a subroutine definition consisting of the keyword sub, followed by the name of the subroutine, greetme, and a block of statements that will execute when the subroutine is called. You can place this definition anywhere in your program and it will do nothing until it is called. In this example, there is only one print statement that will execute when the function is called.

+   2. The subroutine greetme is called by appending a set of empty parentheses to its name. When called, the program will jump into the subroutine and start executing the statements defined there; in this case, the Welcome statement.

+   4. After the subroutine is called (invoked), program execution starts at the line right after where it was called and continues from there.
+   The subroutine greetme is called again. The defined built-in function is used to check that the subroutine has been defined.
+   The program resumes execution after the subroutine exits on line 4.

+   6. The subroutine &bye is called. The definition is found later on line 7. This is an older way of calling a subroutine and rarely used today.

+   7. Subroutine bye is defined. No matter where you place subroutines, the compiler sees them.

+   8. Subroutine bye is called using a null parameter list.

+   2. The sigil for a subroutine is the ampersand (&) and in older programs you may see this used to call a subroutine, as in &greetme. Today, the & is used only in special cases with reference.