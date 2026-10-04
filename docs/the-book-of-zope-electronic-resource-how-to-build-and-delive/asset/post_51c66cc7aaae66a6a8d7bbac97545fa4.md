
## 12.4.3 The insert_sql Method

Now you'll create a Z SQL method userInsert_sql.

You can create an SQL method only if the database connection is active.

- 1. From the folder's add menu, select Z SQL Method. The management screen shown in Figure-12-5 appears.

![](img/43a28cce5475b2f487bf455365567fb6_256_0.png)

Figure 12-5: Creating an SQL insert method

- 2. For the id, editor, select MySQL_database_connection.
- 3. In the Connection Id field, enter all values to be passed to this SQL method, as follows (be sure to leave one space between each of the individual arguments):
- 4. In the Arguments field, enter ...

userid firstname lastname address zipcode city telephone

- 5. In the Query field, enter the following SQL statements:

```sql
INSERT INTO user
(userid,firstname,lastname,address,zipcode,city,telephone)
VALUES
  ('<dml-var name="userid" sql_quote',
  '<dml-var name="firstname" sql_quote',
  '<dml-var name="lastname" sql_quote',
  '<dml-var name="address" sql_quote',
  '<dml-var name="zipcode" sql_quote',
  '<dml-var name="city" sql_quote',
  '<dml-var name="telephone" sql_quote'>)
```

- 6. Click Add and Edit. You should see the screen in Figure 12-6.

![](img/43a28cce5475b2f487bf455365567fb6_257_0.png)

Figure 12-6: The Z SQL method used insertUser_sql

> NOTE The sql_quote attribute of dml-var used above prevents characters significant to SQL, as the single quote ('') or semi-colon (;), from causing errors if they are submitted from the form. Otherwise the name "OConnell" could not be successfully submitted, for instance.

## 12.4.4 Testing Your SQL Methods

To test your SQL methods, click Change and Test. You should see the form in Figure 12-7, where you can enter the values for your user and then write them to the table to test the Z SQL method.

If the test above succeeds, you can now test your custom create user form, as follows:

- 1. View the HTML document userAddForm_html and enter the data as shown in Figure 12-8.
- 2. Click Create.
The data from the form is sent to the userAddr_html method, which in turn calls the Z SQL method just created (insertUser_sql) to insert the data into the user table of the MySQL database, as shown in Figure 12-9.

### insert Input Data

Enter query parameters
UserID
Username
Lastname
Address
Zipcode
City
Telephone

![](img/43a28cce5475b2f487bf455365567fb6_258_0.png)

Figure 12-7: Testing the SQL insert method

| First name | Jim |
| :--- | :--- |
| Last name | Slides |
| Address | PO Box 556 |
| City | Concord |
| ZIP code | CA 94518 |
| Phone | 721-9071 |

Figure 12-8: Creating a user

![](img/43a28cce5475b2f487bf455365567fb6_258_1.png)

Figure 12-9: Communication between Zope and myDB

Sending data from an html form to the database through Zope actually involves several steps:

- 1. The form is completed and submitted by the client to Zope.
- 2. Zope encapsulates the form values in the REQUEST object and calls the object that is the target of the form's action URL.
- 3. The form's target object then calls a Z SQL method, which creates an SQL statement to send to the database backend.
- 4. The SQL statement sends the SQL statement to the database backend using a database adapter.
- 5. The backend database executes the SQL statement and returns the results (if any) to Zope via the database adapter.
- 6. The Z SQL method receives the results from the database and returns them to the form's target object.
- 7. The form's target object displays the results or takes action based on them.

## 12.5 Querying the Database Using Zope

Let's now create a search screen with which you can perform a query to request information from the database. To do so, you'll need:

- Z SQL methods that contain the SQL code to perform the search
- A Search interface that uses this SQL method and formats its output
- An input field for entering search

### 12.5.1 Creating SQL Methods for Searching

First, create the Z SQL method search_lastnames (shown in Figure 12-10) to query the user table by last name.

![](img/43a28cce5475b2f487bf455365567fb6_259_0.png)

Figure 12-10: Z SQL method search_lastnames

### 12.5.2 The sqltest Tag

The sqltest DTML tag is a special tag that can only be used in SQL methods. The sqltest tag inserts an SQL comparison between a table's column and a value supplied as an argument. The column name, lastname, is used in the sqltest tag:

```
<sqltest name="lastname" type="string">
```

The argument with which the column is compared is also called "lastname." All arguments used as variables in SQL methods must be specified explicitly in the Arguments field. Assuming the value "Slides" is supplied as the value of the lastname argument, the above sqltest tag would insert the following text into the statement: `lastname='Slides'`

To create the SQL method search_firstnames, use the same approach. The general syntax is:

```
<sqltest name="name" column="column" type="datatype" optional>
```

To create an SQL method to search for first names, assuming an argument "name" enter the following code into the Z SQL method:

```sql
SELECT * FROM user WHERE <sqltest name="name" type="nb">
```

| Id | search_firstnames |
| :--- | :--- |
| Title | MySQL_database_connection |
| Connection Id | |
| Arguments | name |
| Query Template | SELECT * FROM user WHERE <sqltest name="name" column="firstname" type="nb"> |

Figure 12-11: SQL search_firstnames method

Figure 12-11 shows the completed search_firstnames Z SQL method. Table 12-3 lists the attributes of the sqltest tag.

### Table 12-3: Attributes of the sqltest Tag
| Attribute | Description |
| :--- | :--- |
| name | Name of the variable to be written in the table. |
| column | Name of the column in the table. |
| multiple | A flag that indicates whether several values can be used. |
| optional | A flag that indicates whether the test is optional. If no value exists for a variable or if an empty string is used, operations are performed. |
| op | Parameter indicating the comparison operation. The standard value is |. The following comparison operations can be used. Others may also be available for your database, consult your documentation for details. |
| type | The data type of the variable to be inserted, such as string, int, float, nb. (nb stands for nonblank and represents a string longer than 0 characters.) |

### 12.5.3 The sqlvar Tag

The sqlvar is another DTML tag that is used only in SQL methods. This tag is used to ensure that certain value types, such as string, are correctly interpreted in the SQL text. Data values are converted (if possible), strings are properly quoted, special characters are escaped (as with the sql_quote option of dml-var), and numeric values are passed according to the conventions of your database. Use sqlvar in place of dml-var in your SQL methods.

The syntax to use is:

```
<dml-sqlvar name="name" type="datatype" optional>
```

Table 12-4 lists the attributes of the sqlvar tag.

### Table 12-4: Attributes of the sqlvar Tag
| Attribute | Description |
| :--- | :--- |
| name | Name of the variable to be written in the table. |
| type | The data type of the variable to be inserted, such as string, int, float, nb. (nb stands for nonblank and represents a string that has a length greater than 0 characters.) |
| optional | Inserts nothing if the value is omitted or cannot be successfully converted to the type specified. If this attribute were omitted, a Zope error would occur. |

## 12.6 Creating a Search Interface

Although you certainly may, you do not need to create your own database search interface manually. Zope provides you with a search interface to reduce some of the workload for you. To create a search interface with Zope’s help, follow these steps:

- 1. Select Z Interface from the folder's add menu, then enter the values shown in Figure 12-12.

![](img/43a28cce5475b2f487bf455365567fb6_262_0.png)

Figure 12-12: Creating a search interface

- 2. The top field contains a list of all available SQL methods (and other searchable objects like ZCatalogs). From this list, select the methods you want your search interface to access. For this example, select the SQL method search_lastnames.
- 3. In the Report Id field, enter search_lastnames_report.
- 4. In the Search Input Id field, enter search_lastnames_form.
- 5. Click Add to have Zope create the DTML method searchinterface.

### 12.6.1 Creating an Input Screen for the Search

Suppose you want to use the table in myDB database for records for last name. The search screen should look like Figure 12-13.

![](img/43a28cce5475b2f487bf455365567fb6_262_1.png)

Figure 12-13: Search screen for search_lastnames_form
