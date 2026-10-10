If the user had input the correct answer of 2 instead, the if statement would evaluate to true and the console would print "Correct". In that situation, the else statement would not run at all. Focus once again on the indented code and understand that those lines are indented because they are part of the "if" and "else" code blocks. Also realize that only one statement from a decision structure can ever run in a program, so if "else" runs, that means "if" did not run. Likewise a program that has "if" activated will not run the code block under "else". Conditional statements are not limited to single lines of code, as you can see below.

```
user_input =  input("What language is this written in? ")

if (user_input == "Python"):

print ("Correct!")

else:

print ("Incorrect...")

print ("This is not written in {}, it uses Python!".format(user_input))
```