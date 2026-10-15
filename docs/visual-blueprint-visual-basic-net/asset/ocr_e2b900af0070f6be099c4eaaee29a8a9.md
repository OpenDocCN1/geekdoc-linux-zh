# Extra

The Attributes property consists of a bit-wise combination of constants from the FileAttributes enumeration. You can use the Attributes property to test a file for particular attributes. To test a file, use the And operator combined with a constant. To set the attributes for a file, combine multiple attributes with the Or operator and assign the value to the Attributes property. A table of the most important constants in FileAttributes appears here. See Visual Basic .NET help for the full list.

# FILEATTRIBUTE CONSTANTS:

| NAME | DESCRIPTION |
|---|---|
| Archive | Applications use this attribute to mark files for backup or removal. |
| Directory | A folder or directory. |
| Hidden | Ordinary directory listings do not list this file. |
| Normal | The file is normal and has no other attributes set. |
| ReadOnly | You cannot write to this file. |
| System | The file is part of the operating system. |

# Example:

```
Dim file As New IO.FileInfo("c:\test.txt")
' assign attributes
file.Attributes = IO.FileAttributes.Hidden Or IO.FileAttributes.Archive
Dim test As Boolean
' check attributes
test = file.Attributes And IO.FileAttributes.Hidden
```

![](bbox=[0.07, 0.5, 0.92, 0.8])

7 To perform an action on the file, type myFile.CopyTo ("C:\NewTest.txt"), replacing myFile with the variable name assigned to the FileInfo class, and "C:\NewTest.txt" with the destination for the CopyTo.

Alternatively, you can replace CopyTo in step 7 with Delete or MoveTo.

8 Press F5 to run your project.

The FileInfo class modifies file properties, accesses file properties, and uses methods to perform disk operations.