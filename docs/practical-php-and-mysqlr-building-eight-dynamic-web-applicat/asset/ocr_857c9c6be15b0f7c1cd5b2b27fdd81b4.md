A query is created to gather the subject information and the username that maps to the **subjects.owner_id** field. In previous projects the join was made using the **WHERE** clause in the SQL, but here you are using the **LEFT JOIN** syntax. The following paragraph describes how the syntax works:

Select the username and subject information (**SELECT users.username, subjects.\*** ) from the **subjects** table (**FROM subjects**) and then join the **subjects** and **users** tables (**LEFT JOIN users**) with the relevant condition (**ON subjects.owner_id = users.id**) in which the subject id is the same as $\text{\$validsub** (WHERE subjects.id = $\text{\$validsub.**)

When writing joins, you can use a variety of different types of join (**INNER, OUTER, LEFT**, and **RIGHT**), with **INNER** and **LEFT** as the most common variants. An **INNER** join connects tables with the conditions that you specify. A **LEFT** join performs the same process but also fills in any mismatched fields with **NULL** values. Check the data returned to see if the subject has an owner. If 0 is returned, no owner exists:

```
```
echo "<h1>" . $subrow['subject'] . " </h1>";

if ($subrow['owner_id'] == 0) {
    echo "This subject has no owner.";
}
```
```

# NOTE

# Using the LEFT Join on this Page

The reason for using the **LEFT** join on this page is important. If the **subjects** table has an **owner_id** set to something other than 0, an **INNER** or **LEFT** join can relate the **owner_id** to the **user id** in the **users** table. If, however, the subject has no owner and the **owner_id** is set to 0, an **INNER** join fails because no user with the id 0 exists in the **users** table. When you use a **LEFT** join, this mismatch still returns the data, but the mismatched information is set to **NULL**.

In this project, you use a combination of joins that use the **JOIN** and **WHERE** syntax. This ensures that you are exposed to both methods of creating joins.

If the subject has no owner, check to see if a user is logged in and display a link to the subject ownership page:

```
```
if ($subrow['owner_id'] == 0) {
    echo "This subject has no owner.";
}
```
```