Inside this block an INSERT statement adds the form data to the database. Add the else that encases the main form:

```
header("Location: " . $config_basedir);
}

else {
require("header.php");
?>
<h1>Add a new subject</h1>
<form action="<?php echo $SCRIPT_NAME; ?>" method="post">
Finally, after the form, close the else and add the footer file:
</table>
</form>

<?php
}
require("footer.php");
?>
```

The completed page should look like the one shown in Figure 9-14.

![](bbox=[0.09, 0.61, 0.44, 0.72])

# ### Deleting Subjects

When logged in as an administrator, a user deletes content by clicking the little *X* links. These links hook up with a page to delete the type of content the *X* is next to. If you take a look at the list of subjects, you will see that the *X* next to each subject links to *deletesubject.php* and passes the script the id of the subject to be deleted.