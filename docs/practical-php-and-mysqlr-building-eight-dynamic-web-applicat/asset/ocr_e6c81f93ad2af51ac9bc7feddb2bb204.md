Please click on the following link to verify your new account:

```
$verify/?email=$verifyemail&verify=$verifystring

_MAIL_;
```

You construct the mail message by using *heredoc* syntax. This special technique allows you to use `<<` and an identifier (in this case, `_MAIL_`) to write a large chunk of text without requiring double quotes, single quotes, and new lines. The block ends when the identifier (`_MAIL_`) is added again. In the preceding snippet, the identifier is placed next to a variable declaration (`$mail_body`) to add the heredoc text to the variable. This is a useful method of adding large chunks of text to a variable.

![](bbox=[0.08, 0.37, 0.92, 0.39])

# Don’t Indent heredoc

When you use heredoc syntax, be sure to place the three angled brackets before the identifier (such as `<<IDENTIFIER`) and place both identifiers at the start of a line (unless there is a variable before it, as in code in this example).

Send the email:

```
_MAIL_;

mail($POST['email'], $config_forumsname . " User verification", $mail_body);
```

The `mail()` command sends the message. `mail()` has these three arguments:

+   - Email address
+   - Subject
+   - Body of the message

In this code, the email address from the form (`$POST_['email']`) is used as the first argument, the form name and *User Verification* are concatenated to make the subject, and finally the text from the heredoc syntax is added as the third argument.

Finally, display a message to indicate that the email has been sent:

```
mail($POST['email'],
$config_forumsname . " User verification", $mail_body);
```