
# Apply It

You can use the ByVal and ByRef keywords to manipulate how VB .NET passes information to your method. The keyword ByVal stands for by value, and means that VB .NET creates a copy of the data passed into the method for the method to use. The ByRef keyword stands for by reference, and means that VB .NET sends the actual location in memory of the variable passed into the method. Because you work with the original variable when you use the ByRef keyword, VB .NET maintains changes you make to the value when the method exits.

## TYPE THIS:

```
Sub AddNumber(ByRef number1 As Integer, ByVal number2 As Integer)
' make number1 ByRef so you can change the value
number1 += number2
End Sub

Sub Main()
Dim x As Integer = 10, y As Integer = 15
Console.WriteLine("The value of x is : " & CStr(x))
AddNumber(x, y)
Console.WriteLine("The value of x is : " & CStr(x))
Console.ReadLine()
End Sub
```

## RESULT:

The value of x is: 10
The value of x is: 25

![](img/d6f772854306e15fb6df39b861a7b541_112_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_112_1.png)

## PASS A RETURN VALUE

- 7 Change the Sub keyword in the method declaration to Function.
- 8 At the bottom of the method code, type the keyword Return.
- 9 Type the expression to return.
- 10 Assign the method to a variable and process the result.
- 11 Press F5 to run the project.

The method passes data back and forth to the code that calls it.

# USING THE IF STATEMENT

You can use conditional statements when you run different code based on specific conditions. The most frequently used conditional block relies on the If statement.

For example, if you want to display a message based on a calculation that determines the temperature, you can qualify anything over 80 degrees as hot, and any other temperature as too cold. This calls for a test of the temperature value to determine into which range it falls.

The If statement tests a conditional statement you provide, and runs a block of code if it is True. If the statement is False, VB .NET skips over the block of If code. For more information on forming conditional statements, see "Work with Operators."

The format for an If statement is If expression Then. You can place code to execute if the conditional statement is true on the same line. If you have more that you need to execute, you can start the code on the next line and enclose the statements with an End If statement.

is true on the same line. If you have more that you need to execute, you can start the code on the next line and enclose the statements with an End If statement.

In the case you want to provide code when the condition is False, you can insert an Else statement between the If...Then and End If statements. If the condition is False, the code jumps to the code located between the Else and the End If instead of the code directly after the If.

To make your code easier to understand, you can line up the If, Else, and End If statements with the rest of the code in your method. You can then indent the blocks of code inside the statements. This capability enables you to identify blocks of code easily. The Development Studio provides the smart tab feature, which automatically indents your code, and the environment enables this option by default.

# USING THE IF STATEMENT

![](img/d6f772854306e15fb6df39b861a7b541_113_0.png)

- 1. Create a new project or open an existing one.
- 2. Create or open the method where the test needs to execute.
- 3. Type any initialization code necessary before the test begins.
- 4. Type If x < 5 Then, replacing x < 5 with the conditional statement you want to use.
- 5. Press Enter to move to the next line. VB .NET adds End If automatically.

# Apply It

You may need to test a significant amount of different conditions at a time. Using the If...Else...End If structure, you can create a large quantity of code because you must place If blocks inside other If blocks. You use the ElseIf statement to create more advanced If blocks. You must place ElseIf inside of an If and any condition after an ElseIf statement followed by a Then. The code runs if the condition is True until it reaches an Else, Else, or End If. You can place the following code in a Console Application in Sub Main.

## TYPE THIS:

```
' change these values for different results
Dim x As Integer = 5
Dim y As Integer = 10

If x > 4 And y < 10 Then
    Console.WriteLine("Result 1 occurred.")
ElseIf x < 6 And y > 9 Then
    Console.WriteLine("Result 2 occurred.")
ElseIf x = 3 And y = 2 Then
    Console.WriteLine("Result 3 occurred.")
Else
    Console.WriteLine("No If matched.")
End If
Console.ReadLine()
```

## RESULT:

Result 2 occurred.

![](img/d6f772854306e15fb6df39b861a7b541_114_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_114_1.png)

- 6 Type code to run if the condition is True.
- 7 To run code when the condition specified in the If statement fails, type Else on a new line.
- 8 Type code for the Else condition.
- 9 Press F5 to run the project.

The If statement runs the appropriate code based on the condition.
