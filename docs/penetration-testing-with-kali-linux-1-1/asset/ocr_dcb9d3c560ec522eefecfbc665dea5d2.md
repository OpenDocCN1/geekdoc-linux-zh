![](bbox=[0.23, 0.1, 0.77, 0.45])

Figure 249: Creating a Microsoft Word Macro

Let’s examine our simple macro (shown in Listing 392) and discuss the fundamentals of VBA. The main procedure used in our VBA macro begins with the keyword *Sub*<sup>353</sup> and ends with *End Sub*. This essentially marks the body of our macro.

> *A Sub procedure is very similar to a Function in VBA. The difference lies in the fact that Sub procedures cannot be used in expressions because they do not return any values, whereas Functions do.*

At this point, our new macro, *MyMacro()*, is simply an empty procedure and several lines beginning with an apostrophe, which marks the beginning of comments in VBA.

```
Sub MyMacro()
'    
' MyMacro Macro
'    
'    
End Sub
```

Listing 392 - Default empty macro

<sup>353</sup> (Microsoft, 2017), https://docs.microsoft.com/en-us/office/vba/Language/Concepts/Getting-Started/calling-sub-and-function-procedures