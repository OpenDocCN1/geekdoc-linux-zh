```
```text
<?
<h3>Leave a comment</h3>
<form action="<?php echo $SCRIPT_NAME
        . "?id=" . $validentry; ?>" method="post">
<table>
<tr>
    <td>Your name</td>
    <td><input type="text" name="name" /></td>
</tr>
<tr>
    <td>Comments</td>
    <td><textarea name="comment" rows="10" cols="50"></textarea></td>
</tr>
<tr>
    <td></td>
    <td><input type="submit" name="submit" value="Add comment" /></td>
</tr>
</table>
</form>
```
```

This code creates a table that contains a number of form elements. In the  <form> tag, *action* specifies the page that will process the data from this form. As shown here, you can use a special PHP variable called *SCRIPT_NAME* to reference the name of the current file (in this case, *viewentry.php*). This reference is useful if you later decide to change the filename of your script; you then don’t need to change your code. The *method* attribute in the tag indicates whether you want to submit your variables as POST or GET variables.

Inside the *action* attribute, the *validentry* variable is added as a GET variable. When you process the data from the form, you need to indicate the ID of the blog entry to which you are posting the comment.

The HTML in the preceding form itself is pretty self-explanatory.

# **NOTE**

# **GET Variables Versus Hidden Form Fields**

Another technique of sharing a variable between the form and the script that processes it is to use the hidden form element:

```
```text
<input type="hidden" name="example" value="21" />
```
```

The value attribute of the form can then be accessed as a normal variable with _GET or _POST in your PHP code.