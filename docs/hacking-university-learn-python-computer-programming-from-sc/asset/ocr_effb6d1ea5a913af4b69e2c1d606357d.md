Remembering that only one statement in a decision “tree” can ever run, we can see that any elif that activates essentially runs its code block and then breaks from the decision structure.  Else is used as a “catch-all” type expression in our above program.  Any invalid input, such as “-1” would be picked up by else and displayed as such.  Good programming form comes from catching potential user errors like this, and as an aspiring programmer you should always be expecting the user to incorrectly input values whenever the chance arises.

“And” is a comparison operator that forces both parts of an expression to be true.  Another operator, “or”, is used to force only one part of the expression to evaluate to true.

```
elif (age == 25 or age == 50 or age == 75):   
print ("Happy quarterly birthday!")
```

If we were to put this elif within the above program (under the first if), we would see that only one part of the expression must be true for the whole comparison to be true.  The user’s age could be 25, 50, or 75 and the application would say “Happy quarterly birthday”.  Using “and” instead of “or” would be impossible, because the age cannot be 25 and 50 and 75 all at the same time.  The keywords that we use for comparisons are helpful and greatly useful, but if used incorrectly they can lead to logic errors.