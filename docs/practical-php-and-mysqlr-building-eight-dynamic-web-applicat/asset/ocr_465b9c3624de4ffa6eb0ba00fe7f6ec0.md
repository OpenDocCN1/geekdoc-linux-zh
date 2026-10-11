```
$verifyemail = urlencode($_POST['email']);
$validusername = $_POST['username'];
```

These variables store different types of information, which is added to the verification URL. The first variable ($verifyurl) contains the location of the verification page, which you need to change to something relevant to your setup. The second variable ($verifystring) uses urlencode() to convert $randomstring into something that can be added to the address bar as a GET variable. The third variable uses urlencode() on the email address, and the final variable stores the username.

> **NOTE**
> 
> **Using urlencode()**
> 
> The urlencode() function ensures that a string can be used as a GET variable on the URL. In addition to urlencode() is the urldecode() function, which converts the encoded string back into its original form.

Create a SQL query to insert the username, password, email address, and verifystring in the database while also setting the active field to 0 (inactive):

```
$validusername = $_POST['username'];

$sql = "INSERT INTO
  users(username, password, email, verifystring,
  active) VALUES("
. $_POST['username']
. ", '
. $_POST['password1']
. "', '
. $_POST['email']
. "', addslashes($randomstring)
. ', 0)";
mysql_query($sql);
```

Construct the email to send to the user for verification:

```
mysql_query($sql);

$mail_body=<<< MAIL_

Hi $validusername,
```