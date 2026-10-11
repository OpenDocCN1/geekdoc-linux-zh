
## Display member ID as static text

```php
display_column ("Member ID", $row, "member_id", FALSE);

# $admin is true if the user provided the administrative password,
# false otherwise. Administrative users can edit the expiration
# date, regular users cannot.

display_column ("Expiration", $row, "expiration", $admin);

# Display other values as editable text

display_column ("Last name", $row, "last_name");
display_column ("First name", $row, "first_name");
display_column ("Suffix", $row, "suffix");
display_column ("Email", $row, "email");
display_column ("Street", $row, "street");
display_column ("City", $row, "city");
display_column ("State", $row, "state");
display_column ("Zip", $row, "zip");
display_column ("Phone", $row, "phone");
display_column ("Interests", $row, "interests");

print ("</table>\n");

submit_button ("button", "Submit");
print  "</form>\n";

}
```

The first thing that `display_entry()` does is to verify the password. If the password supplied by the user matches the password stored in the `member_pass` table for the given member ID, or if it matches the administrative password (that is, the password for the special member ID `0`), `edit_member.php` displays the entry in a form so that its contents can be edited. The password-checking function `check_pass()` runs a simple query to yank a row from the `member_pass` table and compare its password column value to the password supplied by the user in the login form:

```php
function check_pass ($dbh, $id, $pass)
{
  $stmt = "SELECT password FROM member_pass WHERE member_id = ?";
  $sth = $dbh->prepare ($stmt);
  $sth->execute (array ($id));
  # TRUE if a password was found and it matches
  return (($row = $sth->fetch ()) && $row ["password"] == $pass);
}
```

Assuming that the password matches, *display_entry()* looks up the row from the member table corresponding to the given member ID, and then goes on to generate an editing form initialized with the values from the row. Most of the fields are presented as editable text fields so that the user can change them, but there are two exceptions. First, the member_id value is displayed as static text. This is the key value that uniquely identifies the row, so it should not be changed. Second, the expiration date is not something that we want League members to be able to change. (They'd be able to push the date farther into the future, in effect renewing their memberships without paying their dues.) On the other hand, if the administrative password was given at login time, the script does present the expiration date in an editable field. Assuming that the League secretary knows this password, this enables the secretary to update the expiration date for members who renew their memberships.

The *display_column()* function handles display of field labels and values. Its arguments are the label to display next to the field value, the array that contains the row to be edited, the name of the column within the row that contains the field value, and a boolean value that indicates whether to present the value in editable or static form. The last value is optional, with a default value of TRUE:

```php
function display_column ($label, $row, $col_name, $editable = TRUE)
{
    print ("<tr>\n");
    print ("<td>" . htmlspecialchars($label) . "</td>\n");
    print ("<td>");
    if ($editable) # display as editable field
        text_field ("row[$col_name]", $row[$col_name], 80);
    else              # display as read-only text
        print (htmlspecialchars ($row[$col_name]));
    print ("</td>\n");
    print ("</tr>\n");
}
```

For editable values, *display_column()* generates text fields using names that have the format row[col_name]. That way, when the user submits the form, PHP will place all the field values into an array variable, with elements keyed by column name. This makes it easy to extract the form contents and to associate each field value with its corresponding member table column when we update the row in the database. For example, by fetching the array into a $row variable, we can access the telephone number as $row['phone'].

The *display_entry()* function also embeds the *member_id* and *password* values as hidden fields in the form so that they will carry over to the next invocation of *edit_script.php* when the user submits the edited entry. The ID enables the script to determine which member table row to update, and the password enables it to verify that the user logged in before. (Notice that this simple authentication method involves passing the password back and forth in clear text, which isn't generally such a great idea. But the Historical League is not a high-security organization, so this method suffices for our purposes. Were you performing operations such as financial transactions, you'd certainly use a more secure form of authentication.)

The function that updates the membership entry when the form is submitted looks like this:

```php
function update_entry ($dbh)
{
    # Get script parameters; trim whitespace from the ID, but not
    # from the password, because the password must match exactly,
    # or from the row, because it is an array.

    $member_id = trim (script_param ("member_id"));
    $password = script_param ("password");
    $row = script_param ("row");

    $member_id = trim ($member_id);
    if (empty ($member_id))
        die ("No member ID was specified\n");
    if (!ctype_digit ($member_id))    # must look like integer
        die ("Invalid member ID was specified (must be an integer)\n");
    if (!check_pass ($dbh, $member_id, $password)
        && !check_pass ($dbh, 0, $password))
        die ("Invalid password\n");

    # Examine the metadata for the member table to determine whether
    # each column allows NULL values. (Make sure nullability is
    # retrieved in uppercase.)

    $stmt = "SELECT COLUMN_NAME, UPPER(IS_NULLABLE)
            FROM INFORMATION_SCHEMA.COLUMNS
            WHERE TABLE_SCHEMA = ? AND TABLE_NAME = ?";
    $sth = $dbh->prepare ($stmt);
    $sth->execute (array ("sampdb", "member"));
    $nullable = array ();
    while ($info = $sth->fetch ())
        $nullable[$info[0]] = ($info[1] == "YES");

    # Iterate through each field in the form, using the values to
    # construct an UPDATE statement that contains placeholders, and
    # the array of data values to bind to the placeholders.

    $stmt = "UPDATE member ";
    $delim = "SET";
    $params = array ();
    foreach ($row as $col_name => $val)
    {
        $stmt .= "$delim $col_name=?";
        $delim = ",";
        # if a form value is empty, update the corresponding column value
        # with NULL if the column is nullable. This prevents trying to
        # put an empty string into the expiration date column when it
        # should be NULL, for example.
        $val = trim ($val);
        if (empty ($val))
        {
            if ($nullable[$col_name])
                $params[] = NULL; # enter NULL
            else
                $params[] = "";  # enter empty string
        } else
            $params[] = $val;
    }
    $stmt .= " WHERE member_id = ?";
    $params[] = $member_id;

    $sth = $dbh->prepare ($stmt);
    $sth->execute ($params);
    printf ("<br /><a href=\"%s\">Edit another member record</a>\n", script_name ());
}
```

First we re-verify the password to make sure someone isn't attempting to hoax us by sending a faked form, and then we update the entry. The update requires some care because if a field in the form is blank, it may need to be entered as NULL rather than as an empty string. The expiration column is an example of this. Suppose that the League secretary logs in with the administrative password (so that the expiration field is editable) and clears the field to indicate “lifetime membership.” This should correspond to a NULL membership expiration date in the database, not an empty string (which isn't a legal date). Therefore, it's necessary to be able to tell which columns can take NULL values and insert NULL (rather than an empty string) when such a column is left blank in the form.

To handle this problem, update_entry() looks up the metadata for the member table and constructs an associative array keyed on column name that indicates which columns can have NULL values and which cannot. This information is available in the COLUMNS table of the INFORMATION_SCHEMA database. The values that we need from the table are the column name and whether it allows NULL values (that is, the COLUMN_NAME and IS_NULLABLE values).

At this point, the edit_member.php script is finished. Install it in the web directory of the web document tree, let the members know their passwords, and they’ll be able to update their own membership information over the Web.
