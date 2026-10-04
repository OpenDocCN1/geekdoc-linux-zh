cutes the code in the indented block (Line 3). (This code block simply adds each item to the total.) In Line 4, we use the Python return statement to exit the script returning the value of the caller.
Once you have entered the code for this script, click on Save Changes. Your script should look like Figure 14-4.

![](bbox=[0.198, 0.137, 0.801, 0.433])

Figure 14-4: The total Python script

# 14.1.8 Using the Script from DTML

The following code could be used to add the numbers 10, 21, 35, 6, and 14:

`<html-var exp="total(10, 21, 35, 6, 14)\>`

The result of processing this code would be

86

As an exercise, you might try creating a form that allows the user to submit a list of numbers with an action that would call the total Python script and display the result. Here's a hint: If you create multiple input fields on a form with the same name and suffix it with `:int:list`, Zope will automatically convert the values to integers code and combine the contents of these fields into a list. For example, the input code could look something like the following:

```
<input type="text" name="values:int:list">
<input type="text" name="values:int:list">
<input type="text" name="values:int:list">
```

When submitted, this code would create a list of integers named "values" in the REQUEST object that could then be passed directly to the total script.

Scripting Zope with Python 269