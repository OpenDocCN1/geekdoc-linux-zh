```
echo "<a href='adminmodquestions.php?func=main'>&lArr;Back to questions</a>";
echo " &bull;";
echo "<a href='adminmodquestions.php?func=allow&id='
.	$row['id'] . "'>Allow</a>";
echo " &bull;";
echo "<a href='adminmodquestions.php?func=deny&id='
.	$row['id'] . "'>Deny</a>";
echo "</td>";
echo "</tr>";
echo "</table>";
break;
```

# The allow Block

To accept a question, add the allow block:

```
echo "</table>";
break;

case "allow":
	$validid = set_validid();
	
	$modqsql = "UPDATE questions SET active = 1 WHERE id = "
	.	$validid . "";
	$modq = mysql_query($modqsql);
	
	header("Location: " . $config_basedir .
	"adminmodquestions.php?func=main");
break;
```

This block updates the question and sets the active field to 1 to make the question live. The page then redirects to the main block of *adminmodquestions.php*.

# The deny Block

To deny a question, the process is split into two parts. The first part asks the user if she is sure that she wants to reject the question. See Figure 9-13.

![](bbox=[0.1, 0.78, 0.8, 0.835])

FIGURE 9-13 Before denying a question, be sure this is what the user wants.

Add the code for this section: