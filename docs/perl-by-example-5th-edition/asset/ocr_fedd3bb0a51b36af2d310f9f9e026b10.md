# EXAMPLE 15-38 (CONTINUED)

```
# Show the user the table after it is updated
print "\nData for $team_name after update:\n";
10 $sth=$dbi->prepare(qq/SELECT * FROM teams
 WHERE name=?/);
   $sth->execute($team_name);
   while((my $name, my $wins, my $losses) = $sth->fetchrow_array()){ 
      print "\t\twins=$wins\n";
      print "\t\tlosses=$losses\n\n";
   }
   
   $sth->finish();
   $dbi->disconnect();
```

(Output)
*What is the name of the team to update?* Chico Hardhats
Data for *Chico Hardhats* before update:
	wins=15
	losses=3

How many games has *Chico Hardhats* won since the last update? *1*
How many games has *Chico Hardhats* lost since the last update? *2*
Data for *Chico Hardhats* after update:
	wins=16
	losses=5

# EXPLANATION

+   1. The user is asked to enter the name of the team in the *teams* table that he will edit.
+   2. A `SELECT` statement is issued to retrieve selected data in the *teams* table.
+   3. Before performing the update, the table will be displayed to see it in its current state.
+   4. The counter will keep track of how many records were returned.
+   5. If the count is zero, nothing was returned from the `SELECT`, and the program will die with an error message.
+   6. The user is asked to enter the number of games that have been won since the last update occurred.
+   7. The user is asked how many games have been lost since the last update.
+   8. The DBI do method is used to prepare and execute the SQL UPDATE statement. It returns the number of rows that were affected by the update. This statement will update the wins column in the *teams* table.
+   9. This update is the same as the last one, except it increases the number of losses.
+   10. After the database table has been updated, this `SELECT` statement is reissued to show the user the table after it was edited.