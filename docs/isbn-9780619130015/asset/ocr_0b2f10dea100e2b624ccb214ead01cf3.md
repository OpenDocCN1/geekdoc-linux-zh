![](bbox=[0.18, 0.08, 0.78, 0.41])

Figure 9-8: Output of example7.p

# ## Arrays

Arrays are variables that store an ordered list of scalar values that are accessed with numeric subscripts, starting at zero. An “at” sign (@) precedes the name of an array when assigning it values. When processing the individual elements of an array, however, use the $ character. For example, this program creates the array pets.

```
#!/usr/bin/perl
# Program name: example8.p
@pets = ("dog", "cat", "parrot", "hamster");
print ("My pets are:\n");
print ($pets[0]\n);
print ($pets[1]\n);
print ($pets[2]\n);
print ($pets[3]\n);
```

Figure 9-9 shows the program output.