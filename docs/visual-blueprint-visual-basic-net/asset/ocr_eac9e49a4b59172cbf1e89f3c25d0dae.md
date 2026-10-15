# Apply It

Often, you need to sort a column of data while keeping another column of data properly in line with it. For example, if you have two arrays, one with last names and one with first names, you need to sort based on last name while keeping the first names together with the last names. The Sort method provides an alternative set of parameters to do this. Pass the array to sort followed by the second array, and Sort sorts the first array. Sort reorders the secondary array as it sorts.

```
Dim firstName() As String = {"John", "Sally", "Chris"}
Dim lastName() As String = {"Normal", "Peck", "Cross"}
Dim x As Integer

For x = 0 To 2                  ' display the initial arrays
    Console.WriteLine(lastName(x) & ", " & firstName(x))
Next

Array.Sort(lastName, firstName)  ' sort the two arrays based on last names

For x = 0 To 2                  ' display the results
    Console.WriteLine(lastName(x) & ", " & firstName(x))
Next

Console.ReadLine()
```

**RESULT:**

Normal, John  
Peck, Sally  
Cross, Chris  

Cross, Chris  
Normal, John  
Peck, Sally

![](bbox=[0.071, 0.51, 0.944, 0.799])

# FIND A VALUE IN THE ARRAY

+   6. Type index = `Array.BinarySearch(myArray, “Megan”)`, replacing index with an integer variable name, myArray with the name of your array, and “Megan” with the key string.

+   7. Type code to work or display the results.

+   The example above prints the index of the located item.

+   8. Press F5 to run your project.

+   The Array object modifies and searches your array.