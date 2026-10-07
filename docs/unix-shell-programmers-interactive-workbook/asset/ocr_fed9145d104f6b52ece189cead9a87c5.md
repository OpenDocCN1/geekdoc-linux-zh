# Chapter 6: ADVANCED VARIABLE USAGE 299

j) What did the shell print?

Enter the following command:

```
print ${#days[@]}
```

k) What number was printed, and how does it relate to the array, days?

Enter the following commands:

```
weekend[0]=6 weekend[1]=0 \
print There are ${#weekend[@]} \
days in the weekend.
print They are ${days[ weekend[0] ]} and \
${days[ weekend [1]]}.
```

l) Explain the output of the first print command.

m) Explain the output of the second print command

Assign the value Birthday to days[31] and assign the empty string to days[99].