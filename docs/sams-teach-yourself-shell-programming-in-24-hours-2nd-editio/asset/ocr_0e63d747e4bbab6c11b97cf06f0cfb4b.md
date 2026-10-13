Look at the flow of control through this statement:

+   1. First, the command
+   `uencode cherry.gif cherry.gif > cherry.uu`
+   is executed.
+   2. If this command is successful, the command
+   `echo "Encoded cherry.gif to cherry.uu"`
+   is executed and the if statement exits.
+   3. Otherwise the command
+   `echo "Error encoding cherry.gif"`
+   is executed, and the if statement exits.

You might have noticed that both the if and then statements appear on the same line in this example. Most shell programmers prefer to write if statements this way in order to make the statement more concise and readable.

# Common Errors

Four common errors that can occur when using the if statement are

+   - Omitting the semicolon (`;`) before the then statement in the single line form.
+   - Using else if or elseif instead of elif.
+   - Omitting the then statement when an elif statement is used.
+   - Writing if instead of fi at the end of an if statement.

The error message generated in each of these cases varies from system to system. In the following examples, a typical error message is displayed; the actual error message on your system may use slightly different wording.

The following example illustrates the first type of error:

```
if uencode cherry.gif cherry.gif > cherry.uu then
echo "Encoded cherry.gif to cherry.uu"
else
echo "Error encoding cherry.gif"
fi
```