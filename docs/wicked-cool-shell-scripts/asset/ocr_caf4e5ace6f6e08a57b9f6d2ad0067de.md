# Adding a Footer of Actions to Take

The script also relies on the presence of an HTML file called apm-footer.html containing occurrences of the strings --myname-- and --options-- ① which are replaced by the current name of the CGI script and the list of users, respectively, as the file is output to stdout.

The $myname variable is processed by the CGI engine, which replaces the variable with the actual name of the script. The script itself builds the $optionstring variable from the account name and password pairs in the .htpasswd file at ②

The HTML footer file in Listing 9-8 provides the ability to add a user, update a user's password, and delete a user.

```
<!-- footer information for APM system. -->

<div style='margin-top: 10px;'>
<table border='1' cellpadding='2' cellspacing='0' width='80%'
style="border:2px solid #666;border-radius:5px;">
<tr><th colspan='4' bgcolor='#cccccc'>Password Manager Actions</th></tr>
<form method="get" action="--myname--">
<table border="0">
<tr><td><input type='hidden' name='a' value='A'>
add user:<td><td><input type='text' name='u' size='15'>
</td></tr><tr><td>
password: <td><td><input type='text' name='p' size='15'>
</td></tr><tr><td colspan='2' align="center">
<input type='submit' value='add' style="background-color:#ccf;">
</td></tr>
</table></form>
</td><td>
<form method="get" action="--myname--">
<table border="0">
<tr><td><input type='hidden' name='a' value='U'>
update:<td><td><select name='u'>--options--</select>
</td></tr><tr><td>
password: <td><td><input type='text' name='p' size='10'>
</td></tr><tr><td colspan='2' align="center">
<input type='submit' value='update' style="background-color:#ccf;">
</td></tr>
</table></form>
</td><td>
<form method="get" action="--myname--"><input type='hidden'
name='a' value='D'>delete <select name='u'>--options--</select>
<br /><br /><center>
<input type='submit' value='delete' style="background-color:#ccf;"></center>
</form>
</td></tr>
</table>
</div>

<h5 style='background:#ccf;border-radius:3px;border:1px solid #99c;padding:3px;'>
```