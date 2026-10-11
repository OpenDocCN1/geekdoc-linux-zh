Now check if parent is set to 1. If it is, the user has clicked a category that can contain a number of subcategories. When this happens, display all the stories in the parent category as well as all of the subcategories. If the selected category is not a parent, return the stories for that specific category. Add the SQL for this:

```
```php
$parentres = mysql_query($parentsql);
$parentrow = mysql_fetch_assoc($parentres);

if($parentrow['parent'] == 1) {
    $sql = sprintf("SELECT stories.* FROM stories INNER JOIN cat_relate ON stories.cat_id = cat_relate.child_id WHERE cat_relate.parent_id = %d UNION SELECT stories.* FROM stories WHERE stories.cat_id = %d;", $currentcat, $currentcat);
} else {
    $sql = "SELECT * FROM stories WHERE cat_id = " . $currentcat . ";";
}
```
```

If the category is a parent, a large query is constructed to return all the stories. This query is really two queries that are cleverly stuck together. The first part (`SELECT stories.* FROM stories INNER JOIN cat_relate ON stories.cat_id = cat_relate.child_id WHERE cat_relate.parent_id = <id>`) uses a join to get all stories where parent_id is set to $currentcat. The second part (`SELECT stories.* FROM stories WHERE stories.cat_id = <id>`) selects stories that are a parent category.

The two parts are wedged together in the same query by using the UNION keyword, which hooks together two queries that use the same types of columns. This can be useful in cases such as this one, when you need to perform two SELECT queries on the same tables.

This large query is constructed inside the `sprintf()` function, which is used when you want to replace part of a string with another string or variable. In this case, you want to add $currentcat at the right points in the query. To do this, the `%d` (called a *type specifier*) in the string is replaced by the variables indicated at the end of `sprintf()`—in this case, $currentcat. Different types of variables use different type specifiers, and you can indulge your type specifier curiosity at www.php.net/sprintf.

In the else, a query is constructed if the selected category is not a parent, and it simply returns the stories for that specific category.

Run the relevant query: