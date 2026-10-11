```
$row = mysql_fetch_assoc($result);
echo "<h1> " . $row['subject'] . " </h1>";
echo date("D jS F Y g:iA", strtotime($row['dateposted'])) . " <br />";
echo n12br($row['body']);
```

When displaying the information, the date is formatted into a readable state and the n12br() function converts empty lines in the body text to `<br>` tags. This conversion ensures that the blank lines in the original text are retained.

When a story is rated, the ratings table stores the score. Using this table, get the number of ratings as well as the average rating for the story:

```
echo date("D jS F Y g:iA", strtotime($row['dateposted'])) . " <br />";
echo n12br($row['body']);
```

```
$avgsql = "SELECT COUNT(id) AS number, AVG(rating) AS avg FROM ratings WHERE story_id = " . $validid . ";";
$avgresult = mysql_query($avgsql);
$avgrow = mysql_fetch_assoc($avgresult);

echo "<p>";
echo "<strong>Rating:</strong> ";
```

This query uses the COUNT() and AVG() MySQL functions to return the number of votes and the average. The AVG() function returns the average of the field that you specify. In this case, you want the average of the ratings field.

There is a good possibility that not every story has a rating, however, so you need to account for this:

```
echo "<p>";
echo "<strong>Rating:</strong> ";
if($avgrow['number'] == 0) {
    echo "No ratings!";
}

If ratings exist, round the average up or down as necessary:
```

```
echo "No ratings!";
}
else {
    $a = (round($avgrow['avg'] * 2) / 2)
```

This line rounds the average with round(), multiplies the result by 2, and then divides by 2 to determine the final rating. This simple little mathematical trick is a good way to get the final value.