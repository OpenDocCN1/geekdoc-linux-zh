# ## 10

If we look back at the code for addseq.sh we can see that we created a variable in the function called sum. When you create variables in functions those variables become globally accessible, meaning that even after the program is finished that variable retains its value in your shell. We can easily verify this by echoing the value of sum:

```
echo $sum
```

# ## 10

This is an example of one strategy we can use to retrieve values that a function has calculated. Unfortunately this approach is problematic because it changes the values of variables that we might be using in our shell. For example if we were storing some other important value in a variable called sum we would destroy that value by accident by running addseq. In order to avoid this problem it’s important that we use the local keyword when assigning variables within a function. The local keyword ensures that variables outside of our function are not overwritten by our function. Let’s create a new version of addseq called addseq2 which uses local when assigning variables.