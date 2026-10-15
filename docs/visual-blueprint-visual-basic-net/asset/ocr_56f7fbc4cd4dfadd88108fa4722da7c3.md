# Extra

You can easily convert numeric data to strings and strings back to numbers. For example, if you expect a user to type a number into a TextBox control, you know Text property returns a string with the contents of the number. You can convert the text into a number before processing. The CType function lets you convert any type of variable to another variable type. Pass the CType function to the variable, and provide the type to which you want to convert the variable. Although convenient to use because it accepts any sort of conversion, CType does not allow VB .NET to preprocess the conversion in the compiling process, and makes CType run very slow. Instead, VB .NET provides conversion function to every basic type. The CStr(var) function converts numeric, dates, and other simple data types into a string. CInt(var) converts a string or decimal number into an integer type. CDate(var) can take a string and convert it to a date according to locale preferences. You can search the VB .NET help system for "Type Conversion Functions" for a complete overview.

```
Example:
Dim myNumber As Integer = CType(TextBox1.Text, Integer)
myNumber = CInt(TextBox2.Text)
Dim myString As String = CStr(myNumber)
```

![](bbox=[0.07, 0.48, 0.48, 0.78])

![](bbox=[0.52, 0.48, 0.93, 0.78])

# ACCESS CHARACTERS

6 Type Dim myChar As Char = myString.Chars(2), replacing myChar with a string variable's name, and 2 with a character index.

7 Type display or manipulation code

8 Press F5 to run the project.

You see a string variable function and display its contents.