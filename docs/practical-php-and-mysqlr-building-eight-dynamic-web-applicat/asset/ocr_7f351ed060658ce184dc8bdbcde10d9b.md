NOTE

# Get the Right Submit Button

The Submit button in the form is named *versubmit*. This page has two Submit buttons (one for the version and one for the releases), and you need to be able to distinguish which one is clicked.

```
echo "</td></tr>";

if($vernumrows == 0) {
  echo "<tr><td colspan=2>This project has no versions or releases.</td></tr>";
}
```

If no rows are present, a message indicates that no versions or releases exist. If rows are present, display them:

```
echo "<tr><td colspan=2>This project has no versions or releases.</td></tr>";
} else {
  while($vverrow = mysql_fetch_assoc($verresult)) {
    echo "<tr>";
    echo "<td><strong>" . $verrow['version'] . "</strong></td>";
    echo "<td>";
```

```
$relesql = "SELECT homeproject_releasefiles.id, homeproject_releasefiles.filename, homeproject_releasefiles.date, homeproject_releasetypes.type FROM homeproject_releaseversions INNER JOIN homeproject_releasefiles ON homeproject_releasefiles.version_id = homeproject_releaseversions.id INNER JOIN homeproject_releasetypes ON homeproject_releasetypes.type_id = homeproject_releasetypes.id WHERE homeproject_releaseversions.id = '" . $verrow['id'] .
"';
$relresult = mysql_query($relesql);
$relnumrows = mysql_num_rows($relresult);
```

In this case, you add the version number in the first cell and then run a query to gather the releases available for that version. This query returns the *id*, *filename*, *date*, and *type* for each version by performing an inner join to hook together the *homeproject_releaseversions*, *homeproject_releasefiles*, and *homeproject_releasetypes* tables.

Check if any releases are returned and display them accordingly:

```
$relnumrows = mysql_num_rows($relresult);

if($relnumrows == 0) {
```