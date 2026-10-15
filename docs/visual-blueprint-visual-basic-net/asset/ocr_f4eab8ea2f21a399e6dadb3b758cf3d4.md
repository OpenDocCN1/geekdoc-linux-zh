# Apply it

The Join & Split method, part of the String class, enable you to concatenate an array of strings or break them up, respectively. You can use these methods to easily store a set of information in a single string and break it apart when necessary. For more information on creating and using arrays, see “Create an Array” later in this chapter. To combine an array of strings, pass the String.Join method the string to use as a separator and a string array. You place a separator between each adjacent item in the array. A common string to use is a comma followed by a space. To combine a set of words into a sentence, simply use a space as the separator. The Split function breaks apart a string and returns a string array. Pass the Split function a string followed by a separator. If you do not pass a separator, Split uses a space.

```
Dim words() As String = {"The", "car", "is", "going", "fast."}
Dim sentence As String
sentence = String.Join(" ", words)
Console.WriteLine(sentence)
Dim splitSentence() As String = Split(sentence, " ")
Dim word As String
For Each word In splitSentence
Console.Write(word & " ")
Next
```

The car is going fast.
The car/is/going/fast./

![](bbox=[0.05, 0.6, 0.48, 0.85])

![](bbox=[0.52, 0.6, 0.95, 0.85])

+   5 On a new line, type myStringChanges = myString.Insert(14, "TONS OF "), replacing myString with the name of the string you want to manipulate, Insert with the manipulation method, and 14, "TONS OF " with the appropriate arguments.
+   6 Type code to use the manipulated string.
+   7 Press F5 to run your project.

The String class alters the string data and your program uses the changes.