
## INHERIT FROM AN EXISTING CLASS

Just like a person often inherits traits of their parents, a class can inherit the traits of another class. To understand when to use class inheritance, think of the phrase "is a type of." For example, begin with the word mammal. A variety of animals inherit traits from mammals, such as cats and dogs. A cat is a type of mammal. A dog is a type of mammal as well.

After you create a base class, you define an inherited class with the Inherits statement. Place the keyword Inherits on a blank line at the top of a class followed by the name of the base class. Visual Basic .NET does not support multiple-inheritance, which means you can only inherit from one base class. You can, however, implement multiple interfaces. See Chapter 5 for more information on interfaces.

Public members of a base class become public members of the inherited class, meaning a user of the class can access

the base class members as if the inherited class contains them. Although it cannot access the base class's private members, the inherited class can access protected members of the base class when users of the class cannot.

You can override a method from the base class if the base class specifies the Overridable keyword in the declaration of a method. You override a base class's method by declaring a method of the same name in the inherited class with the Overrides keyword placed at the beginning of the line.

VB .NET only calls the latest descendant method in a set of classes. For example, assume the base class defines a method Calculate and an inherited class overrides the method. If you declare a variable in the type of the base class and assign an instance of the inherited class to the variable, VB .NET calls the inherited class's method.

![](img/d6f772854306e15fb6df39b861a7b541_197_0.png)

### CREATE THE BASE CLASS

- 1. Create an empty class block.
- 2. Type desired properties and events into the code block.

Note: See Chapter 7 for more information about creating a class, adding a property, and adding an event.

- 3. Type Overridable followed by Sub or Function on a new line inside the class.
- 4. Type a method name.
- 5. Type parameters in parentheses and a return type if the method is a Function.
- 6. Press Enter.
- 7. Add code to the method.

You can repeat steps 3 through 5 to create more base methods.

### Extra

When you override a method in the base class, you may want to access the underlying base method. This is especially useful if the code the base class contains needs to run in addition to the code you add in the overridden method. You can still access the base class's method by using the MyBase keyword. This keyword contains a reference to the original base class, enabling you to run any method available in the base class even if you override it.

Be careful when you make a method call using a class that you may later inherit. Because of Visual Basic .NET's bottom-most method of accessing overloaded methods, you may have a method in the base call a method in the inherited class. But if a class inherits from this class, the inherited class may overload the method, changing its functionality. You can make a method not support overriding by using the NotOverridable keyword. You can make sure a base class always calls its own method by using the MyClass object. This object maintains a reference to the class without using the bottom-most technique to determine the method to call.

### Example

```
Public Class BaseClass
    Public Overridable Sub Method1()
    End Sub
End Class
Public Class InheritedClass : Inherits BaseClass
    Public Overrides Sub Method1()
        MyBase.Method1()
    End Sub
End Class
```

![](img/d6f772854306e15fb6df39b861a7b541_198_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_198_1.png)

### CREATE THE INHERITED CLASS

- 8 Create a new empty class block.
- 9 Type Inherits followed by the base class name on the first line inside the class.
- 10 On a new line, type Overrides followed by Sub or Function, depending on the declaration of a method in the base class.
- 11 Type the name of the method you need to override. For a Function, use the same return type as the base method.
- 12 Press Enter.
- 13 Type code for the overridden method.

Your inherited class is ready for use.

Note: See Chapter 5 for information on using a class.
