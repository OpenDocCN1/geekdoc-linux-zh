When the form is displayed, the select box contains a list of the types from the `homeproject_releasetypes` table. The Submit button is called `relsubmit` so that you can determine whether the user clicked the version or release Submit button.

Close the remaining code:

```
echo "<a href=\"" . $SCRIPT_NAME
. "?func=downloads&addrelver=\" . $verrw['id']
. "">Add a New Release</a>";
}
echo "</td>";
echo "</tr>";
}
echo "</table>";
}
```

With the main interface portions complete, you can focus on processing the form. Jump to the start of the file and begin adding the code:

```
<?php
require_once('../project_functions.php');
pf_protect_admin_page();

$upload_dir = $config_projectdir . $_SESSION['SESS_PROJECTPATH']
. "/releases/";
```

After protecting the page, you set a variable called `$upload_dir`. This variable specifies the location where releases are uploaded. You want to upload files to the `releases` directory inside the project directory so that you can concatenate the `$config_projectdir` and `SESS_PROJECTPATH` variables and then add the `releases` directory.

Begin processing the version form:

```
$upload_dir = $config_projectdir . $_SESSION['SESS_PROJECTPATH']
. "/releases/";
if($_POST['versubmit']) {
  $adds q1 = "INSERT INTO homeproject_releaseversions(project_id,
  version) VALUES("
  . $_SESSION['SESS_PROJECTID']
  . ", '" . $_POST['version'] . "')";
  mysql_query($addsql);
  header("Location: " . $config_projectadminbasedir
  . basename($SCRIPT_NAME) . "?func=downloads");
}
```