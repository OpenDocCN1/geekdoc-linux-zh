# **EXAMPLE 8-10** Continued.

```
    echo $row['name'];
    echo "<p> . $row['description'] . "</p>";
    echo "<p><strong>Date:</strong> " . date("D jS F Y"),
    strtotime($row['date']) . "<br />
    echo "<strong>Time:</strong> " . $row['starttime'] . " - " . $row['endtime'] . "</p>";
}
?>
```

Within this script, you check to see if the **action GET** variable is equal to *getevent*. The *action* variable is used to distinguish among different features on page. You could create another block of code for a different action.

Within the *if*, the record from the *events* table with the same id as the *id GET* variable is returned and displayed. When this functionality is complete, the event information is displayed in the sidebar when the user clicks an item, as shown in Figure 8-6.

![](bbox=[0.09, 0.52, 0.92, 0.86])

**FIGURE 8-6** The dynamic nature of Ajax is not given justice by a static screenshot, but rest assured, it makes the application feel much sleeker.