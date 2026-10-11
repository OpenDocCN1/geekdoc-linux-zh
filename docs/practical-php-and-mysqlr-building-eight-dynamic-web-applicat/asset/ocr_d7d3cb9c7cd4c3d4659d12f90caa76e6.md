```
```
} elseif(!@getimagesize($FILES['userfile']['tmp_name'])) {
    header("Location: " . $HOST_NAME . $SCRIPT_NAME
. "?func=screenshots&error=invalid");
    mysq1_query("$inssql");
}
else {
    $uploaddir = $config_projectdir . $SESSION['SESS_PROJECTPATH']
. "/screenshots/";
    $uploadfile = $uploaddir . $FILES['userfile']['name'];
    if(move_uploaded_file($FILES['userfile']['tmp_name'],
$uploadfile)) {
        $inssql = "INSERT INTO homeproject_screenshots(project_id,
name) VALUES(" . $SESSION['SESS_PROJECTID'] . ", "
. $FILES['userfile']['name'] . ")";
        mysq1_query($inssql);
    }
    header("Location: " . $HOST_NAME . $SCRIPT_NAME
. "?func=screenshots");
}
else {
    echo 'There was a problem uploading your file.<br /r';
}
}
```
```

The code runs the uploaded image through the checks and then copies it to the upload directory (the *screenshots* directory in the current project's path). The page finally redirects to the same page.

Add the else, but before you display the form, run a query to display the existing screenshots:

```
```
}
}
else {
    $imagesq1 = "SELECT * FROM homeproject_screenshots WHERE project_id = " . $SESSION['SESS_PROJECTID'] . ";";
    $imagesresul = mysql_query($imagesq1);
    $imagesnumrows = mysql_num_rows($imagesresul);
    echo "<h1>Current images</h1>";
    
    if($imagesnumrows == 0) {
        echo "No images.";
    }
    else {
        echo "<table>";
        while($imagesrow = mysql_fetch_assoc($imagesresult)) {
            echo "<tr>";
            echo "<td><img src=" . $config_projecturl . $SESSION['SESS_PROJECTPATH'] . "/screenshots/" . $imagesrow['name'] . " width="100"></td>";
```
```