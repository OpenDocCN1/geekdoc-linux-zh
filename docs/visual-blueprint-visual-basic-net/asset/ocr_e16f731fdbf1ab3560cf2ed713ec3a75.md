# Apply It

You can use properties of a RegistryKey object to list the available subkeys and values associated with the key. The SubKeyCount property returns the number of subkeys the particular key contains and the ValueCount property returns the number of values associated with the key. Use the GetSubKeyNames method to return an array of strings representing the names of the available subkeys. To get the values associated with a key, use the GetValueNames method to return an array of strings representing the available values.

# TYPE THIS:

```
Dim regKey As RegistryKey = Registry.LocalMachine.OpenSubKey("SOFTWARE")
Dim keyName As String, valueName As String

Console.WriteLine("Sub Keys:")
For Each keyName In regKey.GetSubKeyNames()
    Console.Write(keyName & ", ")
Next

Console.WriteLine(ControlChars.CrLf & "Values:")
For Each valueName In regKey.GetValueNames()
    Console.Write(valueName & ", ")
Next
Console.ReadLine()
```

# RESULT:

Sub Keys:
Classes, Clients,
Microsoft, ODBC,
Program Groups, Secure,
Windows 3.1 Migration
Status,

Values:
Description,

![](bbox=[0.07, 0.525, 0.475, 0.835])

![](bbox=[0.505, 0.525, 0.955, 0.835])

8 To save changes, type the registry key followed by .Flush().

9 To read a key, type the variable name of the key to access, then .GetValue, and then the name of the value to retrieve in parentheses.

The application adds and retrieves values from the registry.

10 Press F5 to run your project.