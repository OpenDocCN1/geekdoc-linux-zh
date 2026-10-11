If you think about how this page should be designed, it seems logical to list the categories and let the user click on one to see any related blog entries (see Figure 4-7). This functionality is similar to a tree view in a file manager: The directories are listed, and then you click one to see the files and subdirectories.

![](bbox=[0.08, 0.21, 0.92, 0.65])

**FIGURE 4-7** Click any category to view the entries in that category.

On `index.php` and `viewentry.php`, you made the category a link to a page called `viewcat.php`, and the ID of the category was passed as an `id` GET variable. To get started, create a new file called `viewcat.php` and add the following code:

```
```php
require("config.php");
if(isset($_GET['id']) == TRUE) {
    if(is_numeric($id) == FALSE) {
        $error = 1;
    }
}
```
```