Reviewing the resulting message in the Inspector tool, we can see that our characters were not removed or encoded:

![](bbox=[0.13, 0.16, 0.87, 0.65])

Since the input is not filtered or sanitized, and our special characters have passed through into the output, the conditions look right for an XSS vulnerability. Let’s examine the source code to better understand what’s happening.

When feedback is submitted to the site, it is handled by the following code:

```
```php
36  <?php
37  include "database.php";
38  $sql = "INSERT INTO feedback(name, text) VALUES (?,?)";
39  $stmt = $conn->prepare($sql);
40  $stmt->bind_param("ss", $_POST['name'], $_POST['comment']);
41  $stmt->execute();
42  ?>
```
```

Line 40 in Listing 286 handles the values of the "name" and "comment" fields that are posted to the server. The code inserts those values into the database without any modification.