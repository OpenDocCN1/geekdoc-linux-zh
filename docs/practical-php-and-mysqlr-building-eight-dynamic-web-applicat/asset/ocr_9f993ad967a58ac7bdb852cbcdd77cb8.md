```
<table>
<tr>
<td>Project Name</td>
<td><input type="text" name="name" value="<?php echo $row['name'] ?>"></td>
</tr>
<tr>
<td>Path Name</td>
<td><input type="text" name="pathname" value="<?php echo $row['pathname'] ?>"></td>
</tr>
<tr>
<td>Description</td>
<td><textarea name="about" rows="10" cols="50"><?php echo $row['about'] ?></textarea></td>
</tr>
<tr>
<td></td>
<td><input type="submit" name="submit" value="Modify details"></td>
</tr>
</table>
</form>

<?php }
?>
```

When the form is processed, the information is added to the *homeproject_projects* table.

# Deploying the Application

Throughout the development of this project, the code has been developed in something of a vacuum. Sitting in its own dedicated directory, the project has not been put to the test inside an existing Web application.

To test how easily it embeds into an existing project, copy the Generic Web site project (from Chapter 3, “Web Site Design”) to a directory called *genericwithprojects*. Now copy all of the project code to a subdirectory inside *genericwithprojects* called *projects*.

The first step is to adjust *phphomeprojectconfig.php* for the new settings, as shown in Example 10-12.