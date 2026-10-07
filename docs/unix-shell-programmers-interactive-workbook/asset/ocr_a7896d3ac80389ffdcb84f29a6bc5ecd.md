# Lab 4.2: Evaluating and Assigning Values

e) What result do you get if you print a reference to CityState?

Once you assign a value to a variable, it does not change until you assign another value to it, even if its value was assigned using references to other variables.

Now use the following command to change the value of city to Bismarck.

```
city=Bismarck
```

f) What happens if you now print the values of city and CityState?

# 4.2.3 USE SET TO UNINITIALIZE A VARIABLE

The first time you assign a value to a variable, the variable comes into existence.

Other programming languages require you to declare that a name represents a variable before you can use it (the shell supports this feature too; see Lab 6.1, "Typed Variables and Scope") but, in general, you get the shell to create a new variable any time you want to, just by picking a name and assigning a value to it.

Sometimes you will want to get rid of a variable, usually as a way to check that your script or function is doing what you expect it to do, rather than as a normal programming technique.

Remember, if you reference a variable that doesn't exist yet, the shell substitutes an empty string for the value.