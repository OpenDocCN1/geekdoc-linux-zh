Figure 12-14 shows the relationships among the DTML methods search_names_form and search_lastnames_report and the Z SQL method search_last-names.

![](bbox=[0.238, 0.115, 0.803, 0.298])

Figure 12-14: Interrelationship of the DTML and SQL methods

To summarize this process,

+   1. The user uses search_lastnames_form to submit the lastname value to the method search_lastnames_report.

+   2. The search_lastnames_report calls the Z SQL method search_lastnames, which creates an SQL statement that is sent to the MySQL database through the database adapter.

+   3. The search_lastnames_report returns the matching records to search_lastnames_report, which creates a table to display them to the user. This table is returned as the report web page.

Listing 12-14 shows the code for the DTML method search_lastnames_form. In search_lastnames_form, the DTML method searchinterface (Z Search Inter-face) is called as soon as you click the Submit Query button, as shown in bold.

# Listing 12-14: search_lastnames_form

```
<dtml-var standard html_header>
<table>
<tr><th valign="top">last name:</th</th>
<td><form action="search_lastnames_report">
  <input type="text" name=lastname>
  <input type="submit" value=" Go">
</form></td>
</tr>
</table>
<dtml-var standard html_footer>
```

Now, if you run search_lastnames_form and enter 5 Slides in the last name field, you'll see the output shown in Figure 12-15.