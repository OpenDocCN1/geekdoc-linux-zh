declare a global variable in Linux that way. Instead, you use the `export` keyword, which creates an environment variable. As is true of a global variable, you can share an environment variable with other programs.

The following example shows you how to declare a global variable within your program (so just follow this example so that the entire world can know your Social Security number):

```
`declare SSNum="555-55-5555"`
```

You must be very careful whenever you decide to use a global variable in your program for the following reasons:

+   - Any program running on the same computer as your program can read and change the value that you store in the global variable.
+   - The last value that you assign to the global variable is the one that your computer keeps. So if two programs change the value of the same global variable, one program may not work correctly.
+   - Finding a problem resulting from someone assigning a wrong value to a global variable can become a nightmare. You don't know which program changed it.