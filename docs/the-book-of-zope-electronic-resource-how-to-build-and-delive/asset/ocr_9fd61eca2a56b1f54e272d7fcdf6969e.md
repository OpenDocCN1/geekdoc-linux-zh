Annotated text does not appear as a comment in the source text in the third tier. Use the standard HTML comment if you want it to appear in the rendered source.

The comment tag accepts no attributes.

Unfortunately, the comment tag does not completely ignore DTML tags placed inside its body. Although no code inside a comment is ever executed, it must still be well formed and balanced for the DTML parser to accept the document. Because of this, it is not possible to comment out the start of a dtml block (a dtml-ij block, for example).

# 4.3.15 The try and the except Tags

You may wish to access a variable even though you do not know whether it has been defined or whether you can consult it. If you try to access a non-existent variable, Zone will generate an error message, just as a faulty expression is called. You might also be making a call that relies on an external system that could fail, as sending an email as above. These operations can be a problem in certain circumstances because the error message prevents you from displaying a document in the third tier.

Use the try and except tags to bypass error messages. The try tag is a non-empty tag and accepts no attributes. It contains the instructions to be carried out but which may generate a Zone error. It can also include one or more except tags, which may contain alternative instructions to be carried out. The except accepts an optional attribute that identifies the type of error traps. If the attribute is omitted, the except block traps all errors not already trapped above it.

The following structure is used:

```
<dtml-try>
  Instructions that can fail or cause errors
  <dtml-except>
    Instructions to handle the error or exception case Error
  <dtml-except>
    Instructions to handle any other errors.
</dtml-try>
```

For example, say we have a variable that we want to use as a divisor in an expression and we want to trap any errors caused by the expression tries to divide by zero. To trap the error and bypass a Zone error message, use the try tag as follows:

```
<dtml-try>
  The result is: <dtml-var expr="100/x">
  <dtml-except-DivideByZeroError>
    The result could not be displayed.
</dtml-try>
```

The code above bypasses the error message so that the remainder of the document can be displayed. The person viewing the document is informed that the result could not be displayed.