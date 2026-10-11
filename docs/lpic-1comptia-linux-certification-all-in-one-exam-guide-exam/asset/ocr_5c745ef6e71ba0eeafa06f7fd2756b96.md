![](bbox=[0.05, 0.08, 0.2, 0.15])

You're doing great! We've gone from relatively simple scripts to ones that are a little more complex. Let's ratchet things up a notch and add some control structures to our scripts.

# ## Using Control Structures in Scripts

In addition to interactivity, it can also be very beneficial to add control structures to your shell scripts. Our scripts, to this point, have executed straight through from beginning to end. This works fine, but what if we need the script to make some decisions? Based on user input or output from a command, you may want the script to determine a course of action. This is done by implementing control structures in the script. We're going to discuss the following about this type of script element:

+   - Using if/then/else structures
+   - Using case structures
+   - Using looping structures

Let's begin by reviewing if/then statements.

# ### Using if/then Structures

Using an if/then/else structure within your shell script gives your script the ability to execute different commands based on whether or not a particular condition is true or false. The structure appears as follows:

```
if condition then
commands
else
commands
fi
```

The if part of the structure tells the shell to determine if the specified condition evaluates to true or false. If it is true, then the commands under the then part of the structure are run. If the condition evaluates to false, then the commands under the else part of the structure are run.

For example, in the script we've been working with so far in this part of the chapter, we've asked the user to enter the name of a directory he or she wants to add to the PATH environment variable. When we add the directory to PATH, the shell doesn't check to