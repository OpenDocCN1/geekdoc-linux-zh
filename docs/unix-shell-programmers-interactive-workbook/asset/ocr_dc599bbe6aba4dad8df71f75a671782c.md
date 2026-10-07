b) Now run the script again, but with each of the letters of the alpha-bet as parameters. Explain these results.

Create a function named f512 with the same print statement in it as s512. Run it twice, once with your name and once with the letters of the alpha-bet as parameters.

c) Is there any difference between running the function and running the script?

# 5.1.3 USE SPECIAL PARAMETER VARIABLES (# @ *)

The title of this exercise might look like curse words in a comic book, but it's really a list of three special variables the shell sets when a function or script is called. The number of parameter variables is given by the value of the number sign variable ( # ), and all the parameter variables are the value of the at ( @ ) and asterisk (* ) variables. The difference between @ and * has to do with quoting, as you will see.

Create a script named s513 that prints each of these variables, and run it using the following commands:

```
s513 hello 123
s513 There are four words.
```

+   - a) What did you observe?