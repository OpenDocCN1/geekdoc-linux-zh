Create *checkout-address.php* and add the form:

```
```php
require("header.php");
echo "<h1>Add a delivery address</h1>";

if(isset($_GET['error']) == TRUE) {
    echo "<strong>Please fill in the missing information from the form</strong>";
}

echo "<form action=" . $SCRIPT_NAME . " method='POST'>";

if($_SESSION['SESS_LOGGEDIN'])
{
?>
    <input type="radio" name="addselectBox" value="1" checked>Use the address from my account</input><br>
    <input type="radio" name="addselectBox" value="2">Use the address below:</input>
<?php
}
?>
    <table>
        <tr>
            <td>Forename</td>
            <td><input type="text" name="forenameBox"></td>
        </tr>
        <tr>
            <td>Surname</td>
            <td><input type="text" name="surnameBox"></td>
        </tr>
        <tr>
            <td>House Number, Street</td>
            <td><input type="text" name="addlBox"></td>
        </tr>
        <tr>
            <td>Town/City</td>
            <td><input type="text" name="add2Box"></td>
        </tr>
        <tr>
            <td>County</td>
            <td><input type="text" name="add3Box"></td>
        </tr>
        <tr>
            <td>Postcode</td>
            <td><input type="text" name="postcodeBox"></td>
        </tr>
        <tr>
            <td>Phone</td>
            <td><input type="text" name="phoneBox"></td>
```
```