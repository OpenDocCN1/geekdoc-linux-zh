```
```php
else
{
    $error = $res->body->Errors->Error->Message;
    print("Could not add category: ${error}\n");
}
?>
```
```

Now we can use these command scripts to set up some sample data. First, we set up the domains:

```
```
$ create_domain.php
Domain cl_cities created.
Domain cl_categories created.
Domain cl_items created.
```
```

Then, we add some cities:

```
```
$ php add_city.php Bethesda MD
Added city Bethesda in MD
$ php add_city.php Redmond WA
Added city Redmond in WA
$ php add_city.php Boise ID
Added city Boise in ID
$ php add_city.php "San Francisco" CA
Added city San Francisco in CA
```
```

And then, we add the categories:

```
```
$ php add_category.php Cars Trucks Homes Furniture
Added category Cars
Added category Trucks
Added category Homes
Added category Furniture
```
```

If you remember from Chapter 8, each call to SimpleDB's `select` method can return up to 2,500 results, depending on the size and number of attributes returned. However, it is likely that we'll have to run SimpleDB queries that might produce long lists of results. So, let's create a function to make it easier to capture and process result sets of any size. Here's the code for the `runQuery` function: