being inserted into the database without being truncated or translated—or even causing the script to fail (which would have happened if someone had entered a string with double quotes in it).

Similar failures may occur if a user attempts to input data that’s incompatible with the type of column it’s supposed to go into. For instance, if *Age* is defined as an *INT* column, and a user enters “I’m not telling!” for his age, a value of zero will be entered; similarly, if a *VARCHAR* field is only 10 characters long, and the user enters a string longer than that, the string will be truncated upon insertion into the database. Still other conditions can cause the query operation to fail completely, returning an error, and the entire script will crash.

For this reason, it’s important to implement your own consistency-checking code in your script before the data gets to the database. For instance, you can ensure that data going into an *INT* column is a nonzero integer by putting it into a conditional loop, as shown here:

```
if (int($FORM['age']) {
  $udp h = $dbh->query ("UPDATE Users SET Age=‘$FORM[age]’ where id=‘$userid'");
} else {
  print “Error!”;
}
```

> **CAUTION**
> 
> Be aware that using single quotes around field names in associative array elements, such as `$FORM('age')`, won’t work in this kind of query (where the entire query string is double quoted and the field contents are single quoted). Perl lets you get away with leaving out the single quotes within the variable, as shown here, but this can be an invitation to trouble. It may be safer for you to reassign the contents of `$FORM('age')` to another variable (for instance, `$age`) before using it in the query.

Another safeguard is to use the *MAXLENGTH* attribute in your HTML form input fields. For instance, if the length of a *VARCHAR* column is 64 bytes, you can use the following HTML code for the corresponding form input field:

```
<INPUT NAME="fullname" MAXLENGTH="64">
```

This will prevent the user from entering any more than 64 characters, and you won’t have to worry about the input data getting truncated when it’s inserted.

Good coding practices dictate that error-trapping should be done as close as possible to the user. With Web-to-database programming, you’re dealing with three different layers of code separating the user from the data store: the front end (HTML and JavaScript), the *CGI* layer (Perl, Python, or C), and the back end (the database APIs and the built-in table-consistency safeguards). The best-designed Web applications have as much error-checking