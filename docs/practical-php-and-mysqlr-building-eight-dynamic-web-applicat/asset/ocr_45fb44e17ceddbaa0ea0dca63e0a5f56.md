If so, TODAY is added to the cell to indicate the current day. Otherwise, only the date is displayed.

Before you add the cells that contain the events, pad out the days before the first of the month:

```
```
}

echo "</tr>";

echo "<tr>";
for($f=0;$f<=$sweekday;$f++) {
	echo "<td class='cal' width='110' height='10'>";
	if($newcounter <= $ndays) {
}
	echo "</td>";
}

		For the remaining cells on the first row, grab the events from the database and
		display them:
	echo "</td>";
}

for($f=0;$f<=$dayleft;$f++) {
	echo "<td class='cal' width='110' height='40'>";
			$dat = $year . "-" . $month . "-" . $newcounter;
		echo "<a class='cal' href='#' onclick="newEvent("
			. $date . "')\"></a>";

			$eventsq1 = "SELECT * FROM events WHERE date = '
			. $date . "'";
			$ventres = mysql_query($eventsq1);

			while($sevenrow = mysql_fetch_assoc($sevenres)) {
				echo "<a class='deletevent' href='delete.php?id='
				. $sevenrow['id'] . "'" onclick='return confirm("Are you
				sure you want to delete ". $sevenrow["name"] . "?");'>x</a>";
				echo "<a class='event' href='#'
			onclick='getEvent(" . $sevenrow["id"] . "')>"
			. short_event($sevenrow["name"]). "</a><br />";
			}
		echo "</td>";
		$newcounter++;
}

echo "</tr>";
```
```