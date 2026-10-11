If $VALIDAUCTION is equal to 1, a switch statement checks the value of the error GET variable, and the page displays the relevant error.

Add the form:

```
```code
 break;
 }
 ?>
```

```php
<?php echo pf_script_with_get($SCRIPT_NAME);
?> method="post">
 <table>
 <tr>
 <td><input type="text" name="bid"/></td>
 <td><input type="submit" name="submit" value="Bid!"/></td>
 </tr>
 </table>
 </form>
```

```

If $VALIDAUCTION is not set to 1, inform the user that the auction has ended:

```
```php
 <table>
 </form>
 ```
 ```code
 <?php
 } else {
 echo "This auction has now ended.";
 }
```

```

After the bid box, it is helpful to list a history of bids and the users who placed them:

```
```php
 } else {
 echo "This auction has now ended.";
 }
 $historysql = "SELECT bids.amount, users.username FROM bids,
 users WHERE bids.user_id = users.id AND item_id = "
 . $validid . " ORDER BY amount DESC";
 $historyresult = mysql_query($historysql);
 $historynumrows = mysql_num_rows($historyresult);

if($historynumrows >= 1) {
 echo "<h2>Bid History</h2>";
 echo "<ul>";
 while($historyrow = mysql_fetch_assoc($historyresult)) {
 echo "<li>" . $historyrow[‘username’] . " - "
 . $config_currency . sprintf(‘%.2f’, $historyrow[‘amount’]) . "</li>";
 }
 echo "</ul>";
}
```
```